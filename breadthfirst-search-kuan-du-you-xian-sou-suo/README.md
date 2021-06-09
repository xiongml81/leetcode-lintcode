# Breadth-First Search 宽度优先搜索

### 1. The Data Structure of Queue

Queue is an abstract data structure that applies the rule of First-in-First-Out for its elements. Mostly used in BFS implementations of a queue:

* Array: good random access
* List: good performance for insertion and deletion. A deque is somewhat recursively defined: internally it maintains a double-ended queue of chunks of fixed size. Each chunk is a vector, and the queue \("map" in the graphic below\) of chunks itself is also a vector.

### Question: Implement Queue

Implement a Queue. Support the following basic methods:

* enqueue\(item\). Put a new item in the queue
* dequeue\(\). Move the first item out of the queue, return it

Example 1:

```text
Input:
enqueue(1)
enqueue(2)
enqueue(3)
dequeue() // return 1
enqueue(4)
dequeue() // return 2
```

Example 2:

```text
Input:
enqueue(10)
dequeue() //return 10
```

### By Array:

```java
package bfs;

public class Queue {
	//by array
	private static int front, rear, capacity;
	private static Object queue[];
	
	
	public Queue(int c) {
		this.capacity = c;
		front = rear = 0;
		queue = new Object[capacity];
	}
	
	public static void enqueue(int data) {
		if(capacity == rear) {
			//is full
			return;
		}
		else {
			queue[rear] = data;
			rear++;
		}
		return;
	}
	
	public static Object dequeue() {
		if(front == rear) {
			//empty
			return null;
		}
		else {
			Object obj = queue[0];
			for(int i = 0; i < rear - 1; i++) {
				queue[i] = queue[i+1];
			}
			// store 0 at rear indicating there's no element 
            if (rear < capacity) 
                queue[rear] = 0; 
  
            // decrement rear 
            rear--; 
			return obj;
		}
	}
	
	 


	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Queue q = new Queue(10);
		q.enqueue(1);
		q.enqueue(2);
		q.enqueue(3);
		Object obj = q.dequeue();
		q.enqueue(4);
		Object obj2 = q.dequeue();
		System.out.print(obj2);

	}

}

```

### By LinkedList

```java

public class MyQueue {

	private Node front;
	private Node rear;
	
	public MyQueue() {
		// TODO Auto-generated constructor stub
		front = rear = null;
		
	}
	
	public void enqueue(int key) {
		Node temp = new Node(key);
		
		 // If queue is empty, then new node is front and rear both
		if(this.rear == null) {
			this.front = this.rear = temp;
			return;
		}
		
		this.rear.next = temp;
		this.rear = temp;
		
	}
	
	public Node dequeue() {
		// empty
		if(this.front == null) {
			return null;
		}
		
		Node temp = this.front;
		this.front = this.front.next;
		
		 // If front becomes NULL, then change rear also as NULL 
        if (this.front == null) 
            this.rear = null; 
        
        return temp;
	}
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		MyQueue q = new MyQueue(); 
        q.enqueue(10); 
        q.enqueue(20); 
        Node n = q.dequeue(); 
        Node n2 = q.dequeue(); 
        q.enqueue(30); 
        q.enqueue(40); 
        q.enqueue(50); 
        Node n3 = q.dequeue(); 
        System.out.println("Queue Front : " + q.front.key); 
        System.out.println("Queue Rear : " + q.rear.key); 
	}

}

class Node{
	int key;
	Node next;
	
	public Node(int key) {
		this.key = key;
		this.next = null;
	}
}
```

### By Circular Array

