# Merge_interval_snip


## Q1
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

Example 1:

Given intervals [1,3],[6,9] insert and merge [2,5] would result in [1,5],[6,9].

Example 2:

Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] would result in [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

Make sure the returned intervals are also sorted.

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
vector<Interval> Solution::insert(vector<Interval> &v, Interval i) {
    vector<Interval> sol;
    int n=v.size();
    int start=i.start;
    int end=i.end;
    start=min(start,end);
    end=max(start,end);
    bool flag=false;
    for(int i=0;i<n;i++){
        if(v[i].end<start){
            sol.push_back(v[i]);
        }else if(v[i].start>end){
            if(flag==false){
                sol.push_back({start,end});
            }
            sol.push_back(v[i]);
            flag=true;
        }else{
            start=min(v[i].start,start);
            end=max(v[i].end,end);
        }
    }

    if(flag==false){
        sol.push_back({start,end});
    }
    
    return sol;
}


```



## Q2
Given a collection of intervals, merge all overlapping intervals.

For example:

Given [1,3],[2,6],[8,10],[15,18],

return [1,6],[8,10],[15,18].

Make sure the returned intervals are sorted.

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
bool compare(Interval a, Interval b){
    return a.start<b.start;
}
vector<Interval> Solution::merge(vector<Interval> &A) {
    sort(A.begin(),A.end(),compare);
    int st = A[0].start;
    int en = A[0].end;
    vector<Interval> ans;
    ans.push_back({st,en});
    for(int i=1;i<A.size();i++){
        if(A[i].start>en){
            ans.push_back({A[i].start,A[i].end});
            st=A[i].start;
            en=A[i].end;
        }else if(A[i].start<en){
            st=min(st,A[i].start);
            en=max(en,A[i].end);
            ans.pop_back();
            ans.push_back({st,en});
        }
    }
    return ans;

}



```
