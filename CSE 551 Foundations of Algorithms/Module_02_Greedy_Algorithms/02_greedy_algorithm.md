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
- **Key Idea:** A job j starts at $\ s_j$ and finishes at $\ f_j$. Two jobs are **compatible** if their time intervals **do not overlap**.  
- **Example:** The given jobs (labeled as 'a' to 'h') are represented as horizontal bars on a timeline.  
- **Optimal Solution (OPT):** The selected subset of jobs is B, E, H, as they form the largest set of non-overlapping intervals.  
- **Observation:** The smallest job (C) is not in any optimal solution, and the job that starts first (A) is also not included.  

<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_001.png" width=60%, height=60%/>
</p>

### Interval Scheduling: Greedy Algorithm Template
- **Greedy Strategy:** The greedy algorithm considers jobs in some order and takes each job only if it is compatible with the ones already taken.
- **Different Ordering Approaches:**
  - **Earliest Start Time:** Pick jobs in ascending order of start times ($\ s_j$).
  - **Earliest Finish Time:** Pick jobs in ascending order of finish times ($\ f_j$).
  - **Shortest Interval:** Pick jobs with the shortest duration ($\ f_j−s_j$).
  - **Fewest Conflicts:** Pick jobs that have the least number of conflicts (overlaps) with other jobs.

### Visual Representation of Greedy Algorithms
**Illustration:**  

**Breaks Earliest Start Time:** The first approach (earliest start time) can lead to conflicts as jobs that start early may overlap with many others.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_002.png" width=70%, height=70%/>
</p>

**Breaks Shortest Interval:** Choosing the shortest jobs may lead to missing a better overall selection.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_002-1.png" width=70%, height=70%/>
</p>

**Breaks Fewest Conflicts:** Prioritizing jobs with the fewest conflicts can sometimes lead to suboptimal results.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_002-2.png" width=70%, height=70%/>
</p>

### Greedy Algorithm for Interval Scheduling
- **Approach:** The best greedy strategy is to select jobs based on **earliest finish time**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_015.png" width=70%, height=70%/>

- **Time Complexity:** O(nlogn), since sorting takes O(nlogn) and iterating through the jobs takes O(n).
- **Compatibility Check:** A job j is compatible if its start time is greater than or equal to the finish time of the last added job.

### Interval Scheduling Demo
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_003.png" width=70%, height=70%/>
  
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_004.png" width=70%, height=70%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_005.png" width=70%, height=70%/>

<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_006.png" width=70%, height=70%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_007.png" width=70%, height=70%/>

<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_008.png" width=70%, height=70%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_009.png" width=70%, height=70%/>

<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_010.png" width=70%, height=70%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_011.png" width=70%, height=70%/>
</p>

### Interval Scheduling Analysis - Greedy Algorithm is Optimal(최적)
- **Key Idea:** Proving the Greedy Algorithm is Optimal  
This slide introduces a proof by contradiction to show that the greedy algorithm is optimal for the interval scheduling problem.

- **Step-by-Step Breakdown**
  - Assume the Greedy Algorithm is **NOT Optimal**
    We assume that there is a better solution (an optimal solution) than the one produced by the greedy algorithm.

  - Define the Jobs Selected by the Algorithms
    Let i₁, i₂, ..., iₖ be the jobs selected by the greedy algorithm.
    Let j₁, j₂, ..., jₘ be the jobs selected by the optimal solution.

  - Compare the Two Solutions
    The proof assumes that both solutions start similarly:
      The first r jobs are identical:
      - $\ i_1$ = $\ j_1 $
      - $\ i_2$ = $\ j_2 $
      - $\ i_3$ = $\ j_3 $
      
      where r is the largest possible number of common jobs between the greedy and optimal solutions.

- Introducing the Contradiction
  - The greedy algorithm selects job $\ i_{r+1}$ which finishes **before** $\ j_{r+1}$  
  ​- Since $\ i_{r+1}$ finishes before $\ j_{r+1}$, it means that replacing $\ j_{r+1}$ with $\ i_{r+1}$ still produces a valid schedule.  
  - This implies that the optimal solution could have used the greedy choice without losing optimality, contradicting our assumption that the greedy algorithm was suboptimal.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_016.png" width=70%, height=70%/>

- **Conclusion**  
Since we reached a contradiction, the **greedy algorithm must be optimal**.

### **Continuation of the Proof - Contradiction Completes the Proof**
- **Same Assumption and Setup**
  - The proof setup remains the same, where we assumed that the greedy algorithm is not optimal.
- **Finalizing the Contradiction**
  - Since job $\ i_{r+1}$ finishes before $\ j_{r+1}$, replacing $\ j_{r+1}$ with $\ i_{r+1}$ still maintains a valid and feasible solution.
  - The new solution contains at least as many jobs as the optimal one, meaning the greedy algorithm is at least as good as the optimal solution.
  - This contradicts the assumption that the greedy solution is suboptimal.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_02_Greedy_Algorithms/png/Interval_Scheduling_016.png" width=70%, height=70%/>

**Conclusion**  
  - The greedy algorithm always produces an optimal solution.
  - Greedy choice property holds, meaning making the locally optimal choice at each step leads to a globally optimal solution.

## Scheduling to Minimize Lateness

## Optimal Offline Caching

## Further Examples of Greedy Algorithms
