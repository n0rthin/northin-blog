Requirements:
#### Basic experiment setup
Solution needs to provide a way to create a A/B test. Set start/end date, name

#### Frontend & backend
Solution works on the backend and frontend

#### Targeting
We need to be able to run experiment only on a subset of users (new users, clients, only users on specific plans, desktop/mobile, etc.)

#### Minimal effect on latency 
Since ab testing infrastructure will be invoked on each user visit it must have as low effect on latency as possible

#### Feature toggling 
There should be a way to enable/disable feature for specific user group

#### Feature roll out/back
There should be a way to rollout feature for all users or disable it completely after experiment is done

#### Sample size calculation 
We need to calculate duration of the experiment and for that we need to know sample size

#### [[Statistical significance]] calculation 
After experiment is finished we need to calculate difference between control and experiment group and whether it's significant or not

#### Post-experiment analysis 
All data tracked during an experiment must be tied to one of the experiment groups so we can gain deeper insights

### 1. Optimizely + Mixpanel Experiments + online stats calculators
**Prices**
Optimizely - need to contact sales
Mixpanel - need to contact sales
Online stats calculators - free
**Solution**
Basic experiment setup - optimizely has [solution for ab tests](https://docs.developers.optimizely.com/full-stack/docs/run-a-b-tests)
Frontend & Backend - optimizely has [react sdk](https://docs.developers.optimizely.com/full-stack/docs/javascript-react-sdk) and [nodejs sdk](https://docs.developers.optimizely.com/full-stack/docs/javascript-node-sdk)
Targeting - optimizely has [audience](https://docs.developers.optimizely.com/full-stack/docs/target-audiences) feature
Latency - optimizely sdk [caches](https://docs.developers.optimizely.com/full-stack/docs/welcome#supported-functionality) all needed data in-memory
Feature toggling - optimizely has [feature toggles](https://docs.developers.optimizely.com/full-stack/v2.1/docs/use-feature-flags)
Feature rollout - optimizely has [feature rollouts](https://docs.developers.optimizely.com/full-stack/docs/introduction-to-rollouts)
Sample size calculator - online stats calculators: [for conversions](https://www.stat.ubc.ca/~rollin/stats/ssize/b2.html) [for other metrics](https://www.stat.ubc.ca/~rollin/stats/ssize/n2.html)
Statistical significance - optimizely has [stats engine](https://www.optimizely.com/statistics/) that builds [results page](https://docs.developers.optimizely.com/full-stack/v2.1/docs/analyze-results)
Deeper analysis - optimizely won't have all of our data, so we should use mixpanel for that. Mixpanel has [experiment report](https://help.mixpanel.com/hc/en-us/articles/360038439952-Experiments-Report) which helps breakdown any data by control/experiment groups. But it requires enterprise plan 

### 2. Optimizely + Mixpanel free plan + online stats calculators
**Price**
Optiizely - contact sales
Mixpanel - free
Online stats calculators - free
**Solution**
Optimizely - same as in the previous solution
For deeper analysis we would use mixpanel. They have built in solution called Mixpanel Experiments Report
It has a special event $experiment_started which we can send for each user when experiment started. Mixpanel will then recognize it and display each tracked experiment in the UI. Then we can look into data tracked during experiment period and also check breakdown for different experiment groups. We could build any metrics and mixpanel will calculate difference for groups and statistical significance for it
But this functionality requires enterprise plan.
I think we could track experiments and groups with custom events and fields and then use existing breakdown feature to look for differences. As for significance or any other stats I could use 3rd party calculators like ones for sample size calculation
We could still send $experiment_started just in case we buy enterprise plan so old experiments will be available

### 3. Google optimize
**Prices**
Google optimize - need to contact sales
Online stats calculators - free
**Solution**
Basic experiment setup - google optimize provides ability to setup a/b tests
Frontend & Backend - optimizely has [react sdk](https://docs.developers.optimizely.com/full-stack/docs/javascript-react-sdk) and [nodejs sdk](https://docs.developers.optimizely.com/full-stack/docs/javascript-node-sdk)
Targeting - optimizely has [audience](https://docs.developers.optimizely.com/full-stack/docs/target-audiences) feature
Latency - optimizely sdk [caches](https://docs.developers.optimizely.com/full-stack/docs/welcome#supported-functionality) all needed data in-memory
Feature toggling - optimizely has [feature toggles](https://docs.developers.optimizely.com/full-stack/v2.1/docs/use-feature-flags)
Feature rollout - optimizely has [feature rollouts](https://docs.developers.optimizely.com/full-stack/docs/introduction-to-rollouts)
Sample size calculator - online stats calculators: [for conversions](https://www.stat.ubc.ca/~rollin/stats/ssize/b2.html) [for other metrics](https://www.stat.ubc.ca/~rollin/stats/ssize/n2.html)
Statistical significance - optimizely has [stats engine](https://www.optimizely.com/statistics/) that builds [results page](https://docs.developers.optimizely.com/full-stack/v2.1/docs/analyze-results)
Deeper analysis - optimizely won't have all of our data, so we should use mixpanel for that. Mixpanel has [experiment report](https://help.mixpanel.com/hc/en-us/articles/360038439952-Experiments-Report) which helps breakdown any data by control/experiment groups. But it requires enterprise plan 

### 4. In-house solution + Mixpanel free plan + online stats calculators
We could build everything on our own. 

