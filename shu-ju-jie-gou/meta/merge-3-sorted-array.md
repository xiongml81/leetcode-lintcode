# Merge 3 sorted array

Implement a function to merge 3 sorted integer arrays. The output should be another sorted integer array consisting of all integers from the 3 input arrays. The input arrays may have duplicates, but the output array shouldn't have any duplicate.

A: \[-100, -10, -1, -1, 0, 0, 0, 1, 1, 5] B: \[-90, -2, 0, 0, 0, 3, 5, 5] C: \[-20, -1, 0, 0, 1, 4, 4]

Output: \[-100, -90, -20, -10, -2, -1, 0, 1, 3, 4, 5]&#x20;

[https://www.geeksforgeeks.org/merge-3-sorted-arrays/](https://www.geeksforgeeks.org/merge-3-sorted-arrays/)

```java
public static ArrayList<Integer> merge3sorted(int A[], int B[],
                                                  int C[]) {
        ArrayList<Integer> ans = new ArrayList<Integer>();
        int l1 = A.length;
        int l2 = B.length;
        int l3 = C.length;
        int i = 0, j = 0, k = 0;
        while (i < l1 || j < l2 || k < l3) {
            // Assigning a, b, c with max values so that if
            // any value is not present then also we can sort
            // the array.
            int a = Integer.MAX_VALUE,
                    b = Integer.MAX_VALUE,
                    c = Integer.MAX_VALUE;

            // a, b, c variables are assigned only if the
            // value exist in the array.
            if (i < l1)
                a = A[i];
            if (j < l2)
                b = B[j];
            if (k < l3)
                c = C[k];

            // Checking if 'a' is the minimum
            if (a <= b && a <= c) {
                ans.add(a);
                i++;
            }
            // Checking if 'b' is the minimum
            else if (b <= a && b <= c) {
                ans.add(b);
                j++;
            }
            // Checking if 'c' is the minimum
            else {
                if (c <= a && c <= b) {
                    ans.add(c);
                    k++;
                }
            }
        }
        return ans;
    }
```

solution 2: merge two first, then merge again one more time

```java
public static int[] merge(int[] arr1, int[] arr2) {
        int m = arr1.length;
        int n = arr2.length;
        int first = 0;
        int last = 0;
        int[] res = new int[m + n];
        int index = 0;

        while (first < m && last < n) {
            int v1 = arr1[first];
            int v2 = arr2[last];
            if (v1 <= v2) {
                res[index] = v1;
                index++;
                first++;
            } else {
                res[index] = v2;
                last++;
            }
        }

        while (first < m) {
            res[index] = arr1[first];
            index++;
            first++;
        }

        while (last < n) {
            res[index] = arr1[last];
            index++;
            last++;
        }

        return res;
    }
```
