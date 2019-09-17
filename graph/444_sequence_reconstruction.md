# 444 Sequence Reconstruction

```java
/*
Check whether the original sequence org can be uniquely reconstructed from the sequences in seqs. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 104. Reconstruction means building a shortest common supersequence of the sequences in seqs (i.e., a shortest sequence so that all sequences in seqs are subsequences of it). Determine whether there is only one sequence that can be reconstructed from seqs and it is the org sequence.

Example 1:

Input:
org: [1,2,3], seqs: [[1,2],[1,3]]

Output:
false

Explanation:
[1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.
Example 2:

Input:
org: [1,2,3], seqs: [[1,2]]

Output:
false

Explanation:
The reconstructed sequence can only be [1,2].
Example 3:

Input:
org: [1,2,3], seqs: [[1,2],[1,3],[2,3]]

Output:
true

Explanation:
The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].
Example 4:

Input:
org: [4,1,5,2,6,3], seqs: [[5,2,6,3],[4,1,5,2]]

Output:
true
*/

class Solution {
    public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        Map<Integer, Integer> indegree = new HashMap(); // use BFS topsort
        for (List<Integer> seq : seqs) {
            for (int i = 0; i < seq.size(); i++) {
                int vertex = seq.get(i);
                graph.putIfAbsent(vertex, new ArrayList<Integer>());
                indegree.putIfAbsent(vertex, 0);
                if (i > 0) {
                    int lastVertex = seq.get(i-1);
                    graph.get(lastVertex).add(vertex);
                    indegree.put(vertex, indegree.get(vertex) + 1);
                }
            }
        }
        if (org.length != indegree.size()) {
            return false;
        }
        Queue<Integer> queue = new LinkedList<>(); // queue for BFS
        for (Map.Entry<Integer, Integer> entry : indegree.entrySet()) {
            if (entry.getValue() == 0) {
                queue.add(entry.getKey());
            }
        }
        int index = 0;
        while (!queue.isEmpty()) {
            if (queue.size() > 1) {
                return false;
            }
            int vertex = queue.poll();
            if (org[index++] != vertex) {
                return false;
            }
            for (int neighbor : graph.get(vertex)) {
                indegree.put(neighbor, indegree.get(neighbor) - 1);
                if (indegree.get(neighbor) == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        return index == org.length;
    }
}

```
