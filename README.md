# US-Counties-and-FB-network-analysis

The goal of this work is to perform some kind of network analysis and visual representation of two main networks. 
## US-Counties Network
This network, called g_counties, is created taking as nodes all US Counties. An edge between two nodes exists if the two counties share a common border.
Furthermore, the network g_states is created by merging together counties belonging to the same state. In this case, nodes are represented by states and edges between states are weighted according to the neighboring counties belonging to the two states. Some analysis and visualizations are performed.
### Centrality measures
For each node of the two networks, Degree, Closeness, Eigenvectors and Betweeness centrality are calculated. Furthermore, the function get_choropleth_centrality plots a Choropleth of the chosen network colored according to the level of the chosen centrality measure. Fig 1 shows Choropleth maps for both networks according to Betweeness Centrality. 

--- insert image ---- 

### Communities
Using Louvain method, with the function get_choropleth community a community detection analysis is performed and choropleths highlighting community belonging are plotted, as shown below. 

--- insert image --- 

### Other indices
Finally, for both network some indices are calculated, related to small-worldness, degree distribution, assortativity and eccentricity. 

## Facebook Network 
