## Overview
+ do machine learning like the great engineer you are, not like the great machine learning expert you aren't.

+ Most of the problems you will face, in fact, engineering problems. Even with resources of a great machine learning expert, most of the gains come from great features, not great machine learning algorithms. So, the basic approach is:
  + make sure your pipeline is solid end to end
  + start with a reasonable objective
  + add common-sense features in a simple way
  + make sure that your pipeline stays solid.


## Before Machine Learning
### Rule 1-Don't be afraid to launch a product without machine learning
+ if machine learning is not required for your product, don't use it until you have data.

### Rule 2-First, design and implement metrics

### Rule 3-Choose Machine Learning over a complex heuristic.
+ A simple heuristic can get your product out the door. A complex heuristic is unmaintainable.
Once you have data and a basic idea of what you are trying to accomplish, move on to machine
learning.

## ML Phase I: Your First pipeline
### Rule 4-Keep the first model simple and get the infrastructure right.
+ The first model provides the biggest boost to your product, so it doesn't need to be fancy. But
you will run into many more infrastructure issues than you expect. 
+ Choosing simple features makes it easier to ensure that:
  + The features reach your learning algorithm correctly
  + The model learns reasonable weights
  + The features reach your model in the server correctly.
  
### Rule 5-Test the infrastructure independently from the machine learning

### Rule 6-Be careful about dropped data when copying pipelines
+ Another common pattern is to only log data that was seen by the
user. Thus, this data is useless if we want to model why a particular post was not seen by the
user, because all the negative examples have been dropped.

### Rule 7-Turn heuristic into features or use them externally
+ These same heuristic can give you a lift when tweaked with machine learning. Four ways:
  + Preprocess using heuristic
  + Create a feature: Directly creating a feature from the heuristic is great. For example, if
you use a heuristic to compute a relevance score for a query result, you can include the
score as the value of a feature.
  + Mine the raw inputs of the heuristic.
  + Modify the label:This is an option when you feel that the heuristic captures information not currently contained in the label. For example, if you are trying to maximize the number of downloads, but you also want quality content, then maybe the solution is to multiply the label by the average number of stars the app received.
+ Do be mindful of the added complexity when using heuristics in an ML system. Using old heuristics in your new machine learning algorithm can help to create a smooth transition.


## Monitoring
### Rule 8-Know the freshness requirements of your system.
+ How much does performance degrade if you have a model that is a day old? A week old? A quarter old? This information can help you to understand the priorities of your monitoring.

### Rule 9-Detect problems before exporting models.
+ Do sanity check before you export the model.

### Rule 10-Watch for silent failures
+ Suppose that a particular table that is being joined is no longer being updated. The machine learning system will adjust, and behavior will continue to be reasonably good, decaying gradually.

### Rule 11-Give feature column owners and documentation.

## Your First objective

+ You have many metrics, or measurements about the system that you care about, but your machine learning algorithm will often require a single objective, a number that your algorithm is “trying” to optimize.

### Rule 12-Don’t overthink which objective you choose to directly optimize.
+ However, early in the machine learning process, you will notice them all going up, even those that you do not directly optimize. So, keep it simple and don’t think too hard about balancing different metrics when you can still easily increase all the metrics. Don’t take this rule too far though: do not confuse your objective with the ultimate health of the system.
+ And, if you find yourself increasing the directly optimized metric, but deciding not to launch, some objective revision may be
required.

### Rule 13-Choose a simple, observable and attributable metric for your first objective.
+ **The ML objective should be something that is easy to measure and is a proxy for the “true” objective**

### Rule 14-Starting with an interpretable model makes debugging easier
+ For example, in linear, logistic, or Poisson regression, there are subsets of the data where the average predicted expectation equals the average label (1 moment calibrated, or just calibrated) ???
+ However, remember when it comes time to choose which model to use, the decision matters more than the likelihood of the data given the model???

### Rule 15-Separate Spam Filtering and Quality Ranking in a Policy Layer
+ Keep in mind, filtering spam in search results should probably be more aggressive than filtering spam in email. Spam filtering is a different story. You have to expect that the features that you need to generate will be constantly changing. 
+ Keep in mind, filtering spam in search results should probably be more aggressive than filtering spam in email messages. Also, it is a standard practice to remove spam from the training data for the quality
classifier.

## ML Phase II: Feature Engineering
+ After you have a working end to end system with unit and system
tests instrumented, Phase II begins.
### Rule 16-Plan to launch and iterate.

### Rule 17-Start with directly observed and reported features as opposed to learned features.


### Rule 18-Explore with features of content that generalizes across contexts.
+ If you provide those statistics to the learner, it can promote new posts that it has no data for in the context it is optimizing. YouTube Watch Next could use number of watches, or co-watches
(counts of how many times one video was watched after another was watched) from YouTube search.

### Rule 19-Use very specific feature when you can.

### Rule 20-Combine and modify existing features to create new features in human understandable ways.

### Rule 21-The number of feature weights you can learn in a linear model is roughly proportional to the amount of data you have
+ There are fascinating statistical learning theory results concerning the appropriate level of complexity for a model, but this rule is basically all you need to know.

### Rule 22-Clean up features you are no longer using
+ Keep coverage in mind when considering what features to add or keep. How many examples are covered by the feature? For example, if you have some personalization features, but only 8% of your users have any personalization features, it is not going to be very effective.
+ At the same time, some features may punch above their weight. For example, if you have a feature which covers only 1% of the data, but 90% of the examples that have the feature are positive, then it will be a great feature to add.











