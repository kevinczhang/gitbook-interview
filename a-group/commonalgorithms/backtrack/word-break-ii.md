# Word Break II

Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences. For example, given

s = "catsanddog",&#x20;

dict = \["cat", "cats", "and", "sand", "dog"].&#x20;

A solution is \["cats and dog", "cat sand dog"].

## Solution

```java
public class Solution {
    public List<String> wordBreak(String s, Set<String> wordDict) {
        List<String>[] pos = new ArrayList[s.length()+1];
        pos[0] = new ArrayList<String>();
        // Construct a graph
        for(int i = 0; i < s.length(); i++){
            if(pos[i] == null) continue;
            for(int j = i+1; j <= s.length(); j++){
                String sub = s.substring(i,j);
                if(!wordDict.contains(sub)) continue;
                if(pos[j] == null){
                    pos[j] = new ArrayList<String>();
                }
                pos[j].add(sub);
            }
        }
 
        List<String> result = new ArrayList<String>();
        if(pos[s.length()] != null)
            dfs(pos, result, "", s.length());
        return result;
    }
 
    public void dfs(List<String>[] pos, List<String> result, 
				String curr, int curInd){
        if(curInd == 0){
            result.add(curr.trim());
            return;
        }
 
        for(String s : pos[curInd]){
            String combined = s + " "+ curr;
            dfs(pos, result, combined, curInd - s.length());
        }
    }
}

```
