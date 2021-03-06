# Existence of "Six Degrees of Separation" on Reddit - Potential of Quick Information Flow
This is a research project from CSCD25 (Advanced Data Analysis) supervised by Professor Anderson and TA Waller.
https://tonyli1121.github.io/Reddit-Analysis/

## Abstract

The Six degrees of seperation (also known as six handshakes rule) is an idea that all people are six or fewer social connections away from each other. As a result, a chain of "friend of a friend" statement can be made to connect any two people in a maximum of six steps. 

Several studies, such as Milgram's small-world experiment, have been conducted to measure this connectedness empirically, and nowadays the phrase "six degrees of separation" is now often used as a synonym for the idea of the "small world" phenomenon.

    Some ground-breaking phenomenons discovered by researchers are 
	1) There are 19 degrees of separation between any two web pages (by Hungarian physicist Albert-László Barabási in 2013). 
	
	2) shortest path from one Wikipedia to another is 3 degrees, while the furthest is just 11 degrees. 
	
	3) Facebook's data team released two papers in November 2011 which document that amongst all Facebook users at the time of
	research (721 million users with 69 billion friendship links) 
	There is an average distance of 4.74. And by February 2016, the distance is 4.57 on avg on 1.6 billion users 
	(about 22% of the world population)
	
	4) On average, about 50% of people on Twitter are only four steps away from each other.
	...

	It turns out that for social networking websites with large amount of users, the six handshakes rule stays valid. 
	
Reddit, known as one of the most famous social news and discussion website, also has a huge amount of users. According to an analysis on reddit's monthly visitors, as of June 2021, Reddit had almost 48 million monthly active users.	(https://www.statista.com/statistics/443332/reddit-monthly-visitors/) 

Based on how Reddit works

	Registered members submit posts to the site such as links, text posts, images, and videos, which are then 
    voted up or down and commented by other members
	
I am particularly interested in the existence of the Six Degrees of Separation on Reddit and several research questions related to it.

## Research Question:

The goal of this research is to find if given two authors/posts, if there exist a path to get to one from another by tracking user activities in small # of steps.
	
A brief example would be as followed:

            user 1 asked "A" 
		 /\
		/  \
	 answered by user2,user3
	     /         \
	    /           \
	commented by user4   user5, user 6
          /	          \       \
         /		    \       \
	asked "C"       answered "C"   asked "B"

Then we say there is a path from A -> user3 -> user6 -> B, and has a distance of 3
	
Here are a list of research questions with <2>,<3> being the primary ones:
    
1. Is there a "friend of friend" chain (info flow chain) in reddit users (i.e., by commenting)? If so what is the avg distance between users?
    (This question should be similar to the ordinary Six Handshake Problem)
    
2. Is there a "post" chain? For example, can we get from one post to another by tracking user activity as the example above? If so what are the avg distance of the "post" chain?
    (although this question is similar to the above one, it could give a different result as the length of path may differ a lot based on situations)
    
3. Can we predict the distance if the path exist?
    
4. (If have time)Can we form any relation between clusters and length of path?
    (i.e., what is the relationship between posts path length within a subreddit V.S. overall posts path length)

## Hypothesis:
	
1. There is a "Small world"/"Six Handshake Rule" between users
2. There is a "post" chain.
3. It should be hard but worth try
4. Posts will have smaller path length in the subreddits they belong to
	
Verify the hypothesis/research goals by
	
1. Check 
    (a) avg distance for existing path
    (b) max distance for existing path
    (c) possibility for path to exist given any two posts (success/total)

2. Check
   (a) possibility for path to exist given any two posts (success/total)
   (b) avg distance for existing path
   (c) max distance for existing path
    
3. Build a prediction model using the connections between posts (i.e., comment, submission, scores, etc.)

4. Compare the avg distance of each subreddit to the overall avg distance.
    (a) if much smaller then YES (posts have smaller distance to other posts with same topic)
    (b) otherwise NO

		
