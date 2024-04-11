## Reaching Points

Given four integers sx, sy, tx, and ty, return true if it is possible to convert the point (sx, sy) to the point (tx, ty) through some operations, or false otherwise.

The allowed operation on some point (x, y) is to convert it to either (x, x + y) or (x + y, y).

 

Example 1:

Input: sx = 1, sy = 1, tx = 3, ty = 5
Output: true
Explanation:
One series of moves that transforms the starting point to the target is:
(1, 1) -> (1, 2)
(1, 2) -> (3, 2)
(3, 2) -> (3, 5)
**********************************************************************************************************************************************************************************


    public class Solution{
	public boolean reachingPoints(int sx, int sy, int tx, int ty){
		while(sx < tx && sy < ty){
			if(tx > ty){
				tx = tx % ty;
			}
			else{
				ty = ty % tx;
			}
		}
		if(sx == tx && sy <= ty){
			return (ty - sy) % tx == 0;
		}
		else{
			return sy == ty && sx <= tx && (tx - sx) % ty == 0;
		}
	}
           }
