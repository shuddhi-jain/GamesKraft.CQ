#### primes in subtree


Given a tree consisting of N nodes numbered from 1 to n, the root node being 1. Each node has a value associated with it. Given Q queries with each query having a node number, find the number of nodes that have prime values in the subtree of the given node.

Input Format

First line contains an integer N. Next line contains N space-separated integers denoting the value of the ith node. The lines 3 to N+1 contains two space-separated integers denoting an edge between them. Next line contains an integer Q, the number of queries. Next Q lines contains the node number.

Constraints

1 <= N <= 500000

1 <= Ai <= 1000000

1 <= Q <=500000

Output Format

For each query, output the number of nodes that have a prime value in the subtree of the given node in a new line.

Sample Input 0

4
1 2 3 4
1 2
1 3
1 4
2
1
4
Sample Output 0

2
0
Explanation 0

Node 2 and 3 have values 2 and 3 which are prime and is in the subtree of 1 so the answer for first query is 2. No nodes in the subtree have prime value for second query.

***********************************************************************************************************************************************************************************88

        import java.io.*;
        import java.util.*;
        import java.text.*;
      import java.math.*;
       import java.util.regex.*;


     public class Solution {
    
    static ArrayList<Integer>[] tree;
    static int[] values;
    static boolean[] isPrime;
    static int[] primeCount;
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        int N = scanner.nextInt(); // Number of nodes
        values = new int[N + 1];
        for (int i = 1; i <= N; i++) {
            values[i] = scanner.nextInt(); // Values of each node
        }
        
        tree = new ArrayList[N + 1];
        for (int i = 1; i <= N; i++) {
            tree[i] = new ArrayList<>();
        }
        
        // Building the tree
        for (int i = 0; i < N - 1; i++) {
            int u = scanner.nextInt();
            int v = scanner.nextInt();
            tree[u].add(v);
        }
        
        // Precompute primes
        precomputePrimes();
        
        // DFS to compute prime counts for each subtree
        primeCount = new int[N + 1];
        dfs(1);
        
        int Q = scanner.nextInt(); // Number of queries
        for (int i = 0; i < Q; i++) {
            int query = scanner.nextInt(); // Node number for the query
            System.out.println(primeCount[query]);
        }
    }
    
    // Depth First Search
    static void dfs(int node) {
        primeCount[node] = isPrime[values[node]] ? 1 : 0;
        for (int child : tree[node]) {
            dfs(child);
            primeCount[node] += primeCount[child];
        }
    }
    
    // Precompute primes using Sieve of Eratosthenes
    static void precomputePrimes() {
        int maxVal = Integer.MIN_VALUE;
    for (int value : values) {
    maxVal = Math.max(maxVal, value);
    }
        isPrime = new boolean[maxVal + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i * i <= maxVal; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= maxVal; j += i) {
                    isPrime[j] = false;
                }
            }
        }
    }
    }
