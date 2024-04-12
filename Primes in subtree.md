### Primes in subtree

In this challenge, construct a rooted undirected graph and then answer some queries on the graph. There are n nodes numbered from 1 to n. All the nodes are disconnected initially. Construct the graph by drawing an undirected edge between mpairs of nodes, picking one pair at a time and connecting the first and second nodes. After connecting each of the pairs, the graph construction is complete, and node 1 is the root node of this graph. A node's parent is the next node on the shortest path from that node to node 1, and a descendant is on the shortest path to a leaf moving away from node 1. At this point, the graph can be considered a tree rooted at node 1, and subtrees can be formed rooted at any node and consisting of its descendants.

Each node has a positive integer value associated with it. Find the total number of nodes with values as prime numbers in a given subtree rooted at a given node. Note that 1 is not a prime number. There are multiple queries.

► Sample Tree Construction

Function Description

Complete the function primeQuery in the editor below. The function must return an array of integers, each the result of a query, aligned by index.

primeQuery has the following parameters:

n an integer that denotes the number of nodes in the graph to be labeled 1 to n

first[first[0]....first[m-1]]: an array of integers that denotes first node of each pair[i]

second(second[0], second[m-1]] an array of integers that denotes second node of each pair[i]

values[values[1].values[n]]: an array of integers that denotes the data value for each node[i]

queries[queries[0],...queries[q-1 ...queries(q-1]) an array of integers, the node numbers to query

Constraints





***********************************************************************************************************************************************************************8

    import java.util.*;

    public class PrimeQueryInSubtree {
    static int[] numPrimesInSubtree;
    static boolean[] isPrime;
    static List<List<Integer>> adj;

    public static void main(String[] args) {
        // Sample usage
        int n = 6; // Number of nodes
        int[][] pairs = {{1, 2}, {1, 3}, {2, 4}, {2, 5}, {3, 6}}; // Pair of nodes forming edges
        int[] values = {2, 3, 5, 7, 11, 13}; // Values of each node
        int[] queries = {1, 2, 3, 4, 5, 6}; // Queries to find number of primes in subtrees
        int m = pairs.length; // Number of edges
        int q = queries.length; // Number of queries
        boolean[] isPrime = sieveOfEratosthenes(20); // Sieve of Eratosthenes to find primes
        numPrimesInSubtree = new int[n + 1]; // 1-indexed, so n+1 elements

        adj = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            adj.add(new ArrayList<>());
        }

        // Building the adjacency list
        for (int[] pair : pairs) {
            int u = pair[0];
            int v = pair[1];
            adj.get(u).add(v);
            adj.get(v).add(u);
        }

        dfs(1, 0, values);

        // Answering queries
        List<Integer> results = new ArrayList<>();
        for (int query : queries) {
            results.add(numPrimesInSubtree[query]);
        }

        // Printing the number of primes in the subtree for each query
        for (int i = 0; i < q; i++) {
            System.out.println("Query " + queries[i] + ": " + results.get(i));
        }
    }

    static void dfs(int i, int par, int[] values) {
        int fromSelf = isPrime[values[i - 1]] ? 1 : 0; // Checking if the value is prime
        int fromRecursion = 0;

        for (int u : adj.get(i)) {
            if (u == par)
                continue;
            dfs(u, i, values);
            fromRecursion += numPrimesInSubtree[u];
        }

        numPrimesInSubtree[i] = fromSelf + fromRecursion;
    }

    static boolean[] sieveOfEratosthenes(int n) {
        boolean[] primes = new boolean[n + 1];
        Arrays.fill(primes, true);
        primes[0] = primes[1] = false;
        for (int i = 2; i * i <= n; i++) {
            if (primes[i]) {
                for (int j = i * i; j <= n; j += i) {
                    primes[j] = false;
                }
            }
        }
        return primes;
    }
    }
