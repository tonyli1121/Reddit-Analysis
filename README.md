# Existence of "Six degrees of separation" on Reddit
This is a research project from CSCD25 (Advance Data Analysis) on research question that I came up myself supervised by Professor Anderson and TA Waller.

## Abstract:

The Six degrees of seperation (also known as six handshakes rule) is an idea that all people are six or fewer social connections away from each other. As a result, a chain of "friend of a friend" statement can be made to connect any two people in a maximum of six steps. 

Several studies, such as Milgram's small-world experiment, have been conducted to measure this connectness empirically, and nowadays the phrase "six degrees of separation" is now often used as a synonym for the idea of the "small world" phenomenon.

	Some ground-breaking phenomenons discovered by researchers are 
	1) There are 19 degrees of separation between any two web pages (by Hungarian physicist Albert-László Barabási in 2013). 
	
	2) shortest path from one Wikipedia to another is 3 degrees, while the furthest is just 11 degrees. 
	
	3) Facebook's data team released two papers in November 2011 which document that amongst all Facebook users at the time of research 
	(721 million users with 69 billion friendship links) 
	There is an average distance of 4.74. And by February 2016, the distance is 4.57 on avg on 1.6 billion users (about 22% of the world population)
	
	4) On average, about 50% of people on Twitter are only four steps away from each other.
	...

	It turns out that for social networking websites with large amount of users, the six handshakes rule stays valid. 
	
Reddit, known as one of the most famous social news and discussion website, also has a huge amount of users. According to an analysis on reddit's monthly visitors, as of June 2021, Reddit had almost 48 million monthly active users.	(https://www.statista.com/statistics/443332/reddit-monthly-visitors/) 

	Based on how Reddit works (registered members submit posts to the site such as links, text posts, images, and videos,
	which are then voted up or down and commented by other members). I am particularly interested in the existence of 
	the Six Degrees of Separation on Reddit.

## Research Question:

The goal of this research is to find if given two posts (identified by their post_id/title), if we can get to one from another by tracking user activities in small # of steps.
	
	Specifically,	given 	- posts [A, B]
				- users [user_1, user_2, ...]
				- at least one user in the users list answered A or asked A
			can we find a path with small distance to get to post B?

An example would be as followed:

		user 1 asked "A" 
			/\
		       /  \
	 answered by user2,user3
		     /         \
		    /           \
	  commented user4     user5, user 6
		  /	          \       \
		 /		   \       \
	    asked "C"       	answered "C"   asked "B"
	Then we say there is a path from A -> user3 -> user6 -> B, and has a distance of 3
	
Here are a list of research goals with <1>, <3> being the primary ones:
	
	<1> what is the avg distance of path for this analysis?
	<2> what is the max distance of path for this analysis?
	<3> Given two arbitrary posts, what is the possibility that path exists? 
	<4> Given two arbitrary posts, what is the possibility of the path length <= 6?
	<5> Visualize the data

## Hypothesis:
	
The hypothesis will come after some clustering result.

	If the clusters are obvious but has large invariance 
		then hypothesis is low distance, high chance to find path
	If the clusters are obvious but has low invariance (i.e., every cluster is a group with few connection to other clusters)
		then hypothesis is high distance, low chance to find path (but still need to check)
	If the cluster doesn't show anything special (i.e., large invariance for data in each cluster / hard to specify clusters)
		either redo the clustering or start working on the data analysis steps directly.
		(since we have to check the distance/path anyways)
	
Verify the hypothesis/research goals by
	
	1) avg distance
	2) max distance
	3) possibility to find such a path (i.e., successful rate given any two ids)
		3a) plan to do the searching: through using some tree structure 
		(would need to check online for more reference on how other studies did this)
	4) Visualization on distance (current plan)
		4a) a nxn matrix (n = |posts|), every index is value of distance
		4b) bar chart (x-axis = distance value, y-axis = # of paths)

## References that decided to use:

papers on six handshake rule (to help build the model)

Generalists and Specialists: Using Community Embeddings to Quantify Activity Diversity in Online Platforms by Isaac Waller and Ashton Anderson

	("We found a broad spectrum of user styles, from extreme generalists to extreme specialists, and observed that specialists
	are more likely to produce higher-quality replies")
	
will this supply any of the hypothesis (or is there any connection between the research result and the papers result?)
	

## Steps:
	<0> Clean the dataset
	<1> Unsupervised learning to group (a) posts, (b) users using (a) topics (b) texts analysis
		<1.1> Draw hypothesis 
		(YES if connected, NO if seperated. If hard to determine by unsupervised learning result, jump directly to analysis)
	<2> Build a model that takes parameters [id_1, id_2] and return path length if there exists. (exact method TBD)
	<3> Visualize data using the model.
	<4> Check against conclusion from <1.1>

## Other possible research questions if the six handshake is not acceptable:

	<1> among different posts, what are the top topics users talk about? (USING NLP)
		- Political? 
		- Entertainment? 
		- Daily shares?
		- Technologies? 
	
	<2> when some large event happens (i.e., vaccine comes out), what is the trend of people discussing it on Reddit
		- does it follow a bell curve?
		- or keep increasing but suddenly drops?
		- or suddenly increases but slowly drops?



