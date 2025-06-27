# Leetcode----2014
Longest Subsequence Repeated k Times Difficulty: Hard
//code in java 
import java.util.*;

class Solution {
    public String longestSubsequenceRepeatedK(String s, int k) {
        // Count frequency of each character
        Map<Character, Integer> freq = new HashMap<>();
        for (char c : s.toCharArray()) {
            freq.put(c, freq.getOrDefault(c, 0) + 1);
        }

        // Build filtered string with only characters having frequency >= k
        StringBuilder filtered = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (freq.get(c) >= k) {
                filtered.append(c);
            }
        }

        s = filtered.toString();
        Queue<String> queue = new LinkedList<>();
        queue.offer("");

        String result = "";

        while (!queue.isEmpty()) {
            String curr = queue.poll();

            for (char c = 'a'; c <= 'z'; c++) {
                String next = curr + c;
                if (isKSubsequence(s, next, k)) {
                    queue.offer(next);
                    if (next.length() > result.length() ||
                        (next.length() == result.length() && next.compareTo(result) > 0)) {
                        result = next;
                    }
                }
            }
        }

        return result;
    }

    // Check if sub repeated k times is a subsequence of s
    private boolean isKSubsequence(String s, String sub, int k) {
        int i = 0, j = 0, count = 0;
        while (i < s.length()) {
            if (s.charAt(i) == sub.charAt(j)) {
                j++;
                if (j == sub.length()) {
                    count++;
                    if (count == k) return true;
                    j = 0;
                }
            }
            i++;
        }
        return false;
    }
}
