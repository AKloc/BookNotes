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
		- Ex: I have a blog and want to detect groups of similar visitors. **I don't know which groups the visitors belong to**, it has to find the connections itself. It finds that 40% of visitors are males, read the book at the same time, etc.
		- Most important algorithms covered later:
			- Clustering (K-Means, DBSCAN, Hierarchical Cluster Analysis)
			- Anomaly detection and novelty detection (One-class SVM, Isolation Forest)
			- Visualization and Dimensionality Reduction (Principal Component Analysis, Kernel PCA, Locally Linear Embedding, t-Distributed Stochastic NEighbor Embedding)
			- Association Rule Learning (Apriori, Eclat)
	- Visualization
		- Also unsupervised
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjMyMTU0MDE1LC0xOTM0OTUyMTI5LC01Nz
Q5OTQ4NTYsMTk3ODc1NTYxMSwyMTAyODY2Nzc3LDMwODY0Mjgz
M119
-->