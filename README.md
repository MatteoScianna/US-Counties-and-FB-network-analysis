# US-Counties-and-FB-network-analysis

The goal of this work is to perform some kind of network analysis and visual representation of two main networks. 
## US-Counties Network
This network, called g_counties, is created taking all US Counties as nodes. An edge between two nodes exists if the two counties share a common border.
Furthermore, the network g_states is created by merging together counties belonging to the same state. In this case, nodes are represented by states and edges between states are weighted according to the neighboring counties belonging to the two states. Some analysis and visualizations are performed.
### Centrality measures
For each node of the two networks, Degree, Closeness, Eigenvectors and Betweeness centrality are calculated. Furthermore, the function get_choropleth_centrality plots a Choropleth of the chosen network colored according to the level of the chosen centrality measure. Fig 1 shows Choropleth maps for both networks according to Betweeness Centrality. 

<img src="https://github.com/MatteoScianna/US-Counties-and-FB-network-analysis/blob/main/img/choropleth_betweeness_counties.jpg" width="180" height="100">

<img src="https://github.com/MatteoScianna/US-Counties-and-FB-network-analysis/blob/main/img/choropleth_betweeness_state.jpg" width="180" height="100">


### Communities
Using Louvain method, with the function get_choropleth community a community detection analysis is performed and choropleths highlighting community belonging are plotted, as shown below. 

<img src="https://github.com/MatteoScianna/US-Counties-and-FB-network-analysis/blob/main/img/communities_counties.jpg" width="180" height="100">

<img src="https://github.com/MatteoScianna/US-Counties-and-FB-network-analysis/blob/main/img/communities_states.jpg" width="180" height="100">

### Other indices
Finally, for both network some indices are calculated, related to small-worldness, degree distribution, assortativity and eccentricity. 

## Facebook Network 

Also in this network nodes are represented as US Counties. The weights of an edge connecting two nodes, in this case, depends on the SCI (social connectedness index) between the two counties. A discussion of this index is available here https://dataforgood.facebook.com/dfg/tools/social-connectedness-index. 
For this network analysis is performed at two levels:
### County level
The function choropleth_fips returns, for a given county, a choropleth where the color varies according to the SCI index related to the edge connecting the chosen and all other counties. Below, an example.

<img src="https://github.com/MatteoScianna/US-Counties-and-FB-network-analysis/blob/main/img/sci_variation.jpg" width="420" height="300">

Since the network is fully connected, in order to perform some analysis without obtaining pointless results, a reduced version of the network is proposed, by cutting those edges which SCI index is below 400, this network we'll be referred to as g_counties_reduced. 
For the resulting network, indices similar to the ones calculated for the US counties network are calculated. Below, the choropleth of communities detected with the Louvain method. 

### State level 

As before, an alternative version of the network is proposed by merging together nodes belonging to the same state. In order to adjust edges weight, three possible options are proposed.
Be $I = {i_{1},...,i_{n}}$ and $J = {j_{1},..,j_{m}}$ the sets of all counties belonging to states $I$ and $J$, respectively. 
Be ${1}_{\{i_{l},j_{k}\}}$ the indicator function, equal to $1$ iff exists a path connecting counties $i_{l}$ and $j_{k}$, and be $sci(i_{l},j_{k})$ the social connectivness index corresponding to the edge. 

- "weight"  of the edge connecting $I$ and $J$ is defined as $w_{1_{(I,J)}} = \sum \limits_{l,k} {1}_{\{i_{l},j_{k}\}}$

- "weight_sci"  of the edge connecting $I$ and $J$ is defined as $w_{2_{(I,J)}} = \sum \limits_{l,k} sci(i_{l},j_{k}) \cdot {1}_{\{i_{l},j_{k}\}}$

- As for "weight_spacial", given $|I-J|$ a distance measure $^1$ between states $I$ and $J$ and $\alpha_{1}, \alpha_{2} \in [0,1]$ s.t. $\alpha_{1}+\alpha_{2} =1$, we can define

$w_{3_{(I,J)}} = \alpha_{1} \cdot w_{2_{(I,J)}}+\alpha_{2} \cdot |I-J|$ the weight given to every edge $^{2,3}$.

$^1$ Here it has been chosen to use a spatial geodesic distance between states, but of course it is possible to use other concepts of distances, such as the number of steps necessary to go from one state to the other inside the network.
$^2$ As a consequence of the decision of using a spacial distance between ststes, in this case $log(|I-J|)$ is applied.
$^3$ Note finally that the same procedure can be applied if $I=J$, such for counties having a common edge but belonging to the same state. The only difference in this case will be that obviously $w_{i_{(I,I)}}$ will be a node attribute. 



For the resulting graph, a choropleth is plotted according a chosen centrality measure (as done before). Together with the choropleth, nodes and edges are plotted, which are weighted according to the chosen weight. 
The image below shows the resulting plot for Closeness Centrality and weight_sci. 
Note that while for the choropleth the network g_states_reduced has been considered, for the nodes and edges the whole network is been used. 

<img src="https://github.com/MatteoScianna/US-Counties-and-FB-network-analysis/blob/main/img/choropleth%2Bnetwork.jpg" width="420" height="300">
