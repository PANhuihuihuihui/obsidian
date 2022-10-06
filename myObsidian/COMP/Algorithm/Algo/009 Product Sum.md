---
aliases: [algo 009]
tags:
  - 
---

## Algo 009
sum in the array times the depths of the array

```java
class Program {  
public static int productSum(List<Object> array) {
        return productSumHelper(array, 1);
    }
    public productSumHelper(List<Object> array,int depth){
        int sum = 0;
        for(int i =0; i<array.size();i++){
	        if(array[i] instanceof ArrayList){
	            sum += productSumHelper(array[i],depth+1);
	        }
	        else{
	            sum += array[i];
	        }
        }
        return sum*depth;
    }
}
```

suggest  answer 

```java
public static int productSum(List<Object> array) {
	return productSumHelper(array, 1); 
}
public static int productSumHelper(List<Object> array, int multiplie)
	int sum = 0;
	for (Object el : array) {
		if (el instanceof ArrayList) { 
		@SuppressWarnings("unchecked") 
		ArrayList<Object> ls = (ArrayList<Object>) el; 
		sum += productSumHelper(ls, multiplier + 1);
		}else{
			sum += (int) el;
		} 
	}
	return sum * multiplier; 
}
```

#### Takeaway
java 类型转换！