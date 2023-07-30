# Word Ladder II

Given two words (start and end), and a dictionary, find all shortest transformation sequence(s) from start to end, such that:

1. Only one letter can be changed at a time.&#x20;
2. Each intermediate word must exist in the dictionary.

#### Notice

* All words have the same length.&#x20;
* All words contain only lowercase alphabetic characters.

## Solution

```java
public class Solution {
    	    
    class WordNode {
		String word;
		int numSteps;
		WordNode pre;

		public WordNode(String word, int numSteps, WordNode pre) {
			this.word = word;
			this.numSteps = numSteps;
			this.pre = pre;
		}
	};

	public List<List<String>> findLadders(String start, String end, Set<String> dict) {
		List<List<String>> result = new ArrayList<List<String>>();
		Set<String> visited = new HashSet<String>();
		Set<String> unvisited = new HashSet<String>();
		unvisited.addAll(dict);
		int minStep = 0, preSteps = 0;
		Queue<WordNode> queue = new LinkedList<WordNode>();
		queue.offer(new WordNode(start, 1, null));

		while (!queue.isEmpty()) {
			WordNode top = queue.poll();
			String curWord = top.word;
			int curSteps = top.numSteps;
			if (curWord.equals(end)) {
				if (minStep == 0)
					minStep = curSteps;
				if (curSteps == minStep) {
					List<String> temp = new ArrayList<String>();
					temp.add(curWord);
					while (top.pre != null) {
						top = top.pre;
						temp.add(0, top.word);
					}
					result.add(temp);
					continue;
				}
			}
			// Next level
			if (preSteps < curSteps) {
				unvisited.removeAll(visited);
				preSteps = curSteps;
			}
			char[] wordChars = curWord.toCharArray();
			for (int i = 0; i < wordChars.length; i++) {
				for (char c = 'a'; c <= 'z'; c++) {
					char temp = wordChars[i];
					wordChars[i] = c;
					String newWord = new String(wordChars);
					if (unvisited.contains(newWord)) {
						queue.add(new WordNode(newWord, curSteps + 1, top));
						visited.add(newWord);
					}
					wordChars[i] = temp;
				}
			}
		}
		return result;
	}
}

```
