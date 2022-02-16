# 0-1 Knapsack 背包问题 II

Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T. \
\
All candidate numbers are unique. The same repeated number may be chosen from C unlimited number of times. Note: \
\
All numbers (including target) will be positive integers. Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak). \
\
The solution set must not contain duplicate combinations. \
\
Example Input: \[7], \[2, 3, 6, 7] \
\
Example Output: \[\[2, 2, 3], \[7]]



```java
public static void main(String[] args) {
//		Example Input: [7], [2, 3, 6, 7]
//		Example Output: [[2, 2, 3], [7]]

		int[] items = new int[]{2,3,6,7};
		int target = 7;

		//[[2,2,3], [7]]
		ArrayList<ArrayList<Integer>> result = knapsack(items, target);

		System.out.println(result.size());
		result.forEach(item -> {
			System.out.println("Result is: ");
			for (Integer integer : item) {
				System.out.println(integer);
			}
		} );

	}


	public static ArrayList<ArrayList<Integer>> knapsack(int[] items,
												  int target) {

		ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
		ArrayList<Integer> cur = new ArrayList<Integer>();
		knapsack(items, result, cur, 0, target);
		return result;
	}

	public static  void knapsack(int[] items, ArrayList<ArrayList<Integer>> result, ArrayList<Integer> cur, int index, int target){

		if(target == 0){
			result.add(new ArrayList<Integer>(cur));//共用参数，需要重新创建
			return;
		}

		if(target < 0 || (items.length == index && target != 0)){
			return;
		}
		//拿了item, index不动
		cur.add(items[index]);
		knapsack(items, result, cur, index, target - items[index]);
		//不拿item, index + 1，继续往前走，拿下一个
		cur.remove(cur.size() - 1);
		knapsack(items, result, cur, index + 1, target);

	}
```

解法2：\


```java
public static void knapsack2(int[] items, ArrayList<ArrayList<Integer>> result,
								 ArrayList<Integer> cur, int index, int target){
		if(target == 0){
			result.add(new ArrayList<Integer>(cur));
			return;
		}

		if(target < 0 || (items.length == index && target != 0)){
			return;
		}

		for(int i = index; i < items.length; i++){
			cur.add(items[i]);
			knapsack2(items, result, cur, i, target - items[i] );
			cur.remove(cur.size() - 1);
		}

	}
```
