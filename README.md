Java HashMap Notes


What is a HashMap?

- HashMap<K, V> is a key-value data structure in Java.
- It allows fast insertion, deletion, and lookup in O(1) average time complexity.
- It does not maintain order (use LinkedHashMap if order is needed).
```
java
CopyEdit
import java.util.HashMap;

HashMap<String, Integer> map = new HashMap<>();

```

---

2️⃣ Commonly Used HashMap Methods


(A) Basic Operations

Method
Description
put(K key, V value)
Inserts or updates a key-value pair.
get(K key)
Returns the value for a given key (or null if key is missing).
getOrDefault(K key, V defaultValue)
Returns the value for a key, or a default value if key doesn't exist.
remove(K key)
Removes a key-value pair.
containsKey(K key)
Checks if a key exists in the map.
containsValue(V value)
Checks if a value exists in the map.
size()
Returns the number of key-value pairs.
isEmpty()
Checks if the map is empty.
clear()
Removes all key-value pairs from the map.

Example:

```
java
CopyEdit
import java.util.*;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();

        map.put("Apple", 10);
        map.put("Banana", 5);
        map.put("Cherry", 7);

        System.out.println(map.get("Apple")); // Output: 10
        System.out.println(map.getOrDefault("Grapes", 0)); // Output: 0
        System.out.println(map.containsKey("Banana")); // Output: true
        System.out.println(map.containsValue(7)); // Output: true
        map.remove("Cherry");
        System.out.println(map.size()); // Output: 2
    }
}

```

---

(B) Iterating Through a HashMap


1️⃣ Using entrySet()

```
java
CopyEdit
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}

```

2️⃣ Using keySet()

```
java
CopyEdit
for (String key : map.keySet()) {
    System.out.println(key + " -> " + map.get(key));
}

```

3️⃣ Using values()

```
java
CopyEdit
for (Integer value : map.values()) {
    System.out.println(value);
}

```

---

(C) Advanced Methods

Method
Description
replace(K key, V value)
Replaces the value of a specific key.
putIfAbsent(K key, V value)
Inserts the key-value pair only if the key is missing.
computeIfAbsent(K key, Function<K, V> mappingFunction)
Computes a value only if the key is missing.
computeIfPresent(K key, BiFunction<K, V, V> remappingFunction)
Updates the value only if the key exists.

Example:

```
java
CopyEdit
map.putIfAbsent("Apple", 15); // Won't update because "Apple" exists
map.computeIfAbsent("Grapes", k -> 20); // Adds "Grapes" -> 20
map.computeIfPresent("Banana", (k, v) -> v + 5); // Updates Banana -> 10

```

---

(D) Sorting a HashMap

HashMaps are unordered, but you can sort them:

1️⃣ Sort by Key

```
java
CopyEdit
Map<String, Integer> sortedMap = new TreeMap<>(map);
System.out.println(sortedMap); // Sorted by keys

```

2️⃣ Sort by Value

```
java
CopyEdit
map.entrySet().stream()
   .sorted(Map.Entry.comparingByValue())
   .forEach(entry -> System.out.println(entry.getKey() + " -> " + entry.getValue()));

```

---

3️⃣ When to Use HashMap?

✅ Fast Lookups & Insertions - Best for key-value data retrieval.
✅ Counting Frequencies - Example: word or character counting.
✅ Removing Duplicates - Store unique keys.
❌ Need Order? - Use LinkedHashMap or TreeMap instead.
---

4️⃣ Example Problem


Find the Frequency of Elements in an Array

```
java
CopyEdit
import java.util.*;

public class FindFrequency {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 2, 1, 2, 4, 3, 1};

        Map<Integer, Integer> freqMap = new HashMap<>();

        for (int num : arr) {
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }

        for (Map.Entry<Integer, Integer> entry : freqMap.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}

```

---

Conclusion : 

- HashMap is one of the most used Java data structures for fast lookups.
- It offers a variety of useful methods for manipulation.
- Order is not maintained, so use LinkedHashMap or TreeMap when needed.


1️⃣ Count Character Frequency in a String

📝 Problem: Given a string, count the occurrences of each character.

Example

```
rust
CopyEdit
Input:  "hello"
Output: 
h -> 1
e -> 1
l -> 2
o -> 1

```

Solution

java
CopyEdit
```
import java.util.*;

public class CharFrequency {
    public static void main(String[] args) {
        String str = "hello";

        Map<Character, Integer> charCount = new HashMap<>();

        for (char ch : str.toCharArray()) {  //str.toCharArray() converts the given string into an array of characters.
                                             //The for loop iterates over each character in that array, assigning it to the variable ch in each iteration.
            charCount.put(ch, charCount.getOrDefault(ch, 0) + 1);  
// charCount.getOrDefault(ch, 0)

//This checks if ch (the current character) is already present in the charCount HashMap.
//If ch is present, it retrieves its current count.
//If ch is NOT present, it returns 0 by default.
//2️⃣ + 1

//Adds 1 to the retrieved value (since we found another occurrence of ch).
//3️⃣ charCount.put(ch, newValue)

//Updates the HashMap with the new frequency count of ch.
        }

        for (Map.Entry<Character, Integer> entry : charCount.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}

```
🔹 Use Case: Useful in anagram checking and data compression.
---

2️⃣ Find the First Non-Repeating Character

