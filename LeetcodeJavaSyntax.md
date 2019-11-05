## LinkedList
```java
LinkedList<Integer> ans = new LinkedList<>(); 
ans.add(0, 111); // add an element into the first index
ans.offerFirst(111); // the same as the last one
```

## ArrayList
```java
ArrayList<Integer> ans = new ArrayList<>();
ans.clear();
```

## Array
```java
int[] count = new int[26]; 
Arrays.fill(count, Integer.MAX_VALUE);
IntStream.Of(count).sum();
int[] copy = count.clone();
Arrays.sort(copy);
Arrays.asList(1, 2);
```

## Character
```java
Character.toString((char) ('a' + i));
Character.isLetterOrDigit();
Character.toLowerCase();
new StringBuilder(s).reverse().toString();
```

## String
```java
s.toLowerCase();
s.replaceAll("regex", ",");
s.equals();
char[] arr = s.toCharArray();
new String(arr);
s.trim();
s.split("\\s+");
```

## Directions
```java
for(int[] d : new int[][] {{1,0}, {-1,0}, {0,1}, {0,-1}}){}
```