# Facebook-Friend-Recommendation-Using-Graph-Mining
### Problem Statement
This project is based on social media link prediction whether two users are going to be friend in future or not.

### Data Overview
Taken data from facebook's recruting challenge on kaggle https://www.kaggle.com/c/FacebookRecruiting  
data contains two columns source and destination eac edge in graph 
    - Data columns (total 2 columns):  
    - source_node         int64  
    - destination_node    int64  
    
 ### Mapping the problem into supervised learning problem:
- Generated training samples of good and bad links from given directed graph and for each link got some features like no of followers, is he followed back, page rank, katz score, adar index, some svd fetures of adj matrix, some weight features etc. and trained ml model based on these features to predict link. 
- Some reference papers and videos :  
    - https://www.cs.cornell.edu/home/kleinber/link-pred.pdf
    - https://www3.nd.edu/~dial/publications/lichtenwalter2010new.pdf
    - https://kaggle2.blob.core.windows.net/forum-message-attachments/2594/supervised_link_prediction.pdf
    - https://www.youtube.com/watch?v=2M77Hgy17cg
    
### Business objectives and constraints:  
- No low-latency requirement.
- Probability of prediction is useful to recommend ighest probability links

### Performance metric for supervised learning:  
- Both precision and recall is important so F1 score is good choice
- Confusion matrix
### Library which you may not have pre-installed
- Networkx
- pip3 install networkx

### Features used-
#### 1) Jaccard Distance - Let say that you have user1 and user2 

*Set X - u1={u5 , u3 , u4} are the followers of u1*

*Set y - u2={u3, u4, u6} are the followers of u2*

*Then Jaccard distance is equal to |X intersection Y| / |X Union Y|*

*The larger the Jaccard index higher is the chance of between these 2 users.*

*Similary we have done for followees also.*

#### 2) Cosine Distance -
If you have two vectors you can find the cosine similarity between them, similar to cosine distance is Otsuka-Ochiai cosine similarity, where coefficient between two set can be written as-

*Cosine Distance = |X intersection Y| / SQRT(|X|.|Y|)*

*This coefficient is large when there is larger intersection.*

#### 3) Page Rank - 
This features is used in ranking of web-pages , for example when you search something on google a series of website appears in a particualar way! Page rank is the key which rank pages according to number of links coming to page, how famous the page is, interchange of links between pages.
You can read more about page rank here-
https://en.wikipedia.org/wiki/PageRank
We use the Page Rank feature for our dataset also, to get the importance of a user, like for example a person is Bill Gates there is a higher possibilty that he will be followed by Mark Zukerberg also but other two different user following Bill Gates is not necessary that they know each other as Bill Gates is famous so many people follows him.

#### 4) Shortest Path - 
Getting Shortest path between two nodes, if nodes have direct path i.e directly connected then we are removing that edge and calculating path, as shorter the path there is higher probabilty of edges between them.

#### 5) Weakly Connected Components - 
We use this feature to form the community.
To understand Weakly Connected Components we must understand Strongly Connected Components which is a di-graph where each sub-graph has a path from each node to every other node, but you can traverse only in the followed direction.
But if we ignore the directions from strongly connected graph it becomes the Weakly connected graph in which you can go from any node to anywhere, which will help us in our case study to form a community who shares something similar like co-workers, college friends.

#### 6) Adar Index - 
Adamic/Adar measures is defined as inverted sum of degrees of common neighbours for given two vertices.

#### 7) Follow Back
#### 8) Katz Centrality -
https://en.wikipedia.org/wiki/Katz_centrality
https://www.geeksforgeeks.org/katz-centrality-centrality-measure/
 Katz centrality computes the centrality for a node based on the centrality of its neighbors. It is a 
  generalization of the eigenvector centrality.
 
#### 9) HITS Score -
https://en.wikipedia.org/wiki/HITS_algorithm
The HITS algorithm computes two numbers for a node. Authorities estimates the node value based on the incoming links. Hubs estimates the node value based on outgoing links.

#### 10) Weight Features -
In order to determine the similarity of nodes, an edge weight value was calculated between nodes. Edge weight decreases as the neighbor count goes up. Intuitively, consider one million people following a celebrity on a social network then chances are most of them never met each other or the celebrity. On the other hand, if a user has 30 contacts in his/her social network, the chances are higher that many of them know each other. 
`credit` - Graph-based Features for Supervised Link Prediction
William Cukierski, Benjamin Hamner, Bo Yang