[https://leetcode-cn.com/problems/design-circular-queue/](https://leetcode-cn.com/problems/design-circular-queue/)  
  


```java
class MyCircularQueue {
    private int front;
    private int rear;
    private int capacity;
    private int[] arr;

    public MyCircularQueue(int k) {
        capacity = k + 1;
        arr = new int[capacity];
        front = 0;
        rear = 0;
    }
    
    public boolean enQueue(int value) {
        if(isFull()) return false;

        arr[rear] = value;
        rear = (rear + 1) % capacity;
        return true;
    }
    
    public boolean deQueue() {
        if(isEmpty()) return false;

        front = (front + 1) % capacity;
        return true;
    }
    
    public int Front() {
        if(isEmpty()) return -1;
        return arr[front];
    }
    
    public int Rear() {
        if(isEmpty()) return -1;
        return arr[(rear - 1 + capacity) % capacity];
    }
    
    public boolean isEmpty() {
         return front == rear;
    }
    
    public boolean isFull() {
         return (rear + 1) % capacity == front;
    }
}

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue obj = new MyCircularQueue(k);
 * boolean param_1 = obj.enQueue(value);
 * boolean param_2 = obj.deQueue();
 * int param_3 = obj.Front();
 * int param_4 = obj.Rear();
 * boolean param_5 = obj.isEmpty();
 * boolean param_6 = obj.isFull();
 */
```

\*\*\*\*

### Graph Fundamentals

Graph as an offline data structure is often represented by &lt;E,V&gt;, where E is edge, and V is verte. Thus, graph is a set of verteces and edges.  
Direct Graph vs. Undireted Graph

![](../.gitbook/assets/image%20%281%29.png)

Most of the time, BFS is performed on a graph, it applies to both directed and undirected graph.  
Tree is a special graph, making things simpler ,where one node would only have up to one parent, and there is no circles in the tree. Topological sorting could only apply to directed graph

### Graph Representation

![](../.gitbook/assets/image%20%282%29.png)

**Directed Graph**

```java
class DirectedGraphNode {
    int label;
    List<DirectedGraphNode> neighbors;
    DirectedGraphNode(int x) {
        label = x;
        neighbors = new ArrayList<>();
    }
}

Another way: (Can used HashSet intead of Array)
Map<Node, Node[]> graph = new HashMap<Node, Node[]>();
```



### Breadth First Search \(BFS\)

Most asked type of questions

**When to use BFS?**

* **Connected Components 连通性问题**
  * Find all connected points of one point in a graph
  * Iterative way of finding all solutions
  * Could be done by both DFS and BFS - they have same time complexity. The biggest issue about DFS is stack over flow, and thus BFS is preferred
* **Level-Order Traversal**
  * Traversal by level for a graph, tree or matrix
  * Simple Graph Shortest Path \(Simple Directed/Undirected Graph: all edges are of equal length\)
* **Topological Sorting**
  * Topological Sort must be on directed graph, undirected graph does not apply
  * Topological Order does not neccessarily exists, neither is it unique   
  * Get any one topological order
  * Check if unique topological order exists
  * Could be done by both DFS and BFS, BFS is preferred, because DFS is much much hard/more complicated to implement than BFS

#### Shortest Path Problem

* Simple Graph: BFS
* Complex Graph: Floyd, Dijkstra, Bellman-ford, SPFA

#### Longest Path Problem

* If Graph could be levelized: Dynamic Programming
* If Graph could not be levelized: DFS
* Definition of Gragh being levelized: take a directional path with no loops, the points at level i could only go to level i+1, but cannot go back to level i-1; equivaiently, it means there's no circular dependency in the graph. We could use topological sorting to check if there is circular dependency in a graph

#### BFS on Binary Tree vs. On Graph

* Binary Tree is a directed graph \(parent-&gt;children\)
* Graph could be directed/undirected \(just siblings\)
* Binary Tree does not need to used hashSet to check if a node has been visited
* Graph might have circled nodes, and the same node could get into the queue multiple times, need to use HashSet to check if a node has been visited

#### BFS vs DFS

BFS consume memory, DFS stack overflow

#### BFS Implementation - For Tree

```java
 queue.offer(root);

        while(!queue.isEmpty()) {
            ....
            // traverse all nodes in current level
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                ..
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
        }
```

#### [https://leetcode.com/problems/binary-tree-level-order-traversal/](https://leetcode.com/problems/binary-tree-level-order-traversal/)

#### [https://leetcode.com/problems/binary-tree-level-order-traversal-ii/](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

#### [https://leetcode.com/problems/average-of-levels-in-binary-tree/](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/)

#### BFS Implementation - For Graph

```java
Queue<T> queue = new LinkedList<>();
Set<T> set = new HashSet<>();

set.add(start);
queue.offer(start);
while (!queue.isEmpty()) {
    T head = queue.poll();
    for (T neighbor : head.neighbors) {
        if (!set.contains(neighbor)) {
            set.add(neighbor);
            queue.offer(neighbor);
        }
    }
}
```

[https://leetcode.com/problems/clone-graph/](https://leetcode.com/problems/clone-graph/)

  








