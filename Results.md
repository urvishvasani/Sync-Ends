# Phase 3 Experiment

In this experiment, we evaluated the performance improvement of the API consumer in a rapidly developing environment.

## It vs Not It
In the presence of this sync-ends service, once the change is made to the API in the postman collection, the changes are directly fetched from the Postman and a slack message is sent in the channel with a detailed diff notifying the API consumer of this change.

In the absence of this service, the developer would need to manually notify changes to the API consumer. If the developer forgets to do so, the API consumer will be unaware of API changes. As a result, the API consumer will face a crash when their application tries to call the updated API with old parameters.

## Methodology
Each experiment was run in pairs where one of the session conductor from our team behaved as the API developer and the participant acted as the API consumer.

The job of the developer was to change the API schemas in Postman which mocks the behaviour that a change has been made in the serving of API in the actual codebase.

The job of the API consumer was to monitor those changes and note them down which mocks the behaviour that the API consumer was then aware that a change was needed to be made in the codebase where this API is used.

The experiment is divided into two phases:

1. In the first half of the experiment, API developer makes changes to the API and communicates to the API consumers manually without using the Sync-Ends service. 
This scenario mimics the **Not It** part where there is no automated communication.

2. In the second half of the experiment, API developer makes changes to the API and Sync-Ends takes care of communication. 
This scenario mimics the **It** part where any changes are notified to the API consumers in the automated way.

During these two phases, the job of the API developer remains the same which is to note the changes as when they are communicated.
To capture the precise time when consumers gets the notification, we asked participants to direct message to one of the session conductor about the notified changes.

## Material
For this experiment, we have used:
* A general postman account with a single collection but multiple APIs. 
    - API developer make periodic changes to this APIs and the Sync Ends service takes care of the rest.
* A slack channel along with configured Slack Bot which interacts with the Sync-Ends service.
    - Our participants who are API consumers, are added to this channel.

## Observations

To draw meaningful conclusions out of this experiment, we used the following quantitative and qualitative observations.

### Quantitative measures
1. Time taken when the API developer published a particular change.
2. Time when the API consumer gets notified about the change made in the above point.

For each phase of the experiment, we made 5 changes to the API and noted the time when consumer gets notified. 
Since each experiment consists of two phases, we have a total of 10 observation for each experiment.
That makes a total of 100 observations since we have conducted this experiment with 10 participants.

### Qualitative measures
1. How easy it is for API consumer to find the changes (In presence of the Sync Ends system v/s Without the system)

This can be a crucial observation since automated change notifications follows a particular structure for each communication.
API consumer over the time gets used to this structure and can easily extract out the changes made. 
On the other hand, If such structure is not followed in the manual change notification, it is a lot harder for consumer to adapt since developers change over the time and so does their communication type.

## Statistical Analysis

The bar plot given below shows compares average time taken to notify API user about change with Sync-Ends and without Sync-Ends. As seen in the plot, notifications via Sync-Ends was faster compared to notifications without Sync-Ends and not just slightly faster but faster by a huge margin.

<img src="https://github.com/urvishvasani/Sync-Ends/blob/master/images/bar.png" height="400" width="650"/>

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

<img src="https://github.com/urvishvasani/Sync-Ends/blob/master/images/hist.png"/>

As we can see from the histogram, 80% of the participants prefer the Sync-Ends over the manual communication of changes. 
The rest 20% are fine with or without Sync-Ends as long as they get the change notifications properly.

## Conclusion
From the results obtained in the analysis section, we can confidently conclude that overall latency of communication when using Sync-Ends is much lower than when not using Sync-ends.
and majority of the participants prefers the Sync-ends service over the manual form of communication.

## Threats to Validity

There are a few factors that affect the conclusion drawn from this experiment significantly. 
API development and consumption of that takes place over the longer time spam and to mimic the similar procedure in the 45 minute time frame is difficult.
There are two real life scenario which might contradict the concluded observations.

1. In real life, when API developers makes any changes to the API, it is not always the case that they notify the API consumers straight away.
There can be the scenarios where they have developed a particular API but didn't notified the consumers until the another dependent API is published and notified.
We tried to mimic this scenario making a change at a time t and notified the consumers after t+2 or t+3 minutes as and when it is required by the other API.
For example, in our experiment we first created an API to add the student's subject details but didn't notified the consumers. 
Later on, when we developed an API that lists the student's subject details and notified the consumer about that, we let the consumer complain about no provision for adding the subject details and then we notified them about the add subject details API.

2. We have used Slack channel to communicate any API changes to the consumer. During the experiment, API consumers (Participants) only had to observe the slack channel for any API changes.
However, in real life, consumer are not always looking at their slack channel for API changes, they can be busy in their own development.
To simulate this scenario, we asked API consumers (Participants) to write us a detailed message about the changes that they have been notified of.
So, it can be the case that when they are writing us for the past changes, they got notified about the new change.
Here writing us a detailed message about an API change can be linked with the time when they are doing their own development.

This way, we tried to mitigate any biases that might affect our conclusions.  
