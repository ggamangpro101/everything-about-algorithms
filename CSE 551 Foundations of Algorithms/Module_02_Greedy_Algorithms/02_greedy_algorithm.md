# Module 2 Greedy Algorithm

In Module 2, we will learn about Greedy Algorithms. The algorithms covered include Interval Scheduling, Interval Partitioning, Minimum Lateness Scheduling, Optimal Offline Caching, Shortest Path, Minimum Spanning Trees, and Clustering.

## Contents

1. [Interval Scheduling](#Interval-Scheduling)
2. [Scheduling to Minimize Lateness](#Scheduling-to-Minimize-Lateness)
3. [Optimal Offline Caching](Optimal-Offline-Caching)
4. [Further Examples of Greedy Algorithms](Further-Examples-of-Greedy-Algorithms)

## Interval Scheduling
- **Concept:** Interval scheduling is a problem where we are given a set of jobs with their start and finish times.  
- **Goal:** To find the maximum subset of mutually compatible jobs—meaning jobs that do not overlap.  
- **Key Idea:** A job j starts at $\ s_j $ and finishes at $\ f_j $. Two jobs are **compatible** if their time intervals **do not overlap**.  
- **Example:** The given jobs (labeled as 'a' to 'h') are represented as horizontal bars on a timeline.  
- **Optimal Solution (OPT):** The selected subset of jobs is B, E, H, as they form the largest set of non-overlapping intervals.  
- **Observation:** The smallest job (C) is not in any optimal solution, and the job that starts first (A) is also not included.  

<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_001.png" width=60%, height=60%/>
</p>

### Interval Scheduling: Greedy Algorithm Template
- **Greedy Strategy:** The greedy algorithm considers jobs in some order and takes each job only if it is compatible with the ones already taken.
- **Different Ordering Approaches:**
  - **Earliest Start Time:** Pick jobs in ascending order of start times ($\ s_j $).
  - **Earliest Finish Time:** Pick jobs in ascending order of finish times ($\ f_j $).
  - **Shortest Interval:** Pick jobs with the shortest duration ($\ f_j−s_j $).
  - **Fewest Conflicts:** Pick jobs that have the least number of conflicts (overlaps) with other jobs.

### Visual Representation of Greedy Algorithms
**Illustration:**  

**Breaks Earliest Start Time:** The first approach (earliest start time) can lead to conflicts as jobs that start early may overlap with many others.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_012.png" width=60%, height=60%/>
</p>

**Breaks Shortest Interval:** Choosing the shortest jobs may lead to missing a better overall selection.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_013.png" width=60%, height=60%/>
</p>

**Breaks Fewest Conflicts:** Prioritizing jobs with the fewest conflicts can sometimes lead to suboptimal results.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_014.png" width=60%, height=60%/>
</p>

### Greedy Algorithm for Interval Scheduling
- **Approach:** The best greedy strategy is to select jobs based on **earliest finish time**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_015.png" width=60%, height=60%/>

- **Time Complexity:** O(nlogn), since sorting takes O(nlogn) and iterating through the jobs takes O(n).
- **Compatibility Check:** A job j is compatible if its start time is greater than or equal to the finish time of the last added job.


## Scheduling to Minimize Lateness

## Optimal Offline Caching

## Further Examples of Greedy Algorithms
