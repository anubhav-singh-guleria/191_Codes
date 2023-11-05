## Greedy - Maximum Number of Events That Can Be Attended
<div class="elfjS" data-track-load="description_content"><p>You are given an array of <code>events</code> where <code>events[i] = [startDay<sub>i</sub>, endDay<sub>i</sub>]</code>. Every event <code>i</code> starts at <code>startDay<sub>i</sub></code><sub> </sub>and ends at <code>endDay<sub>i</sub></code>.</p>

<p>You can attend an event <code>i</code> at any day <code>d</code> where <code>startTime<sub>i</sub> &lt;= d &lt;= endTime<sub>i</sub></code>. You can only attend one event at any time <code>d</code>.</p>

<p>Return <em>the maximum number of events you can attend</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/02/05/e1.png" style="width: 400px; height: 267px;">
<pre><strong>Input:</strong> events = [[1,2],[2,3],[3,4]]
<strong>Output:</strong> 3
<strong>Explanation:</strong> You can attend all the three events.
One way to attend them all is as shown.
Attend the first event on day 1.
Attend the second event on day 2.
Attend the third event on day 3.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> events= [[1,2],[2,3],[3,4],[1,2]]
<strong>Output:</strong> 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= events.length &lt;= 10<sup>5</sup></code></li>
	<li><code>events[i].length == 2</code></li>
	<li><code>1 &lt;= startDay<sub>i</sub> &lt;= endDay<sub>i</sub> &lt;= 10<sup>5</sup></code></li>
</ul>
</div>

### Solution

```
// Sort + PriorityQueue Solution
// 1. Sort events by start day
// 2. Store end days of in progress events in min heap
// 3. Join the earliest ending in progress evetns from the earliest start event to the latest start evetn.
//    1) Get current date
//    2) Add just started events at current day in the min heap
//    3) Join the earliest ending event
//    4) Remove already ended events
// 4. Do the loop until we explore all the events and the min heap is empty.
// Time complexity: O(NlogN)
// Space complexity: O(N)
class Solution {
    public int maxEvents(int[][] events) {
        if (events == null || events.length == 0) return 0;
        final int N = events.length;
        // Sort events by start day.
        Arrays.sort(events, (e1, e2) -> Integer.compare(e1[0], e2[0]));
        // Store end days of in progress events in min heap.
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        // Join the earliest ending in progress evetns from the earliest start event to the latest start event.
        int i = 0, day = 0, res = 0;
        while (i < N || !pq.isEmpty()) {
            // Get current date.
            if (pq.isEmpty()) {
                day = events[i][0];
            }
            // Add just started events at current day in the min heap.
            while (i < N && day == events[i][0]) {
                pq.add(events[i][1]);
                i++;
            }
            // Join the earliest ending event.
            pq.poll();
            res++;
            day++;
            // Remove already ended events.
            while (!pq.isEmpty() && day > pq.peek()) {
                pq.poll();
            }
        }
        return res;
    }
}
```

## Greedy - Minimum Platforms
<div class="problems_problem_content__Xm_eO"><p><span style="font-size:18px">Given arrival and departure times of all trains that reach a railway station. Find the minimum number of platforms required for the railway station so that no train is kept waiting.<br>
Consider that all the trains arrive on the same day and leave on the same day. Arrival and departure time can never&nbsp;be the same for a train&nbsp;but we can have arrival time of one train equal to departure time of the other.&nbsp;At any&nbsp;given instance of time, same platform can not be used for both departure of a train and arrival of another train.&nbsp;In such cases,&nbsp;we need different platforms<strong>.</strong></span></p>

<p><br>
<span style="font-size:18px"><strong>Example 1:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input</strong>: n = 6&nbsp;
arr[] = {0900, 0940, 0950, 1100, 1500, 1800}
dep[] = {0910, 1200, 1120, 1130, 1900, 2000}
<strong>Output</strong>: 3
<strong>Explanation</strong>: 
Minimum 3 platforms are required to 
safely arrive and depart all trains.</span></pre>

<p><span style="font-size:18px"><strong>Example 2:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input</strong>: n = 3
arr[] = {0900, 1100, 1235}
dep[] = {1000, 1200, 1240}
<strong>Output</strong>: 1
<strong>Explanation</strong>: Only&nbsp;1 platform is required to 
safely manage the arrival and departure 
of all trains.&nbsp;</span>
</pre>

