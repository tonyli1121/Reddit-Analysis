# Reddit-Analysis
This is a research project from CSCD25 (Advance Data Analysis) to analyze the connection between Reddit users and their roles in constructing connections

# Research Questions

  1. 
  2.
  3.

# Data Story

https://tonyli1121.github.io/Reddit-Analysis/

# Methodologies used in the project
		
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
