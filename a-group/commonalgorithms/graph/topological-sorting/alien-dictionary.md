# Alien Dictionary

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of **non-empty** words from the dictionary, where words are **sorted lexicographically by the rules of this new language**. Derive the order of letters in this language.

Example

**Example 1:**

```
Input：["wrt","wrf","er","ett","rftt"]
Output："wertf"
Explanation：
from "wrt"and"wrf" ,we can get 't'<'f'
from "wrt"and"er" ,we can get 'w'<'e'
from "er"and"ett" ,we can get 'r'<'t'
from "ett"and"rftt" ,we can get 'e'<'r'
So return "wertf"
```

**Example 2:**

```
Input：["z","x"]
Output："zx"
Explanation：
from "z" and "x"，we can get 'z' < 'x'
So return "zx"
```

```java
public class Solution {
    /**
     * @param words: a list of words
     * @return: a string which is correct order
     */
    public String alienOrder(String[] words) {
        // Topo sort
        // Edge case
        if(words == null || words.length == 0) return "";
        
        //1. Init inDegree & topoMap
        HashMap<Character, Integer> inDegree = new HashMap<>();
        HashMap<Character, List<Character>> topoMap = new HashMap<>();
        for(String word : words)
            for(char c : word.toCharArray()) {
                inDegree.put(c, 0);
                topoMap.put(c, new ArrayList<Character>());
            }
        
        //2. Build Map
        for(int i = 0; i < words.length - 1; i++) {
            String w1 = words[i], w2 = words[i + 1];
            for(int j = 0; j < Math.min(w1.length(), w2.length()); j++) {
                char parent = w1.charAt(j), child = w2.charAt(j);
                if(parent != child) {
                    inDegree.put(child, inDegree.get(child) + 1);
                    topoMap.get(parent).add(child);
                    break;
                }
            }
        }
        
        //3. Topo sort
        StringBuilder res = new StringBuilder();
        while(!inDegree.isEmpty()) {
            boolean flag = false;
            for(Character c : inDegree.keySet()) {
                if(inDegree.get(c) == 0) {
                    flag = true;
                    res.append(c);
                    List<Character> children = topoMap.get(c);
                    for(Character ch : children)
                        inDegree.put(ch, inDegree.get(ch) - 1);
                    inDegree.remove(c);
                    break;
                }
            }
            if(flag == false)
                return "";
        }
        return res.toString();
    }
}
```