## Steps:

    1. Load and clean the dataset, take an eye on it for understanding (milestone)
    
    2. create a binary matrix on user connection and analyze with it (currently working on)
        a. construct a graph with the matrix, perform Dijkstra on it to find shortest path for all users
        b. put the values into a matrix, the matrix will be N x N, every entry is the distance
        c. take the upper triangle of the matrix, find avg/max value
        d. visualize the data (i.e., matrix with colour, and a box chart represent the distance values)
        e. draw conclusion with it
	
    3. Similar to 1, create binary matrix on post to user connection
        a. if posts is answered/asked/commented by a user, then the user is connected to that post
        b. then if connect the user to other users/posts (by using answering/asking/commenting)
        c. construct graph, perform Dijkstra
        d. matrix to store value, take upper tri. for avg/max
        e. visualize data
        f. draw conclusion     
	
    4. Build a prediction model using the binary matrix from step 2
        a. train it with accurate data and popularity using accurate data (label)
        b. compare the predicted result again label
        c. conclude whether we can apply the model on larger dataset based on performance
        d. if can, apply on larger dataset for insights in a general perspective
        e. otherwise, conclude that we either need more data to train model or connection/popularity is not a 
        good predictor
	
    5. Perform (3) on every subreddit
        a. perform dijkstra on every subreddit matrix
        b. compare with result of 3
        c. visualize it by using bar chart and a horizontal line representing general avg.
	
## Questions / Problems to think about

1. What is the question you intend to answer?
	
		as listed in RESEARCH QUESTIONS
	
2. What is the analysis strategy you will use in your pursuit of this question? What analyses, modeling steps, and visualization plans do you have? What alternatives did 	you consider but eventually drop in favour of your proposed plan?

		Analysis strategy:
		- See steps for current plan.
		
		Alternative dropped methods:
		- using unsupervised learning on the graph (matrix) for some insights. (like A2 part 1)
		- Abandoned b/c the authors are just linked to those posts, we cannot get a general idea on what 
		  the entire (full) reddit dataset would be grouped by just using the authors.
            
		- use author path length to represent posts path length in step 3.
		- Dropped b/c these are two different tasks, although they have similar meaning and won't differ by 
		  too much, if we have time we still want accurate enough result.
		
3. What dataset(s) will you use?
	
		Full dataset is the best choice. Since it provides a more general understanding on the path distance 
        overall on Reddit.
		Using the full dataset we will be able to create a report similar to Facebook's data team.

		HOWEVER!! It would probably be too large and unnecessary. Hence, the main dataset with only metadata 
        would be more applicable.
        
		Also since the main dataset is random 2% down-sample, we can maintain characteristics while process with
        a easier dataset.

		Will consider using the text dataset in prediction part, but so far only using main dataset.
	
4. How will you manage the size of the dataset(s) you have chosen?
	
		Consider the size of main dataset is still 1GB, I will create a report using all data if possible.
		However, most likely I will just use a random proportion of data to create matrix and bar charts. 
        This would help reduce the amount of data that I pass into my model. And once I confirm that my model 
        is working properly, i will let it run with the entire main dataset

5. How will you filter, transform, and/or enrich the raw data to get it in a form appropriate for your project?

        I will transform the data into a matrix representation like we did in A2 part 1.
		I'm not planning to add too much addition information, the post and users should be enough to 
        connect the graph.
		I will keep the dataset without dropping too much rows, because it will show the generality.
		The plan on processing data may change through the data processing process, it really depends on
        whether I found anything that requires modification.
        
6. It is very likely that our path length will be larger than the optimal length using the entire reddit data, since for the entire dataset, there are more choices for every vertex in the path.

        I am consider to leave this problem.
            Reason 1: we can't run the entire dataset, impossible on home laptop setting
            Reason 2: the prediction model (step 4 of research) may be able to solve this
            Reason 3: The optimal length is smaller than the path length we found, so if our result is 
            small, we can conclude that in Reddit the optimal path length for all data is even smaller.
	
## References that decided to use:

Wikipedia

papers on six handshake rule (to help build the model on Dijkstra)

Generalists and Specialists: Using Community Embeddings to Quantify Activity Diversity in Online Platforms by Isaac Waller and Ashton Anderson

	"We found a broad spectrum of user styles, from extreme generalists to extreme specialists, and observed that specialists are more likely to produce higher-quality replies"
	
will this supply any of the hypothesis (or is there any connection between the research result and the papers result?


