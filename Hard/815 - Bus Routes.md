# 815. Bus Routes

Difficulty: **Hard**

Link to Problem Statement: [https://leetcode.com/problems/bus-routes/description/](https://leetcode.com/problems/bus-routes/description/)

### My Solution

```python
from math import inf

class Solution:
    def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
        if source==target:
            return 0
        
        busesFromSource, busesToTarget=[], [] 
        for i in range(len(routes)):
            routes[i]=set(routes[i])
            if source in routes[i] and target in routes[i]:
                return 1
            elif source in routes[i]:
                busesFromSource.append(i)
            elif target in routes[i]:
                busesToTarget.append(i)
        
        # Vertices are buses, an edge between 2 buses represent 1 or more common bus stops.
        adjList={i:[] for i in range(len(routes))}
        for i in range(len(routes)-1):
            for j in range(i+1, len(routes)):
                if len(routes[i]&routes[j])>0:
                    adjList[i].append(j)
                    adjList[j].append(i)
        
        # Each edge has a distance of 1. We use shortest path between 2 vertices with BFS to find the minimum number of buses to reach destination.
        leastNumBuses=inf
        for sourceBus in busesFromSource:
            numBuses={bus:inf for bus in adjList}
            numBuses[sourceBus]=1
            queue=[sourceBus]
            while len(queue)>0:
                curr=queue.pop(0)
                for bus in adjList[curr]:
                    if numBuses[bus]>numBuses[curr]+1:
                        numBuses[bus]=numBuses[curr]+1
                        queue.append(bus)
            for targetBus in busesToTarget:
                if leastNumBuses>numBuses[targetBus]:
                    leastNumBuses=numBuses[targetBus]

        return leastNumBuses if leastNumBuses!=inf else -1
```
Runtime: *1406 ms*

Link to my Solution: [https://leetcode.com/problems/bus-routes/solutions/2535089/python-memory-usage-289-mb-less-than-9994/](https://leetcode.com/problems/bus-routes/solutions/2535089/python-memory-usage-289-mb-less-than-9994/)
