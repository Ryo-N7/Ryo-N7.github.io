---
layout: post
title: Graphics for Social Network Analysis
img: "/assets/2017-04-03-social-network-analysis_files/unnamed-chunk-1-1.png"
---

## A small introduction with the _sna_ and the _igraph_ packages.!

#### This was originally a small introduction to R's capabilities for social network analysis for my fellow group members in a project for the **Talent Management** module of my MSc. program. Therefore it is really barebones, especially since we were only going to use it as a nice demonstration graphic in our PowerPoint presentation... It was also the first time I used **RMarkdown** so I kept this in here for nostalgia's sake. I _may_ do a more detailed intro or a project with this if my interests lean toward social network analysis again in the future...

Testing social network analysis with the _sna_ and the _igraph_ packages for R using the Erdos-Renyi model for constructing the graphs. But first, some simple graphs:

Full graph: Every node/vertex has every possible connection.

```r
library(sna)
library(igraph)
g_full <- make_full_graph(8, directed = FALSE)
plot(g_full)
```
![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-1-1.png)

Ring graph: Graph is circular, where neighboring nodes are connected to each other to form a ring.  

```{r}

g_ring <- make_ring(12, directed = FALSE, mutual = FALSE, circular = TRUE)

plot(g_ring)
```

![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-2-1.png)  

Star graph: A single central vertex is connected by a singular edge from other vertices.

```{r}

g_star <- make_star(10, center = 1)

plot(g_star)
```

![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-3-1.png)  


Without actual data, we can use `sample_gnp` or `sample_gnm` to create network graphs with randomized data.

"In the G(n, M) model, a graph is chosen uniformly at random from the collection of all graphs which have 'n' nodes and 'M' edges. For example, in the G(3, 2) model, each of the three possible graphs on three vertices and two edges are included with probability 1/3.

In the G(n, p) model, a graph is constructed by connecting nodes randomly. Each edge is included in the graph with probability 'p' independent from every other edge." 
More info [here](https://en.wikipedia.org/wiki/Erd%C5%91s%E2%80%93R%C3%A9nyi_model). 



```r
g1 <- sample_gnp(30, 0.08, directed = FALSE, loops = FALSE) 

plot(g1)
```

![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-4-1.png)  
Next we can use the function `igraph()` to customize even more attributes of the SNA graph, be careful as things might get ugly! 


```r
plot.igraph(g1, vertex.label = V(g1)$name, vertex.size = 40,
            vertex.label.color = "yellow", vertex.label.font = 2,
            vertex.color = "darkblue", edge.color = "red",
            vertex.frame.color = "green")
```

![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-5-1.png)

or you can use the `%>%` pipes with the `set_vertex_attr()` or `set_edge_attr()` etc. functions to achieve similar results: 


```r
g2 <- sample_gnp(30, 0.4, directed = FALSE, loops = FALSE) %>% 
  set_vertex_attr("color", value = "red") %>% 
  set_edge_attr("color", value = "black")

plot(g2)
```

![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-6-1.png)<!-- -->

With actual data such as in `undirected.txt`, just load it in using `read.table()`:


```r
indirectdata <- read.table("undirected.txt")

graph1 <- graph_from_data_frame(indirectdata, directed = FALSE, vertices = NULL)

plot(graph1)
```

![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-7-1.png)<!-- -->

How about directed graphs? Simply set `directed =` to `TRUE`: 


```r
directdata <- read.table("directed.txt")

graph2 <- graph_from_data_frame(indirectdata, directed = TRUE, vertices = NULL)

plot(graph2)
```
![](../assets/2017-04-03-social-network-analysis_files/unnamed-chunk-8-1.png)<!-- -->  