📝 Problem: Given a string, find the first character that appears only once.

Example

```
vbnet
CopyEdit
Input:  "swiss"
Output: w

```

Solution

```
java
CopyEdit
import java.util.*;

public class FirstUniqueChar {
    public static void main(String[] args) {
        String str = "swiss";
        Map<Character, Integer> charCount = new HashMap<>();

        for (char ch : str.toCharArray()) {
            charCount.put(ch, charCount.getOrDefault(ch, 0) + 1);
        }

        for (char ch : str.toCharArray()) {
            if (charCount.get(ch) == 1) {
                System.out.println("First non-repeating character: " + ch);
                return;
            }
        }
        System.out.println("No unique character found");
    }
}

```
🔹 Use Case: Important for text processing and search algorithms.
---

3️⃣ Two Sum Problem (Pair with Given Sum)

📝 Problem: Find two numbers in an array that add up to a given target sum.

Example

```
makefile
CopyEdit
Input:  nums = [2, 7, 11, 15], target = 9
Output: (2, 7)

```

Solution

```
java
CopyEdit
import java.util.*;

public class TwoSum {
    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        Map<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            int complement = target - num;
            if (map.containsKey(complement)) {
                System.out.println("Pair found: (" + complement + ", " + num + ")");
                return;
            }
            map.put(num, 1);
        }
        System.out.println("No pair found");
    }
}

```
🔹 Use Case: Used in interview problems and array-based optimizations.
---

4️⃣ Group Anagrams

📝 Problem: Given a list of words, group words that are anagrams.

Example

```
lua
CopyEdit
Input:  ["bat", "tab", "cat", "act", "tac"]
Output: [[bat, tab], [cat, act, tac]]

```

Solution

```
java
CopyEdit
import java.util.*;

public class GroupAnagrams {
    public static void main(String[] args) {
        String[] words = {"bat", "tab", "cat", "act", "tac"};
        Map<String, List<String>> anagramGroups = new HashMap<>();

        for (String word : words) {
            char[] chars = word.toCharArray();
            Arrays.sort(chars);
            String sorted = new String(chars);

            anagramGroups.putIfAbsent(sorted, new ArrayList<>());
            anagramGroups.get(sorted).add(word);
        }

        System.out.println(anagramGroups.values());
    }
}

```
🔹 Use Case: Used in dictionary-based applications and sorting algorithms.
---

5️⃣ Find Duplicates in an Array

📝 Problem: Find all duplicate elements in an array.

Example

```
makefile
CopyEdit
Input:  [4, 5, 6, 7, 4, 6, 8]
Output: [4, 6]

```

Solution

```
java
CopyEdit
import java.util.*;

public class FindDuplicates {
    public static void main(String[] args) {
        int[] arr = {4, 5, 6, 7, 4, 6, 8};
        Map<Integer, Integer> map = new HashMap<>();
        Set<Integer> duplicates = new HashSet<>();

        for (int num : arr) {
            map.put(num, map.getOrDefault(num, 0) + 1);
            if (map.get(num) > 1) {
                duplicates.add(num);
            }
        }

        System.out.println("Duplicates: " + duplicates);
    }
}

```
🔹 Use Case: Used in data cleaning and checking repeated values.
---

6️⃣ Find Intersection of Two Arrays

📝 Problem: Find the common elements between two arrays.

Example

```
makefile
CopyEdit
Input:  
arr1 = [1, 2, 3, 4, 5]
arr2 = [3, 4, 5, 6, 7]
Output: [3, 4, 5]

```

Solution

```
java
CopyEdit
import java.util.*;

public class ArrayIntersection {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        int[] arr2 = {3, 4, 5, 6, 7};

        Set<Integer> set1 = new HashSet<>();
        Set<Integer> result = new HashSet<>();

        for (int num : arr1) {
            set1.add(num);
        }

        for (int num : arr2) {
            if (set1.contains(num)) {
                result.add(num);
            }
        }

        System.out.println("Intersection: " + result);
    }
}

```
🔹 Use Case: Used in database queries and data comparison tasks.
---

7️⃣ Check if Two Strings are Isomorphic

📝 Problem: Two strings are isomorphic if each character in one string maps to a unique character in the other.

Example

```
vbnet
CopyEdit
Input:  ("egg", "add")
Output: true

Input:  ("foo", "bar")
Output: false

```

Solution

```
java
CopyEdit
import java.util.*;

public class IsomorphicStrings {
    public static void main(String[] args) {
        System.out.println(areIsomorphic("egg", "add")); // true
        System.out.println(areIsomorphic("foo", "bar")); // false
    }

    public static boolean areIsomorphic(String s1, String s2) {
        if (s1.length() != s2.length()) return false;

        Map<Character, Character> map = new HashMap<>();
        Set<Character> mappedValues = new HashSet<>();

        for (int i = 0; i < s1.length(); i++) {
            char c1 = s1.charAt(i);
            char c2 = s2.charAt(i);

            if (map.containsKey(c1)) {
                if (map.get(c1) != c2) return false;
            } else {
                if (mappedValues.contains(c2)) return false;
                map.put(c1, c2);
                mappedValues.add(c2);
            }
        }
        return true;
    }
}

```
🔹 Use Case: Used in pattern matching and cryptographic algorithms.
---

Conclusion

These HashMap-based problems are frequently asked in interviews and are useful in real-world applications
