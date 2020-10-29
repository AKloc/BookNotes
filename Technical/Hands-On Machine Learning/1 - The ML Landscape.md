## Chapter 1 - The ML Landscape

**Key Chapter Takeaways**
- Most important parts of the chapter?

**Notes + Metacognition**
- ML is great for problems whose solutions are complex or nuanced. Example given - how do you identify when a word begins with a "t"? What about in noise? Etc. 
- More examples:
	- Finding tumors
	- Classifying news articles
	- Flagging offensive comments
	- Summarizing long docs
	- Detecting credit card fraud
	- Video game bots (use "Reinforced Learning", covered in chapter 18)
- Types of ML:
	- **Supervised** 
		- The dataset that you feed the algorithm includes the desired solutions (called "labels")
		- Ex: Spam filter. You'd provide the emails, along with their "class" - whether or not they're spam.
		- Ex: "Predictors", which predict a target value, like the price of a car, given certain datapoints (called "features"). You'd provide many examples of cars, with their predictors and their labels (in this case, the label is the price of the car).
		- Most important supervised algorithms that will be covered:
			- k-nearest neighbors
			- linear regression
			- logistic regression
			- support vector machines (SVMs)
			- decision trees and random forests
			- neural networks
	- **Unsupervised**
		- Training data is unlabeled. The system tries to learn without a teacher.
		- Ex: I have a blog and want to detect groups of similar visitors. **I don't know which groups the visitors belong to**, it has to find the connections itself. It finds that 40% of visitors are males, read the book at the same time, etc.
		- Most important algorithms covered later:
			- Clustering (K-Means, DBSCAN, Hierarchical Cluster Analysis)
			- Anomaly detection and novelty detection (One-class SVM, Isolation Forest)
			- Visualization and Dimensionality Reduction (Principal Component Analysis, Kernel PCA, Locally Linear Embedding, t-Distributed Stochastic Neighbor Embedding)
			- Association Rule Learning (Apriori, Eclat)
	- Visualization
		- Also unsupervised.
		- The models output a 2D or 3D representation of the data to make it easier to understand at a glance.
	- Visualization often uses "dimensionality reduction," which tries to simplify data without losing too much information.
	- "Feature extraction": Ties correlating features together to simplify the model. e.g., a car's mileage and age. There are "Dimensionality reduction algorithms" that can do this, leading to faster and simpler models that take up less disk space.
	- "Anomaly Detection": If you know what "normal" looks like, you can look for things that aren't. e.g., credit card fraud, manufacturing defects, or removing outliers from a dataset.
	- "Novelty Detection": Similar to anomaly detection, goal is to identify new data points that are different from the rest of the dataset. Requires very clean "backing" data to compare against.
	- "Association rule learning": Uncovers relations between attributes. e.g.: I run an association rule against my grocery sales data and find that people who by bbq sauce and potato chips are also likely buying steak, so I put those items next to each other.
- "Instance": Basically a single datapoint in the model. If I'm modeling something like how likely a user is to enroll in a particular medical coverage given a large dataset of previous enrollments, then an "instance" would be a single user enrollment.
- Semisupervised Learning: 
	- Labeling data takes a lot of time, often will have a mix of labeled and unlabeled instances. Semisupervised help classify unlabeled instances. e.g.: If I upload a photo into Google Photos, it can recognize the faces in my photos by itself, and if it doesn't recognize someone, it lets me name that person.
- Reinforcement Learning:
	- Uses an "agent," which can observe the environment and select and perform actions which may yield a reward or penalty based on what it does. Based on this learning, it determines a strategy, or "policy", that maximizes the reward over time. e.g.: Video game bots. Chess bots.
