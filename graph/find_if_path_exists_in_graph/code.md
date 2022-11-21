### Code №1 (Breadth first search, BFS)

    class Solution {
      public boolean validPath(int n, int[][] edges, int start, int end) {
        
        LinkedList<Integer> adj[]=new LinkedList[n];
        createAdjList(n,adj,edges);                       // создаём граф на LinkedList
        boolean flag=false;
        boolean visited[]=new boolean[n];                 // для того, чтобы избежать повторного посещения узлов
        
        Queue<Integer> q=new LinkedList<>();              // очередь узлов графа для посещения
        
        q.add(start);
        visited[start]=true;
        while(q.size()!=0){                               // пока ещё есть узлы для просмотра в очереди
           
            start=q.poll();
            if(start==end)                                 // каждый раз переопределяем start и когда искомыйэлемент совпадёт со start выдаём ответ true (если не переопределим, то по-умолчанию, false)
                {
                    flag=true;
                    break;
                }
            Iterator<Integer> it=adj[start].listIterator(); // получаем итератор и итерируемся по LinkedList для добавления узлов в очередь
            while(it.hasNext()){
                int val=it.next();
                if(!visited[val])
                {
                    visited[val]=true;
                    q.add(val);
                }
            }
        }
        return flag;                                          // возврат ответа
      }

      private void createAdjList(int n,LinkedList<Integer> adj[],int[][] edges ){
        for(int i=0;i<n;i++){
            adj[i]=new LinkedList<>();
        }
        for(int i=0;i<edges.length;i++){
            adj[edges[i][0]].add(edges[i][1]);
             adj[edges[i][1]].add(edges[i][0]);
        }
      }
    }

### Code №2 (Deep first search, DFS)

    class Solution {
    
      ArrayList<ArrayList<Integer>> al;
      boolean[] visited;
      boolean startFound = false;
      boolean endFound = false;
	
      public boolean validPath(int n, int[][] edges, int start, int end) {
        
        visited = new boolean[n];                               // для того, чтобы избежать повторного посещения узлов
        al = new ArrayList<>();
        for(int i=0;i<n;i++) al.add(new ArrayList<>());
        
                                                                // создаём граф на ArrayList
        for(int i=0;i<edges.length;i++){
            al.get(edges[i][0]).add(edges[i][1]);
            al.get(edges[i][1]).add(edges[i][0]);
        }
        
        for(int i=0;i<n;i++){
            if(!visited[i]){                                     // для всех непосещённых ранее узлов графа
                dfs(i,start,end);                                // рекурсивно ищем start и end относительно каждой вершины
                if(startFound && endFound) return true;          // ответ true
                else {
                    startFound = false;
                    endFound = false;
                }
            }
        }
        
        return false;                                            // ответ false (если ранее не ответили true)
    }
    
    public void dfs(int vertex,int start,int end){
        visited[vertex] = true;
        
        if(vertex == start) startFound = true;
        if(vertex == end) endFound = true;
        
        for(int ll : al.get(vertex))
            if(!visited[ll]) 
                dfs(ll,start,end);
        
    }
}
