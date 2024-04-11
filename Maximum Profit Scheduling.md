### Maximum Profit in Job Scheduling

Solved
Hard
Topics
Companies
Hint
We have n jobs, where every job is scheduled to be done from startTime[i] to endTime[i], obtaining a profit of profit[i].

You're given the startTime, endTime and profit arrays, return the maximum profit you can take such that there are no two jobs in the subset with overlapping time range.

If you choose a job that ends at time X you will be able to start another job that starts at time X.

 

Example 1:



Input: startTime = [1,2,3,3], endTime = [3,4,5,6], profit = [50,10,40,70]
Output: 120
Explanation: The subset chosen is the first and fourth job. 
Time range [1-3]+[3-6] , we get profit of 120 = 50 + 70.
************************************************************************************************************************************************************************************************


    class Solution {
    class Job{
        int start, end, profit;
        Job(int start, int end, int profit){
            this.start = start;
            this.end = end;
            this.profit = profit;
        }
    }
    public int jobScheduling(int[] startTime, int[] endTime, int[] profit) {
        int n = profit.length;
        Job []jobs = new Job[n];
        for(int i=0; i<n; i++){
            jobs[i] = new Job(startTime[i], endTime[i], profit[i]);
        }
        
        Arrays.sort(jobs, (a,b) -> (a.end-b.end));              // sorting based on end time
        
        int dp[] = new int[n];                     // dp[i] = maximum profit earned till jobs(1...i)
        dp[0] = jobs[0].profit;
        
        for(int i = 1; i < n; i++){
            
            dp[i] = Math.max(dp[i-1], jobs[i].profit);
            for(int j = i-1; j >= 0; j--){
                if(jobs[j].end <= jobs[i].start){
                    dp[i] = Math.max(dp[i], jobs[i].profit + dp[j]);
                    break;
                }
            }
        }
        return dp[n-1];
    }
    }
                        
