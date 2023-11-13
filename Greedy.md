## Table of Content
1. [Maximum Number of Events that Can be Attended](#greedy---maximum-number-of-events-that-can-be-attended)
2. [Minimum Platforms](#greedy---minimum-platforms)
3. [Job Sequencing Problem](#greedy---job-sequencing-problem)
4. [Fractional Knapsack](#greedy---fractional-knapsack)
5. [Coin Change](#greedy---coin-change)


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

## Go To
[Table of Content](#table-of-content)

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

## Go To
[Table of Content](#table-of-content)


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

## Go To
[Table of Content](#table-of-content)


## Greedy - Fractional Knapsack

<div class="problems_problem_content__Xm_eO"><p><span style="font-size:18px">Given <em>weights</em> and <em>values</em> of <strong>N</strong> items, we need to put these items in a knapsack of capacity <strong>W</strong> to get the <em>maximum</em> total value in the knapsack.<br>
<strong>Note:</strong> Unlike 0/1 knapsack, you are allowed to break&nbsp;the item.&nbsp;</span></p>

<p>&nbsp;</p>

<p><span style="font-size:18px"><strong>Example 1:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:
</strong>N = 3, W = 50
values[] = {60,100,120}
weight[] = {10,20,30}
<strong>Output:
</strong>240.00<strong>
Explanation:</strong>Total maximum value of item
we can have is 240.00 from the given
capacity of sack. 
</span></pre>

<p><span style="font-size:18px"><strong>Example 2:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:
</strong>N = 2, W = 50
values[] = {60,100}
weight[] = {10,20}
<strong>Output:
</strong>160.00<strong>
Explanation:
</strong>Total maximum value of item
we can have is 160.00 from the given
capacity of sack.</span></pre>

<p>&nbsp;</p>

<p><span style="font-size:18px"><strong>Your Task</strong> :<br>
Complete the function&nbsp;<em><strong>fractionalKnapsack</strong>()</em> that receives maximum capacity , array of structure/class&nbsp;and size n and returns a double value representing the maximum value in knapsack.<br>
<strong>Note:&nbsp;</strong>The details of structure/class is defined in the comments above the given function.</span></p>

<p><br>
<span style="font-size:18px"><strong>Expected Time Complexity</strong> : O(NlogN)<br>
<strong>Expected Auxilliary Space</strong>: O(1)</span></p>

<p><br>
<span style="font-size:18px"><strong>Constraints:</strong><br>
1 &lt;= N &lt;= 10<sup>5</sup><br>
1 &lt;= W &lt;= 10<sup>5</sup></span></p>
</div>

### Solution
<h3>Intuition</h3>
<p>The idea is to use <strong>greedy approach</strong>. The basic idea of the greedy approach is to calculate the ratio value/weight for each item and sort the item on the basis of this ratio. Then take the item with the highest ratio and add them until we can’t add the next item as a whole and at the end add the next item as much as we can.</p>
<h3>Example:</h3>
<blockquote><p><strong>Input:&nbsp;</strong><br><strong>Items as (value, weight) pairs&nbsp;</strong><br><strong>arr[] = {{100, 20}, {120, 30}, {60, 10}}&nbsp;</strong><br><strong>Knapsack Capacity, W = 50</strong></p><ul><li>After sorting arr based on ratio, we will get:<br>arr[] = {{60, 10}, {100, 20}, {120, 30}} as their ratios are 6.0 &gt;= 5.0 &gt;= 4.0 respectively.<br>We can add item1 and item2 fully, getting finalValue as 160 and curWeight as 30.<br>At item3, we are left with remaining weight of 50 - 30 which is 20, so we can't add it fully as it is having weight 30.<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; so we can simply add 20 by 30, which is 2/3 part of it, which will generate value 120*20/30 = 80.<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; finalValue becomes ( 160 + 80 ) which is 240.<br>Return 240 as answer.</li></ul></blockquote>
<h3>Implementation</h3>
<ul><li>Calculate the ratio(value/weight) for each item.</li><li>Sort all the items in decreasing order of the ratio.</li><li>Initialize curWeight(current weight we collected) and finalValue(it will be the final value generated with collected items) with 0.</li><li>Run a loop for i from 0 to N-1:&nbsp;<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Do the following for every item "i" in the sorted order:<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;<strong>case1)</strong> If the weight of the current item is less than or equal to the remaining capacity then&nbsp;<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; add the value of that item into the finalValue.<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; add the weight of that item into the curWeight.<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;<strong>case2)</strong> Else add the current item as much as we can and break out of the loop.<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Value generated by it will be (total value of that item)*(remaining weight we can add) / (total weight of that item).</li><li>Return finalValue.</li></ul>

```
class Solution
{
    public:
    //comparison function to sort items according to value/weight ratio.
    static bool cmp(Item a, Item b)
    {
        double r1 = (double)a.value / a.weight;
        double r2 = (double)b.value / b.weight;
        return r1 > r2;
    }
    
    
    public:
    //Function to get the maximum total value in the knapsack.
    double fractionalKnapsack(int W, Item arr[], int n)
    {
        
        //sorting items on basis of value/weight ratio.
        sort(arr, arr + n, cmp);
        
        //taking variable for current weight in knapsack.
        int curWeight = 0;
        double finalvalue = 0.0;
        
        //iterating over all the items.
        for (int i = 0; i < n; i++)
        {
            //if currweight + item's weight is less than or equal to W,
            //then we add the item's value to final value.
            if (curWeight + arr[i].weight <= W)
            {
                curWeight += arr[i].weight;
                finalvalue += arr[i].value;
            }
            //else we take the fraction of the that item's value 
            //based on the remaining weight in knapsack.
            else
            {
                int remain = W - curWeight;
                finalvalue += arr[i].value * ((double) remain / arr[i].weight);
                break;
            }
        }
        //returning final value.
        return finalvalue;
    }
};
```

<h3>Complexity</h3>
<p><strong>Time Complexity: O(N.log(N))</strong>, as we sorted the vectors of size N.<br><strong>Auxiliary Space: O(1)</strong>, as we are not using any extra space.</p>

## Go To
[Table of Content](#table-of-content)

## Greedy - Coin Change
<div class="elfjS" data-track-load="description_content"><p>You are given an integer array <code>coins</code> representing coins of different denominations and an integer <code>amount</code> representing a total amount of money.</p>

<p>Return <em>the fewest number of coins that you need to make up that amount</em>. If that amount of money cannot be made up by any combination of the coins, return <code>-1</code>.</p>

<p>You may assume that you have an infinite number of each kind of coin.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> coins = [1,2,5], amount = 11
<strong>Output:</strong> 3
<strong>Explanation:</strong> 11 = 5 + 5 + 1
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> coins = [2], amount = 3
<strong>Output:</strong> -1
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> coins = [1], amount = 0
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= coins.length &lt;= 12</code></li>
	<li><code>1 &lt;= coins[i] &lt;= 2<sup>31</sup> - 1</code></li>
	<li><code>0 &lt;= amount &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><ol>
<li>
<p>Let's start with the initialization. 2 points to note.</p>
<ul>
<li>
<p>Given <strong>no coins</strong>, it is impossible to make any amount you give me. Hence, initialized to <code>∞</code></p>
</li>
<li>
<p>Given <strong><code>amount</code> = 0</strong>, we don't need any coins at all. Hence, initialized to <code>0</code></p>
</li>
</ul>
</li>
</ol>
<p><img src="https://assets.leetcode.com/users/images/7a78ed23-6ab2-4712-93ff-068897ddec85_1593946439.0402143.png" alt="image"></p>
<ol start="2">
<li>
<p>Let's begin filling up the rest of the cells from [1, 1] onwards.</p>
</li>
<li>
<p>Let's do <strong>Cell [1,1]</strong> now. We ask ourselves</p>
<ul>
<li>
<p><strong>Which coin to look at, and which amount to look at?</strong></p>
</li>
<li>
<p><code>coin</code> : We look at the coin with value = 1 (in row 1)</p>
</li>
<li>
<p><code>amount</code>: We look at the amount with value = 1 (in col 1)</p>
</li>
<li>
<p>Can I use the coin with value <code>1</code>?</p>
</li>
</ul>
</li>
<li>
<p>Now, we ask ourselves</p>
<ul>
<li>
<p>Can I <strong>use</strong> this coin? <strong>YES</strong>, because its value (<code>1</code>) **&lt;= **my <em><strong>current</strong></em> <code>amount</code> --&gt; this gives us 1 + 0 = <code>1</code> coin</p>
</li>
<li>
<p>Can I <strong>NOT use</strong> this coin? YES, you can always choose not to use it. --&gt; this gives us <code>∞</code> coin</p>
</li>
<li>
<p>Choose the <strong>minimum / smaller</strong> of the 2 options --&gt; <code>1</code> coin</p>
</li>
</ul>
</li>
</ol>
<p><img src="https://assets.leetcode.com/users/images/5f832b9f-a9e1-4388-8869-46c2923c5b0d_1593946420.0466368.png" alt="image"></p>
<br>
<ol start="5">
<li>We repeat this for the entire row 1</li>
</ol>
<p><img src="https://assets.leetcode.com/users/images/3a6f7b7e-a6e5-44c3-8493-6225570927ad_1593946498.7684975.png" alt="image"></p>
<br>
<ol start="6">
<li>
<p>Let's look at <strong>Cell [2,1]</strong> next. We ask ourselves</p>
<ul>
<li>
<p>Can I <strong>use</strong> this coin? <strong>NO</strong>, because its value (<code>2</code>) ** &gt; **my <em><strong>current</strong></em> <code>amount</code></p>
</li>
<li>
<p>Okay, this means having this coin with value <code>2</code> is worthless to us</p>
</li>
<li>
<p>Hence, minimum coins needed at this cell = minimum coins needed in the top cell (I'm <strong>throwing</strong> the coin with value <code>2</code> away, and my <strong>amount remains unchanged</strong>).</p>
</li>
</ul>
</li>
</ol>
<br>
<p><img src="https://assets.leetcode.com/users/images/6596f859-4263-4333-a4e5-427ec60bbebf_1593946829.9951413.png" alt="image"></p>
<br>
<ol start="7">
<li>Work it out by hand, and see if you get the result.</li>
</ol>
<p><img src="https://assets.leetcode.com/users/images/962b960a-fe9c-4ecc-b2da-2266b9a63544_1593946888.9626093.png" alt="image"></p>
<br>

```
class Solution {
public:
  int coinChange(vector<int>& coins, int amount) {
    // EDGE CASE
    if (amount == 0) {
      return 0;
    }

    // INIT DIMENSIONS
    int nrows = coins.size() + 1;
    int ncols = amount + 1;

    // BY DEFAULT, 2^64 DENOTES IMPOSSIBLE TO MAKE CHANGE
    vector<vector<int>> dp(nrows, vector<int>(ncols, INT_MAX));

    // BY DEFAULT, IF AMOUNT = 0, WE NEED EXACTLY 0 COINS
    for (int i = 0; i < nrows; i++) {
      dp[i][0] = 0;
    }

    // OTHER CELLS
    for (int i = 1; i < nrows; i++) {
      for (int j = 1; j < ncols; j++) {
        // CASE 1 - WE MUST LEAVE THE COIN
        if (j < coins[i - 1]) {
          dp[i][j] = dp[i - 1][j];
        }

        // CASE 2 - WE CAN TAKE OR LEAVE THE COIN
        else {
          int take = 1 + dp[i][j - coins[i - 1]];
          int leave = dp[i - 1][j];
          dp[i][j] = min(take, leave);
        }
      }
    }

    return dp[-1][-1] == INT_MAX ? -1 : dp[-1][-1];
  }
};
```
## Go To
[Table of Content](#table-of-content)
