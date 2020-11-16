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

1. In the first half of the experiment, API developer makes changes to the API and communicates to the API consumers manually without using the Sync-Ends. 
This scenario mimics the **Not It** part where there is no automated way of communication.

2. In the second half of the experiment, API developer makes changes to the API and Sync-Ends takes care of communication. 
This scenario mimics the **It** part where any changes are notified to the API consumers in the automated way.

During these two phase, job of the API developer remain the same which is to note the changes as when they are communicated.
To capture the precise time when consumers gets the notification, we asked participants to direct message one of the session conductor about the notified changes.

## Material
For this experiment, we have used:
* A general postman account with a single collection but multiple APIs. 
    - API developer make periodic changes to this APIs and the Sync Ends service takes care of the rest.
* A slack channel along with configured Slack Bot which interacts with the Sync-Ends service.
    - Our participants who are API consumers, are added to this channel.

## Observations

To draw meaningful conclusions out of this experiment, we have used the following quantitative and qualitative observations.

### Quantitative measures
1. Time when the API developer published a particular change.
2. TIme when the API consumer gets notified about the change made in the above point.

For each phase of the experiment, we have made 5 changes to the API and noted the time when consumer gets notified. 
Since each experiment consists of two phases, we have a total of 10 observation for each experiment.
That makes a total of 100 observations since we have conducted this experiment with 10 participants.

### Qualitative measures
1. How easy it is for API consumer to find the changes (In presence of the Sync Ends system v/s Without the system)

This can be a crucial observation since automated change notifications follows a particular structure for each communication.
API consumer over the time gets used to this structure and can easily extract out the changes made. 
On the other hand, If such structure is not followed in the manual change notification, it is a lot harder for consumer to adapt since developers change over the time and so does their communication type.

## Analysis
It was clear from our set of observations that using sync-ends, user was able to decrease the overall time by a huge
margin, but in order to support our visible claims we decided to run t-test on both the probability distribution to
be sure whether the means of both the distribution were same or not. Here the null hypothesis is that the two means
are equal, and the alternative is that they are not. 

1. The following image gives us an idea about the overall time distibution after using sync_ends.
<img src="https://github.com/urvishvasani/Sync-Ends/blob/master/images/with_syncends.PNG" height="400" width="650"/>

2. The following image gives us an idea about the overall time distibution before using sync_ends.
<img src="https://github.com/urvishvasani/Sync-Ends/blob/master/images/without_syncends.PNG" height="400" width="650"/>

Based on the p-value obtained from above data, it can be concluded that we can reject the null-hypothesis which would
support the claim of both the means are different.

* More details can be observed from this [code](https://github.com/urvishvasani/Sync-Ends/blob/master/statistical_analysis.ipynb). 

### Quantitative analysis
When we asked participants about their preference about whether they got convinced to use the Sync-Ends or not, we got the following results:
(5 being the Highest preference and 1 being the lowest preference.)

<img src="https://github.com/urvishvasani/Sync-Ends/blob/master/images/hist.PNG" height="400" width="650"/>

As we can see from the histogram, 80% participant prefers the Sync-Ends over the manual communication of changes. 
The rest 20% are fine with or without Sync-Ends as long as they get the change notifications properly.

## Conclusion
From the results obtained in the analysis section, we can confidently conclude that overall latency of communication when using Sync-Ends is much lower than when not using Sync-ends.
and majority of the participants prefers the Sync-ends service over the manual form of communication.

## Threats to Validity

