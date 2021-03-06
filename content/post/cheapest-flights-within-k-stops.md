---
title: "Cheapest Flights Within K Stops"
description: "Some description ..."
authors: ["lek-tin"]
tags: ["leetcode", "graph", "dijkstra"]
categories: ["algorithm"]
date: 2020-06-14T01:30:31-07:00
lastmod: 2020-06-14T01:30:31-07:00
draft: false
archive: false
---

There are n cities connected by `m` flights. Each flight starts from city `u` and arrives at `v` with a price `w`.  

Now given all the cities and flights, together with starting city `src` and the destination `dst`, your task is to find the cheapest price from src to `dst` with up to `k` stops. If there is no such route, output `-1`.  

### Example 1:

```
Input: 
n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
src = 0, dst = 2, k = 1
Output: 200
```
**Explanation**: 
The graph looks like this:
![cheapest flights within k stops example 1](/img/post/cheapest-flights-within-k-stops-example-1.png)
The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.

### Example 2:

```
Input:
n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
src = 0, dst = 2, k = 0
Output: 500
Explanation:
```
The graph looks like this:
![cheapest flights within k stops example 2](/img/post/cheapest-flights-within-k-stops-example-2.png)
The cheapest price from city 0 to city 2 with at most 0 stop costs 500, as marked blue in the picture.

#### Constraints:

1. The number of nodes n will be in range `[1, 100]`, with nodes labeled from `0` to `n - 1`.
2. The size of flights will be in range `[0, n * (n - 1) / 2]`.
3. The format of each flight will be `(src, dst, price)`.
4. The price of each flight will be in the range `[1, 10000]`.
5. `k` is in the range of `[0, n - 1]`.
6. There will not be any duplicated flights or self cycles.

### Solution

Java
```java
class Solution {

    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int K) {

        // Build the adjacency matrix
        int adjMatrix[][] = new int[n][n];
        for (int[] flight: flights) {
            adjMatrix[flight[0]][flight[1]] = flight[2];
        }

        // Shortest prices array
        int[] prices = new int[n];

        // Shortest steps array
        int[] currentStops = new int[n];
        Arrays.fill(prices, Integer.MAX_VALUE);
        Arrays.fill(currentStops, Integer.MAX_VALUE);
        prices[src] = 0;
        currentStops[src] = 0;

        // The priority queue would contain (node, cost, stops)
        PriorityQueue<int[]> minHeap = new PriorityQueue<int[]>((a, b) -> a[1] - b[1]);
        minHeap.offer(new int[]{src, 0, 0});

         while (!minHeap.isEmpty()) {

            int[] info = minHeap.poll();
            int node = info[0], stops = info[2], cost = info[1];

             // If destination is reached, return the cost to get here
            if (node == dst) {
                return cost;
            }

            // If there are no more steps left, continue
            if (stops == K + 1) {
                continue;
            }

            // Examine and relax all neighboring edges if possible
            for (int nei = 0; nei < n; nei++) {
                if (adjMatrix[node][nei] > 0) {
                    int dU = cost, dV = prices[nei], wUV = adjMatrix[node][nei];

                    // Better cost?
                    if (dU + wUV < dV) {
                        minHeap.offer(new int[]{nei, dU + wUV, stops + 1});
                        prices[nei] = dU + wUV;
                    }
                    else if (stops < currentStops[nei]) {
                        // Better steps?
                        minHeap.offer(new int[]{nei, dU + wUV, stops + 1});
                        currentStops[nei] = stops;
                    }
                }
            }
         }

        return prices[dst] != Integer.MAX_VALUE? prices[dst] : -1;
    }
}
```
