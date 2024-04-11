#### Find Indexes of a subarray with given sum


Given an unsorted array A of size N that contains only non negative integers, find a continuous sub-array that adds to a given number S and return the left and right index(1-based indexing) of that subarray.

In case of multiple subarrays, return the subarray indexes which come first on moving from left to right.

Note:- You have to return an ArrayList consisting of two elements left and right. In case no such subarray exists return an array consisting of element -1.

Example 1:

Input:
N = 5, S = 12
A[] = {1,2,3,7,5}
Output: 2 4
Explanation: The sum of elements 
from 2nd position to 4th position 
is 12.

*********************************************************************************************************************************************************************************************************************

              
    class Solution
    {
    //Function to find a continuous sub-array which adds up to a given number.
    static ArrayList<Integer> subarraySum(int[] arr, int n, int s) 
    {
        ArrayList<Integer> res = new ArrayList<>();
        int sum = 0;
        int start = 0;

        for (int end = 0; end < n; end++) {
            sum += arr[end];

            while (sum > s && start <= end) {
                sum -= arr[start];
                start++;
            }

            if (sum == s && start <= end) {
                res.add(start + 1);
                res.add(end + 1);
                return res; // return only after finding the first subarray
            }
        }

        res.add(-1);
        return res;
    }
    }
