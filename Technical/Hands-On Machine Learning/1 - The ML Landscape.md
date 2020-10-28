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
			- Visualization and Dimensionality Reduction (Principal Component Analysis, Kernel PCA, Locally Linear Embedding, t-Distributed Stochastic Neighbor Embedding)
			- Association Rule Learning (Apriori, Eclat)
	- Visualization
		- Also unsupervised.
		- The models output a 2D or 3D representation of the data to make it easier to understand at a glance.
	- Visualization often uses "dimensionality reduction," which tries to simplify data without losing too much information.
	- "Feature extraction": Ties correlating features together to simplify the model. e.g., a car's mileage and age. There are "Dimensionality reduction algorithms" that can do this, leading to faster and simpler models that take up less disk space.
	- "Anomaly Detection": If you know what "normal" looks like, you can look for things that aren't. e.g., credit card fraud, manufacturing defects, or removing outliers from a dataset.
	- "Novelty Detection": Similar to anomaly detection, goal is to identify new data points that are different from the rest of the dataset. Requires very clean "backing" data to compare against.
	- "Association rule learning"
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NTE5NjYyMzQsLTg5ODA5MjQ0NiwtMT
kzNDk1MjEyOSwtNTc0OTk0ODU2LDE5Nzg3NTU2MTEsMjEwMjg2
Njc3NywzMDg2NDI4MzNdfQ==
-->