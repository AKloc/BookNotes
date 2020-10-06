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
	- Supervised 
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
	- Unsupervised
		- Training data is unlabeled. The system tries to learn without a teacher.
		- Most important algorithms covered later:
			- Clustering (K-Means, DBSCAN, Hierarchical Cluster Analysis)
			- Anomaly detection and novelty detection (One-class SVM, Isolation Forest)
			- Visualization and Dimensionality Reduction (Principal Component Analysis, Kernel PCA, Locally Linear Embedding, t-Distributed Stochastic NEighbor Embedding)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMDI1MDM1MDgsLTU3NDk5NDg1NiwxOT
c4NzU1NjExLDIxMDI4NjY3NzcsMzA4NjQyODMzXX0=
-->