#
**solution**

Sort by start, merge the overlap intervals in order

**time complexity**

O(nlogn) sort. O(n) merge.

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
    struct myOp{
        bool operator() (Interval a, Interval b){return a.start<b.start;}
    }muOp;
    
    
    void merge(vector<Interval>& res,Interval a, Interval b){
        if(a.end > b.start && a.end > b.end)
            return;
        else if(a.end >= b.start && a.end < b.end){
            res.pop_back();
            Interval temp(a.start, b.end);
            res.push_back(temp);
        }
    }
    
    vector<Interval> merge(vector<Interval>& intervals) {
        if(intervals.size() <= 1) return intervals;
        sort(intervals.begin(),intervals.end(),muOp);
        vector<Interval> res;
        res.push_back(intervals[0]);
        for(int i = 1;i < intervals.size();++ i){ 
            if(res.back().end >= intervals[i].start)
                merge(res,res.back(),intervals[i]);
            else{
                res.push_back(intervals[i]);
            }
        }
        return res;
    }
};

```