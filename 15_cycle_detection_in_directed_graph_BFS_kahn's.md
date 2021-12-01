# Detect cycle in directed graph using BFS

We will use the idea of the topological sort, we know that the topological sort can only be generated in the graph which is DAG, so if we are unable to generate topological sort using kahn's algo then we can say that the graph is cyclic, we are just using the reverse algorithm

```java

class Solution {
    // Function to detect cycle in a directed graph.
    public boolean isCyclic(int V, ArrayList<ArrayList<Integer>> adj) {
        // code 
        
        int[] indegree = new int[V];
        for(int i = 0; i< V ; i++) {
            for(Integer it : adj.get(i)) indegree[it]++;
        }
        
        Queue<Integer> q = new LinkedList();
        for(int i = 0; i< V; i++) if(indegree[i] == 0) q.add(i);
        
        int cnt = 0;
        while(!q.isEmpty()){
            Integer node = q.poll();
            cnt++;
             for(Integer it: adj.get(node)){
                 indegree[it]--;
                 if(indegree[it] == 0 )  q.add(it);
                 
             }
            
            
            
        }
        if(cnt == V) return false;
        return true;
        
        
        
        
        
        
        
        
    }
}
```
