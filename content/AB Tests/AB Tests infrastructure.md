Each experiment must have a document in the `experiments` collection in DB.

**Experiment entity**

| Name | Type | Required |  
|:-:|:-:|:-:|
| id | string | yes |
| name | string | yes |
| featureToggleName | string | yes |
| active | boolean | yes |
| stardDate | Date | yes |
| endDate | Date | yes |
| createdAt | Date | yes |

Every user should have a field `experiment` which includes an object with information on experiments in which user is participant. Structure of the object looks like this:

*How do we decide whether user is part of the experiment or not? How we can target different segments of users? For example, if we want to launch ab test only for mobile user or specific browser?*
When we execute procedure that sorts users into experiment we need to provide it with data from client

If we don't have enough data to decide whether user should participate in experiment or not then user should not be participant of the test.

*How we segment and target users in relation to AB tests?*

