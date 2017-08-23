---
layout: post
title: SNA (testerinho)
subtitle: Subtitulos - el testing Uno Dos Tres.
---



## Social Network Analysis (test40385769745 uuuu with html instead)

Testing social network analysis with the "sna" and "igraph" packages for R using the Erdos-Renyi model for constructing the graphs. But first, some simple graphs:

Full graph: Every node/vertex has every possible connection.

```r
library(sna)
library(igraph)
g_full <- make_full_graph(8, directed = FALSE)
plot(g_full)
```

![][workpls]

[workpls]: https://github.com/Ryo-N7/Ryo-N7.github.io/blob/master/img/ISD-1.jpg

Ring graph: Graph is circular, where neighboring nodes are connected to each other to form a ring. 

<img src = "https://assets-cdn.github.com/images/modules/open_graph/github-logo.png" >

![image](../assets/2017-08-21-social-network-analysis_files/unnamed-chunk-1-1.png "blah")

```{r}

g_ring <- make_ring(12, directed = FALSE, mutual = FALSE, circular = TRUE)

plot(g_ring)
```

Star graph: A single central vertex is connected by a singular edge from other vertices.

```{r}

g_star <- make_star(10, center = 1)

plot(g_star)
```

### asdf34957834697359gjlgjl


Without actual data, we can use `sample_gnp` or `sample_gnm` to create network graphs with randomized data.

"In the G(n, M) model, a graph is chosen uniformly at random from the collection of all graphs which have 'n' nodes and 'M' edges. For example, in the G(3, 2) model, each of the three possible graphs on three vertices and two edges are included with probability 1/3.

In the G(n, p) model, a graph is constructed by connecting nodes randomly. Each edge is included in the graph with probability 'p' independent from every other edge." <https://en.wikipedia.org/wiki/Erd%C5%91s%E2%80%93R%C3%A9nyi_model>



```r
g1 <- sample_gnp(30, 0.08, directed = FALSE, loops = FALSE) 

plot(g1)
```

![workworkwork](../assets/2017-08-21-social-network-analysis_files/unnamed-chunk-4-1.png "ellariasand")
Next we can use the function `igraph()` to customize even more attributes of the SNA graph, be careful as things might get ugly! 


```r
plot.igraph(g1, vertex.label = V(g1)$name, vertex.size = 40,
            vertex.label.color = "yellow", vertex.label.font = 2,
            vertex.color = "darkblue", edge.color = "red",
            vertex.frame.color = "green")
```

![](SNA_files/figure-html/unnamed-chunk-5-1.png)

or you can use the `%>%` pipes with the `set_vertex_attr()` or `set_edge_attr()` etc. functions to achieve similar results: 


```r
g2 <- sample_gnp(30, 0.4, directed = FALSE, loops = FALSE) %>% 
  set_vertex_attr("color", value = "red") %>% 
  set_edge_attr("color", value = "black")

plot(g2)
```

![](SNA_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

With actual data such as in `undirected.txt`, just load it in using `read.table()`:


```r
indirectdata <- read.table("undirected.txt")

graph1 <- graph_from_data_frame(indirectdata, directed = FALSE, vertices = NULL)

plot(graph1)
```

![](SNA_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

How about directed graphs? Simply set `directed =` to `TRUE`: 


```r
directdata <- read.table("directed.txt")

graph2 <- graph_from_data_frame(indirectdata, directed = TRUE, vertices = NULL)

plot(graph2)
```

![](SNA_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
