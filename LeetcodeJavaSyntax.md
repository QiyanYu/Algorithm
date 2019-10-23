## LinkedList
```java
LinkedList<Integer> ans = new LinkedList<>(); 
ans.add(0, 111) // add an element into the first index
ans.offerFirst(111) // the same as the last one
```

## Array
```java
int[] count = new int[26]; 
Arrays.fill(count, Integer.MAX_VALUE);
IntStream.Of(count).sum();
int[] copy = count.clone():
Arrays.sort(copy);
```

## String
```java
Character.toString((char) ('a' + i))
```

## Directions
```java
for(int[] d : new int[][] {{1,0}, {-1,0}, {0,1}, {0,-1}}){}
```