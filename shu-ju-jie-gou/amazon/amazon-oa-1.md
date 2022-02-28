# Amazon OA 1



```java
// Question 1:
// Amazon ships millions of packages every day. A large percentage of them are fulfilled by. Amazon, so it is important to minimize shipping costs. It has been found that moving a group of 3 packages to the shipping facility together is most efficient. The shipping process needs to be optimized at a new warehouse. There are the following types of queries or requests:
// INSERT package id: insert package id in the queue of packages to be shipped
// SHIP-: ship the group of 3 items that were in the queue earliest i.e. they are returned in the order they entered,
// Perform q queries and return a list of lists, one for every SHIP - type query. The lists are
// either; 3 package ID strings in the order they were queued. Or, if there are not enough packages in the queue to fulfill the query, the result is I"N/A"J.
// Note:
// •: Initially, the queue is empty.
// •. The list of packages shipped per group should be in the order they were queued.

// The function performQueries take List<List<>> of type String as a parameter which contains each query where
// list.get(i).get(0) = INSERT | SHIP
// list.get(i).get(1) = shipmentID | -

// Example Test Case:
// 5
// 2
// INSERT GT23513413
// INSERT TQC2451340
// SHIP -
// INSERT VYP8561991
// SHIP

// Expected result:
// [N/A]
// [GT23513413, TQC2451340, VYP8561991]
```

![](<../../.gitbook/assets/Question 1.jpg>)

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World!");
        
    }
    
    public static List<List<String>> performWarehouseQueries(List<List<String>> query){
        List<List<String>> res = new ArrayList<>();
        LinkedList<String> queue = new LinkedList<>();
        
        for(List<String> row :  query){
            String command = row.get(0);
            if(command.equals("INSERT")){
                queue.add(row.get(1));
            }
            else if (command.equals("SHIP")){
                List<String> r = new ArrayList<>();
                if(queue.size() >= 3){
                    r.add(queue.poll())；
                    r.add(queue.poll());
                    r.add(queue.poll());
                }
                else{
                    r.add("N/A");
                }
            }
            res.add(r);
        }
        return res;
    }
}
```

