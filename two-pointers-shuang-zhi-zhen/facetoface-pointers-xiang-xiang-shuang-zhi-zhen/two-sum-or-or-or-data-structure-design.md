# 170. Two Sum \|\|\| \(Data Structure Design\)

[https://leetcode-cn.com/problems/two-sum-iii-data-structure-design/](https://leetcode-cn.com/problems/two-sum-iii-data-structure-design/)  


Design a data structure that accepts a stream of integers and checks if it has a pair of integers that sum up to a particular value.

Implement the TwoSum class:

TwoSum\(\) Initializes the TwoSum object, with an empty array initially. void add\(int number\) Adds number to the data structure. boolean find\(int value\) Returns true if there exists any pair of numbers whose sum is equal to value, otherwise, it returns false.

 **Example 1:**

```text
Input
["TwoSum", "add", "add", "add", "find", "find"]
[[], [1], [3], [5], [4], [7]]
Output
[null, null, null, null, true, false]

Explanation
TwoSum twoSum = new TwoSum();
twoSum.add(1);   // [] --> [1]
twoSum.add(3);   // [1] --> [1,3]
twoSum.add(5);   // [1,3] --> [1,3,5]
twoSum.find(4);  // 1 + 3 = 4, return true
twoSum.find(7);  // No two integers sum up to 7, return false


```

```java
class TwoSum {
  
    private HashMap<Integer, Integer> map;
    /** Initialize your data structure here. */
    public TwoSum() {
        this.map = new HashMap<Integer, Integer>();
    }
      //time: O(1)
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        if(map.containsKey(number)){
            int value = this.map.get(number) + 1;
            this.map.replace(number, value);
        }
        else{
            this.map.put(number, 1);
        }
        
    }
    //time: O(n)
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        for(Map.Entry<Integer, Integer> entry : this.map.entrySet()){
            int target = value - entry.getKey();
            if(target != entry.getKey()){
                if(this.map.containsKey(target)){
                    return true;
                }
            }
            else{
                if(entry.getValue() > 1){
                    return true;
                }
            }
        }
        return false;
    }
}

/**
 * Your TwoSum object will be instantiated and called as such:
 * TwoSum obj = new TwoSum();
 * obj.add(number);
 * boolean param_2 = obj.find(value);
 */
```

