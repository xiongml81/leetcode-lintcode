# Debug Legacy Code

Reference:  
[https://www.geeksforgeeks.org/find-the-point-where-a-function-becomes-negative/](https://www.geeksforgeeks.org/find-the-point-where-a-function-becomes-negative/)  
  
We have a black-box legacy function that nobody knows its source code anymore, but it is pretty critical in the system. We only know that the function takes in a double value and returns a double value, and it is an increasing function. Recently our system got some issues, and we want debug our system. We traced down the output from this function, which is y, and we want to deduce what the value our caller gave to the function so that we could continue to track back in our caller chain. Could you help us what value the caller passes to this function?

#### Comment

Range of double: 4.94065645841246544e-324d to 1.79769313486231570e+308d \(positive or negative\)  
Search on a continuous rang L, with accuracy tolerance of e &gt; 0? How to do it, and whats the search time complexity ? O\(log\(L/e\)\)



```java
public static float debugFunction(Object function, int epsilon, int target) {
		float left = Float.MIN_VALUE ; float right = Float.MAX_VALUE;
		
		while(left  < right) {
			float mid = left + (right - left) / 2;
			if (function(mid) > target + epsilon / 2) {
				right = mid;
				
			}
			else if(function(mid) < target + epsilon / 2) {
				left = mid;
			}
			else
				return mid;
		}
		
		
		
		return -1;
	}
```

