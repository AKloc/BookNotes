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



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY5MjIyNjgyMywtMTM2Njc2NjA5NCwtOD
k4MDkyNDQ2LC0xOTM0OTUyMTI5LC01NzQ5OTQ4NTYsMTk3ODc1
NTYxMSwyMTAyODY2Nzc3LDMwODY0MjgzM119
-->