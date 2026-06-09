# LeetCode 57 - Insert Interval

## Problem
Given a set of non-overlapping intervals sorted by start time, insert a new interval and merge if necessary.

## Approach
1. Add intervals completely before the new interval.
2. Merge all overlapping intervals.
3. Insert the merged interval.
4. Add the remaining intervals.

## Time Complexity
O(n)

## Space Complexity
O(n)

## C++ Solution
```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> ans;
        int n = intervals.size();
        int i = 0;

        while (i < n && intervals[i][1] < newInterval[0]) {
            ans.push_back(intervals[i]);
            i++;
        }

        while (i < n && intervals[i][0] <= newInterval[1]) {
            newInterval[0] = min(newInterval[0], intervals[i][0]);
            newInterval[1] = max(newInterval[1], intervals[i][1]);
            i++;
        }

        ans.push_back(newInterval);

        while (i < n) {
            ans.push_back(intervals[i]);
            i++;
        }

        return ans;
    }
};
