# Phase 3 Experiment

In this experiment, we evaluated the performance improvement of the API consumer in a rapidly developing environment.

## It vs Not It
In the presence of this sync-ends service, once the change is made to the API in the postman collection, the changes are directly fetched from the Postman and a slack message is sent in the channel with a detailed diff notifying the API consumer of this change.

In the absence of this service, the developer need to manually notify changes to the API consumer and if the developer forgets to do so, the API consumer will be unaware of API changes and as a result, the API consumer will have a crash when their application tries to call the updated API with old parameters.

## Methodology
Each experiment ran in pairs where one of the session conductor from our team behaved as the API developer and the participant acted as the API consumer.

The job of the developer is to change API schemas in Postman which mocks the behaviour that a change has been made in the serving of API in actual codebase.

The job of the API consumer is to monitor those changes and note them down which mocks the behaviour that the API consumer is now aware that a change need to be made in the codebase where this API is used.

The experiment is divided into two phases:

1. 

2.

## Material
For this experiment, we have used:
* A general postman account with a single collection but multiple APIs. 
    - API developer make periodic changes to this APIs and the Sync Ends service takes care of the rest.
* A slack channel along with configured Slack Bot which interacts with the Sync-Ends service.
    - Our participants who are API consumers, are added to this channel.

## Observations

## Analysis
It was clear from our set of observations that using sync-ends, user was able to decrease the overall time by a huge
margin, but in order to support our visible claims we decided to run t-test on both the probability distribution to
be sure whether the means of both the distribution were same or not. Here the null hypothesis is that the two means
are equal, and the alternative is that they are not. 

1. The following image gives us an idea about the overall time distibution after using sync_ends.
<img src="https://github.com/uvasani/Sync-Ends/blob/master/images/with_syncends.PNG" height="500" width="800"/>

2. The following image gives us an idea about the overall time distibution before using sync_ends.
<img src="https://github.com/uvasani/Sync-Ends/blob/master/images/without_syncends.PNG" height="500" width="800"/>

Based on the p-value obtained from above data, it can be concluded that we can reject the null-hypothesis which would
support the claim of both the means are different.

* More details can be observed from this [code](https://github.com/urvishvasani/Sync-Ends/blob/master/statistical_analysis.ipynb). 
  

## Conclusion

## Threats to Validity