- Batch and online learning
	- Batch learning: The system doesn't learn as it goes. It's trained with all available data at once.
		- Generally takes a lot of time, so is done offline. When the model is finished, it's put into production. From there, it isn't learning anything, just executing the model. AKA "Offline learning."
		- Typically you retrain the model and replace the old ones. This can be automated so that the batch system is still generally responsive, just at certain increments of time rather than on a smooth / constant basis. Things that tie into the strategy is how often new data rolls in, how much time it takes to train the new model, etc.
			- This approach is probably fine for something like predicting enrollments.
	- Online learning
		- Train incrementally instead of in batches.
		- Feed the model data instances sequentially, individually, in small groups ("mini-batches"), whatever works best. System learns as it goes.
		- Preferred method for anything with a continuous flow (e.g., stock prices).
		- Also a good option if computing resources are limited since you don't need the same sort of burst processing power as you would with batch learning.
		- Same with space. You don't need to horde huge amounts of instances to feed the model if you process it as it comes in.
		- "Out-of-core learning": Basically a hack where you have the system learn on a chunk of data, then move to the next chunk, to avoid overloading the system's main memory. Sort of like memory paging with RAM.
		- "Learning rate": How fast should the system process new data? If it's high, the system rapidly responds, but is quick to forget old data. If it's low, the system learns more slowly, but will be less sensitive to "noise" in the new data. Seems like a "how reactive do you want this to be?" setting. Don't set it too high for instances where weird data might roll in and throw off the whole model.
		- Important when using online learning to monitor the input data and make sure it isn't "off," since it's going to be affecting the model directly.
- Instance-based vs. Model-based learning
	- Distinction is about how ML systems "generalize" / make predictions.
	- Instance-based learning:
		- System learns examples and memorizes them, then compares new instances to the one it's memorized and applies a "measure of similarity" between known and new instances. 
		- e.g.: An email spam filter that might do something like count the number of words in "good" emails and compare them against new emails to try to determine if they're spam.
	- Model-based learning:
		- System generalizes from a set of examples to build a model and then uses the model to make predictions.
		- e.g.: "Life Satisfaction" to "GDP per Capita" graph that shows that there's a trend with life satisfaction and GDP - almost a straight line. 
			- Because the shape of the graph is a line, we would use a "model selection" of a "linear model". (This might sound wordy because I'm trying to capture all of the terms in the book, but it's literally just saying "Your data looks like a line, so predict using that same line.")
			- The linear model has two parameters it takes. Depending on what those two values are set at, they can represent any linear function. In our case: *life_satisfaction =p1 + pw x GDP_per_capita*
			- How do we know which values to use for p1 and p2? We need to specify a "performance measure" that tells us how our model is performing. Two methods:
				- "Fitness Function": tells you how GOOD your model is.
				- "Cost Function": tells you how BAD your model is. Most linear regression uses cost functions that measure the distance between the model's prediction and the training examples. The model optimizes to REDUCE this distance.
			- Going back to our GDP / life satisfaction model, this is where we can use a Linear Regression algorithm. We give it our training data, and IT will find the best parameters that match our data (this is called "training" the model). 
				- (Relatively simple Python code ensues that loads data from a CSV, creates a model, feeds it the data, then predicts the life satisfaction for a country given a GDP).
- Main Challenges of ML
	- Boils down to: Bad model, or bad data.
	- Bad data:
		- Not having enough training data. A Microsoft study showed that as you added more and more data, different algorithms would eventually end up converging on what they predicted. MORE DATA!
		- Nonrepresentative training data. Going back to GDP example - you want to show countries across the entire spectrum if possible, so that the linear equation reflects that. If all of the data was concentrated in one area, it wouldn't do as good of a job predicting instances outside of that area. This is AKA "Sample bias." Another example - sending presidential polls out only to folks in reading clubs, who are going to be wealthier and more likely to vote Republican.
		- Poor-quality data. Obvious one, if your data is full of trash data or noise. Have to be careful with what constitutes "trash," though. Having some outliers to reflect the reality of the superset is important.
		- Irrelevant features. The system can  



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY1NDc5OTQ4NCwtMTYyNzYxNTQ0Niw5MD
c3MDc2MzMsLTE4MDcwMDIyNTMsLTIyOTY0OTI2NSwtMTAxOTQ1
OTc0NiwtMjEzMDIxMDk4NCwtNDQ1MDEzMjA1LC0xMjcxNzE5Nj
kyLC0xMzY2NzY2MDk0LC04OTgwOTI0NDYsLTE5MzQ5NTIxMjks
LTU3NDk5NDg1NiwxOTc4NzU1NjExLDIxMDI4NjY3NzcsMzA4Nj
QyODMzXX0=
-->