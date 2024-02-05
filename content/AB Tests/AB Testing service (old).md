## Version 1
### Problem
In order to launch ab tests in our product we need a way to assign user to control/experiment groups. 
The solutions is to introduce new data structures which will contain information about active experiments and how users participate in them. Also we need a new service responsible for experiment-related work.

### What
**Data structures**
New entity: **Experiment**
| Name | Type | Required |  
|:-:|:-:|:-:|
| id | string | yes |
| name | string | yes |
| featureToggleName | string | yes |
| active | boolean | yes |
| stardDate | Date | yes |
| endDate | Date | yes |
| createdAt | Date | yes |
The experiment entity will contain information on the experiment. For now, it will be read-only meaning there won't be a way to create or update experiment in the backend.
Experiments information will be added to the DB by the person responsible for the ab test. After that, backend will use this info to navigate users through the experiment.

New field in user model: user.experiment
user.experiment is an object with following structure:
| Name | Type | Required |  
|:-:|:-:|:-:|
| activeExperiments | array of string | yes |
Each string in the user.experiment.activeExperiments has following pattern:
`{experiment_name}-{a|b}`


## Version 2
Stateless deterministic bucketing using hashing instead of random assignment which requires storing state.
Uses rules to target users
Each time a user is exposed to an experiment update profile in the mixpanel.
Cache experiments data in memory
Redis as single source of truth
Provide endpoint to access experiments data from frontend
Do not render frontend until experiments are loaded
Cache experiments data locally
MurmurHash - 4ms on average to generate 100000 hashes. 4/100000 = 0,00004ms per hash = 0,00000004s = 40nanoseconds