<p><br>
<span style="font-size:18px"><strong>Your Task:</strong><br>
You don't need to read input or print anything. Your task is to complete the function&nbsp;<strong>findPlatform()</strong>&nbsp;which takes the array arr[] (denoting the arrival times), array dep[] (denoting the departure times)&nbsp;and the size of the array as inputs and returns the minimum number of platforms required at the railway station such that no train waits.</span></p>

<p><span style="font-size:18px"><strong>Note:</strong> Time intervals are in the 24-hour format(<strong>HHMM) ,</strong>&nbsp;where the first two characters represent hour (between 00 to 23 ) and the last two characters represent minutes (this may be &gt; 59).</span></p>

<p><br>
<span style="font-size:18px"><strong>Expected Time Complexity:&nbsp;</strong>O(nLogn)<br>
<strong>Expected Auxiliary Space:&nbsp;</strong>O(n)</span></p>

<p><br>
<span style="font-size:18px"><strong>Constraints:</strong><br>
1 ≤ n ≤ 50000<br>
0000 ≤ A[i] ≤ D[i] ≤ 2359</span></p>
</div>

### Solution
<h3><span>Intuition</span></h3>
<p dir="ltr"><span>The idea is to consider all events in sorted order. Once the events are in sorted order, trace the number of trains at any time keeping track of trains that have arrived, but have not departed.</span></p>
<p dir="ltr"><b><strong>Example:-</strong></b></p>
<p dir="ltr"><span>arr[] &nbsp;= {9:00, &nbsp;9:40, 9:50, &nbsp;11:00, 15:00, 18:00}</span><br><span>dep[] &nbsp;= {9:10, 12:00, 11:20, 11:30, 19:00, 20:00}</span></p>
<p dir="ltr"><span>All events are sorted by time.</span></p><p dir="ltr"><span>Total platforms at any time can be obtained by subtracting total departures from total arrivals by that time.</span></p>
<table class="GFGEditorTheme__table"><colgroup><col><col><col></colgroup><tbody><tr><th class="GFGEditorTheme__tableCell GFGEditorTheme__tableCellHeader" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start; background-color: rgb(242, 243, 245);"><span>&nbsp; &nbsp; &nbsp; &nbsp; Time &nbsp; &nbsp; &nbsp;</span></th><th class="GFGEditorTheme__tableCell GFGEditorTheme__tableCellHeader" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start; background-color: rgb(242, 243, 245);"><span>&nbsp; &nbsp; &nbsp;Event Type &nbsp; &nbsp; &nbsp;</span></th><th class="GFGEditorTheme__tableCell GFGEditorTheme__tableCellHeader" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start; background-color: rgb(242, 243, 245);"><span>Total Platforms Needed at this Time</span></th></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>9:00</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Arrival</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>1</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>9:10</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Departure&nbsp;</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>0</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>9:40</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Arrival</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>1</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>9:50</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Arrival</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>2</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>11:00</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Arrival</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>3</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>11:20</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Departure&nbsp;</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>2</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>11:30</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Departure&nbsp;</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>1</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>12:00</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Departure&nbsp;</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>0</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>15:00</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Arrival</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>1</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>18:00</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Arrival</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>2</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>19:00</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Departure&nbsp;</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>1</span></td></tr><tr><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>20:00</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>Departure&nbsp;</span></td><td class="GFGEditorTheme__tableCell" style="width: 233.333px; border: 1px solid black; vertical-align: top; text-align: start;"><span>0</span></td></tr></tbody></table>
<p dir="ltr"><span>Minimum Platforms needed on railway station = Maximum platforms needed at any time = 3</span></p>
<p dir="ltr"><b><strong>Note: </strong></b><span>This doesn’t create a single sorted list of all events, rather it individually sorts arr[] and dep[] arrays, and then uses the merge process of merge sort to process them together as a single sorted array.</span></p>
<h3><span>Implementation</span></h3>
<p dir="ltr"><b><strong>Steps:-</strong></b></p>
<ol><li value="1"><span>Sort the arrival and departure times of trains.</span></li><li value="2"><span>Create two pointers i=1, and j=0, and a variable to store ans and current count plat.</span></li><li value="3"><span>Run a loop while i&lt;n and j&lt;n and compare the ith element of the arrival array and jth element of the departure array.</span></li><li value="4"><span>If the arrival time is less than or equal to departure then one more platform is needed so increase the count, i.e., plat++ and increment i</span></li><li value="5"><span>Else if the arrival time is greater than the departure then one less platform is needed to decrease the count, i.e., plat– and increment j</span></li><li value="6"><span>Update the ans, i.e. ans = max(ans, plat).</span></li></ol>
<h3><span>Complexity</span></h3>
<ul><li value="1"><b><strong>Time Complexity: O(N * log N),</strong></b><span> One traversal O(n) of both the array is needed, for sorting O(N * log N).</span></li><li value="2"><b><strong>Auxiliary space: O(1),</strong></b><span> As no extra space is required.</span></li></ul>

