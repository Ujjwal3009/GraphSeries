# Topological sorting using BFS

About topological sort is in the previous code

Now we're going to find out the topo sort order using Kahn's algorithm, steps are:
* Create an array which will store the indegree of all the nodes and an array which will store the topo sort i.e the answer
* Store the indegree of all the nodes in that array 
* create a queue, and store the element which has indegree 0 in the queue
* Run your loop until queue will become empty
* pop top element from the queue
* add it in topo sort array
* Go to all the adjacent elements of that node
* and decrease their indegree by 1
* if anyone becomes 0 then push it in a queue
* continue the process intil queue will become empty
* return topo array
* note: topo sort will always start from someone whose indegree is 0
* Now why we are decreasing the indegree by 1 , because when we took that element out and put it into our topo sort then let us assume that it is removed from the
 figure now from whoever it is connected will have degree one lesser because it's depeendency got decreased byy removing this node
* This is kahn's algorithm



![Screenshot from 2021-08-29 22-02-02](https://user-images.githubusercontent.com/42698268/131258131-887dc8ab-980a-42fe-9f14-95d987e76520.png)


## Time complexity and space complexity
* Time complexity would be ```O(N+E)``` same as BFS
* space complexity would be ```O(N+E) + O(N) + O(N)``` for adjacency list, indegree array and queue ds


```java
class Solution {
    static void findTopoSort(int node, int vis[], ArrayList<ArrayList<Integer>> adj, Stack<Integer> st) {
        vis[node] = 1; 
        for(Integer it: adj.get(node)) {
            if(vis[it] == 0) {
                findTopoSort(it, vis, adj, st); 
            } 
        }
        st.push(node); 
    }
    static int[] topoSort(int N, ArrayList<ArrayList<Integer>> adj) {
        Stack<Integer> st = new Stack<Integer>(); 
        int vis[] = new int[N]; 
        
        for(int i = 0;i<N;i++) {
            if(vis[i] == 0) {
                findTopoSort(i, vis, adj, st);
            }
        }
        
        int topo[] = new int[N];
        int ind = 0; 
        while(!st.isEmpty()) {
            topo[ind++] = st.pop();
        }
        // for(int i = 0;i<N;i++) System.out.println(topo[i] + " "); 
        return topo; 
    }
}
```
