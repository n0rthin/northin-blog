### Problem
In order to launch ab tests in our product we need a way to assign a user to control/experiment groups. We're going to achieve it by implementing a new piece of infrastructure that will store information about active experiments and will be responsible for targeting and bucketing users into different groups.

### What
**Experiments data**
We'll use Redis as single source of truth on active experiments.
Redis is the best choice in this case since this is a in-memory storage meaning it'll have minimal effect on latency.
Backend we'll retrieve updated state from [redis keyspace notifications](https://medium.com/@micah1powell/using-redis-keyspace-notifications-for-a-reminder-service-with-node-c05047befec3)
Every time a key with experiments data changes, redis will send an event to the backend. Then, backend must store this data in its own memory.
Experiments data must be only accessed from backend memory, additional network requests to redis should not be sent.
Experiment data is an object with following structure:
Experiment {
	key: string;
	active: boolean;
	startsAt: Date
	targetingSchema: [fastest-validator](https://www.npmjs.com/package/fastest-validator) schema
}
**Targeting**
We should be able to launch an experiment only for certain group of users (only paying clients, only new user, only end customers, etc).
We'll do it by running a schema validation on user before assigning them to control or experiment group. We'll use [fastest-validator](https://www.npmjs.com/package/fastest-validator) for that purpose because it's fast. 
So experiment object will have a field `targetingSchema` which will contain a schema for the fastest-validator. Then we run validation on the user object. If validation passes, user is part of the experiment, otherwise everything should be as usual for the user.

**Experiment service**
Implement a new service called ExperimentService. It should have following methods:
`updateExperimentsData` - this method should take experiments data as argument and store it in the memory for future usage. 
`activate` - activates an experiment for the user and returns a group the user belong ("control", "variation" or null if user is not part of the experiment).
Receives following arguments:
- experimentKey - a string containing experiment key
- userId - a string containing user id
- attributes - an object that will be validated by `experiment.targetingSchema`
activate method should do following:
1. Is there an experiment that has `active` === true, `startsAt` in the past and `key` equal to `experimentKey`? If not return null
2. If there is such experiment we should check targeting next. Run validation against object in `attributes` argument using `experiment.targetingSchema`. Validation passes? If not return null
3. If user passes targeting then we need to determine bucket which they belong. We'll do it by using [murmurhash](https://www.npmjs.com/package/murmurhash). murmurhash is a fast hashing algorithm (~40ns per hash) which takes a string as input and returns random integer between 0 and 2[^32]. But it always the same number for the same string. Construct a string using experiment key and user id like this: "{experimentKey}{userId}". Execute murmurhash with the string. Divide resulting number by 2^32 and multiply by 10000. If the number in the end is less then or equal 4999 return "control" string otherwise return "variant" string.
4. Before returning string from the last step `activate` method should send an impression event to Segment
`getVariation` - this method is the same as `activate` but it should not send impression event in the end. It will be used to get user variation without activating experiment for them.

**API**
Create a new endpoint GET /api/experiments. It should return experiments data currently stored in the memory. Response should include `cache-control` header so data is cached by browser. Set cache expiration to 4 hours

**Frontend**
During initial app loading fetch data from /api/experiments.
Do not render app until experiments data is loaded
Implement a function that does the same what ExperimentService.activate does.
Implement hooks that use this function so activate function could be used in components.

### Expected behaviour
Minimal effect on latency and performance
Redis is single source of truth on experiments data
Stateless - the code should not store information about experiments in users so we can avoid additional requests to DB. Use hashing instead which gives the same result every time.
Should target users based on schema in experiment object.
Frontend should cache experiments data
