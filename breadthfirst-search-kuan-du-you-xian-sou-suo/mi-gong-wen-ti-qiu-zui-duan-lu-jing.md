# 迷宫问题求最短路径



题从目是要求一步步走，每步可以四个方向走​



```java
class Solution {
     class Node{
        int x;
        int y;
        int step;
        
        public Node(int x, int y, int step){
            super();
            this.x = x;
            this.y = y;
            this.step = step;
        }
    }
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        int m = maze.length;
        int n = maze[0].length;
        
        Queue<Node> queue = new LinkedList<>();
        boolean[][] visited = new boolean[m][n];
        Node startNode = new Node(start[0], start[1], 0);
        queue.offer(startNode);
        
        int[][] dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};            
        while(!queue.isEmpty()){
      
            Node node = queue.poll();
            visited[node.x][node.y] = true;
            if(destination[0] == node.x && destination[1] == node.y){    
                System.out.println(node.step);
                return true;
            }
            
            for(int[] dir : dirs){
                int newX = dir[0] + node.x;
                int newY = dir[1] + node.y;

               Node newNode = new Node(newX, newY, node.step + 1); 
               if(newX >= 0 && newY >= 0 && newX < m && newY < n && !visited[newNode.x][newNode.y] && maze[newX][newY] == 0){
                   queue.offer(newNode); 
               }
               
                    
            }
        }
        
        return false;
    }
}
```
