      Solution {

    public List<Integer> frequencyCount(int[] arr) {
    

      Map <Integer,Integer> map = new HashMap<>();
        List <Integer> list = new ArrayList<>();
      for(int i=0;i<arr.length;i++)
    {
     map.put(arr[i],map.getOrDefault(arr[i],0)+1);
     }
    for(int i=1;i<=arr.length;i++)
    {
     list.add( map.getOrDefault(i, 0));
    }
    return list ;
  
      }


### Syntax:
```java
V getOrDefault(Object key, V defaultValue)
```

- **`key`**: The key whose associated value is to be returned.
- **`defaultValue`**: The value to return if the key is not present in the map.

### Purpose:
- If the `key` exists in the map, `getOrDefault` returns the associated value.
- If the `key` does not exist, `getOrDefault` returns the `defaultValue` provided.

### Example:
```java
Map<Integer, String> map = new HashMap<>();
map.put(1, "One");
map.put(2, "Two");

// Using getOrDefault
System.out.println(map.getOrDefault(1, "Default")); // Output: One
System.out.println(map.getOrDefault(3, "Default")); // Output: Default
```

### Use Case in Your Code:
In the context of your code, `getOrDefault` is used to ensure that if a number is not present in the map, its frequency is considered `0`. This is particularly useful for building a list of frequencies where you want to account for all possible keys (even if some do not appear in the map).

```java
map.put(arr[i], map.getOrDefault(arr[i], 0) + 1);
```

In this line:
- **`map.getOrDefault(arr[i], 0)`** retrieves the current frequency of `arr[i]` or returns `0` if `arr[i]` is not already in the map.
- **`+ 1`** increments the frequency count.

