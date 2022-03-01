# Amazon OA 2

Find the strength a password as per the definition of strength mentioned below

The strength of a password is the sum of all the unique characters in all the possible substrings of a word.

E.g password is "test"\
possible substrings are -> "t","e","s","t", "te","es","st", "tes", "est", "test"

here the strength is 1 + 1 + 1 + 1+ 2+ 2 + 2 + 3 + 3 + 3 = 19

Let me know in comments section if you need clarity.

Link to similar question is\
[https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/](https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/)



```java
class Result {

    /*
     * Complete the 'findPasswordStrength' function below.
     *
     * The function is expected to return a LONG_INTEGER.
     * The function accepts STRING password as parameter.
     */

    public static long findPasswordStrength(String s) {
		Map<Character, long[]> map = new HashMap<>();
		long pre = 0;
		long res = 0;
//teet,
//t				cur = 1
//te -> e, te	cur = 3,	i = 1
//tee -> e', ee', tee', 	cur = 6,	i=2, res = 4, curres = 1
//teet -> et', eet', teet', t' cur = 10,		res = 9, curres = 3

		for(int i = 0; i < s.length(); i++){
			long cur = pre + i + 1;
			char c = s.charAt(i);
			if(!map.containsKey(c)){
				map.put(c, new long[] {0,0});
			}
			long[] v = map.get(c);
			map.put(c, new long[]{ i+1, v[0]+v[1] }); //{3,2}
			res += cur - sum(map); //curres = 4; {ee, tee}
			pre = cur;

		}
		return res;
	}
	
    public static long sum(Map<Character, long[]> map){
        long res = 0;
        for(long[] values : map.values()){
            res += values[1];
        }
        return res;
    }
}
```