```
class Solution{

    public:
    //Function to find the minimum number of platforms required at the
    //railway station such that no train waits.
    int findPlatform(int arr[], int dep[], int n)
    {
       // plat_needed indicates number of platforms
       // needed at a time
       int ans = 1;
    
       // Run a nested for-loop to find the overlap
       for (int i = 0; i < n; i++) {
    
           // Initially one platform is needed
           int temp = 1;
           for (int j = 0; j < n; j++) {
               if (i != j)
                   // Increment plat_needed when there is an
                   // overlap
                   if (arr[i] >= arr[j] && dep[j] >= arr[i])
                       temp++;
           }
    
           // Update the result
           ans = max(temp, ans);
       }
       return ans;
    }
};
```

## Greedy - Job Sequencing Problem
<div class="track_body__GeGQu"><strong>Problem</strong>: Given an array of jobs where every job has a deadline and associated profit if the job is finished before the deadline. It is also given that every job takes a single unit of time, so the minimum possible deadline for any job is 1. How to maximize total profit if only one job can be scheduled at a time.<br><br><strong>Examples:</strong><br><pre><strong>Input</strong>: Four Jobs with following deadlines and profits
  JobID    Deadline      Profit
    a        4            20   
    b        1            10
    c        1            40  
    d        1            30
<strong>Output</strong>: Following is maximum profit sequence of jobs
        c, a   

<strong>Input</strong>: Five Jobs with following deadlines and profits
   JobID     Deadline     Profit
     a         2           100
     b         1           19
     c         2           27
     d         1           25
     e         3           15
<strong>Output</strong>: Following is maximum profit sequence of jobs
        c, a, e

</pre><br><br><br>This is a standard Greedy Algorithm problem. Following is the greedy algorithm to solve the above problem:<br><pre>1) Sort all jobs in decreasing order of profit.
2) Initialize the result sequence as the first job in sorted jobs.
3) Do following for remaining n-1 jobs
.......a) If the current job can fit in the current result sequence 
          without missing the deadline, add the current job to the result.
          Else ignore the current job.

```
// C++ program to find the maximum profit 
// job sequence from a given array
// of jobs with deadlines and profits
#include<iostream>
#include<algorithm>
using namespace std;

// A structure to represent a job
struct Job
{
    char id; // Job Id
    int dead; // Deadline of job
    
    // Profit if job is over 
    // before or on deadline
    int profit; 
};

// This function is used for sorting all
// jobs according to profit
bool comparison(Job a, Job b)
{
    return (a.profit > b.profit);
}

// Returns minimum number of platforms reqquired
void printJobScheduling(Job arr[], int n)
{
    // Sort all jobs according to 
    // decreasing order of prfit
    sort(arr, arr+n, comparison);

    int result[n]; // To store result (Sequence of jobs)
    bool slot[n]; // To keep track of free time slots

    // Initialize all slots to be free
    for (int i=0; i<n; i++)
        slot[i] = false;

    // Iterate through all given jobs
    for (int i=0; i<n; i++)
    {
        // Find a free slot for this job 
        // (Note that we start
        // from the last possible slot)
        for (int j=min(n, arr[i].dead)-1; j>=0; j--)
        {
            // Free slot found
            if (slot[j]==false)
            {
                result[j] = i; // Add this job to result
                slot[j] = true; // Make this slot occupied
                break;
            }
        }
    }

    // Print the result
    for (int i=0; i<n; i++)
    if (slot[i])
        cout << arr[result[i]].id << " ";
}

// Driver Code
int main()
{
    Job arr[] = { {'a', 2, 100}, {'b', 1, 19}, {'c', 2, 27},
                {'d', 1, 25}, {'e', 3, 15}};
                
    int n = sizeof(arr)/sizeof(arr[0]);
    
    cout << "Following is maximum profit sequence of job : ";
    
    printJobScheduling(arr, n);
    
    return 0;
}
```

Output:</b><br><pre>Following is maximum profit sequence of job : c a e

</pre><br></div><br><br><strong>Time Complexity</strong> of the above solution is O(n<sup>2</sup>).</div>

## Greedy - 

