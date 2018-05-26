#
**solution**

scan all the vector, merge and insert. Be aware of the corner cases.
Corner case:
[[]] [2,3] , [[1,2]] [3,4] , [[3,4]] [1,2]

**time complexity**

O(n).

**space complexity**

O(n).

```cpp

/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:

    bool overlap(Interval a, Interval b){
        if(a.end < b.start || b.end < a.start) return false;
        return true;
    }
    
    vector<Interval> insert(vector<Interval>& intervals, Interval newInterval) {
        vector<Interval> res;
        if(intervals.size() == 0) {
            res.push_back(newInterval);
        }
        int i = 0;
        for( ;i < intervals.size();++ i){
            
            if(intervals[i].end < newInterval.start)
                res.push_back(intervals[i]);
                
            if(newInterval.end < intervals[i].start){
                res.push_back(newInterval);
                break;
            }
            else if(overlap(newInterval,intervals[i])){
                newInterval.start = min(newInterval.start,intervals[i].start);
                newInterval.end = max(newInterval.end,intervals[i].end);
                
            }
        }
        for( ;i < intervals.size();++ i){
             res.push_back(intervals[i]);
        }
        if(res.size() == 0 || res.back().end < newInterval.start){
            res.push_back(newInterval);
        }
        return res;
    }

};

```