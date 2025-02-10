# Module 1 Stable Matching

In Module 1, we will explore **algorithms**, why they matter, and how they help solve problems. We’ll focus on the **Stable Matching Problem**, learning the right algorithmic techniques to solve it and how to evaluate those solutions. You will also get a quick introduction to **five key problems**: **Interval Scheduling**, **Weighted Interval Scheduling**, **Bipartite Matching**, **Independent Set**, and **Competitive Facility Location**.

## Key Terms
- **Perfect matching** means that everyone is paired up in a one-to-one relationship, with no one left unmatched. Each person has exactly one partner.
- **Stability** in a matching means that no two people have a reason to abandon their assigned partners for each other. If a pair—let’s call them A and B—both prefer each other over their current matches, they might choose to leave their assigned partners and form a new pair, disrupting the existing arrangement. This situation is called instability.
- **Stable matching** ensures that no such dissatisfied pairs exist. It guarantees that within the given preferences, every person is matched in a way where no two individuals would rather be with each other than their assigned partners.
- **Unstable matching** happens when two people like each other more than their current partners. If this happens, they might leave their matches to be together, making the matching unstable.
- **Stable matching problem** is about finding such a pairing using the preference lists of **n** men and **n** women, ensuring that the final match has no unstable pairs that could lead to switching.

## Stable Matching Problem
The **Stable Matching Problem** involves finding a stable pairing between two equally sized groups, where each member has a ranked preference list. The goal is to ensure that no two individuals would prefer each other over their assigned partners. This concept can be demonstrated through various examples.

### Example
Given three men **(Alex, Bob, David)** and three women **(Emily, Megan, Grace)**, along with their preference lists, determine a **stable matching** where no two individuals prefer each other over their assigned partners.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_001.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_001.png" width=45%, height=45%/>
</p>

**Q:** Is assignment **Alex-Grace**, **Bob-Megan** and **David-Eemily** stable?
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_002.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_002.png" width=45%, height=45%/>
</p>

**A:** No, because Alex and Megan will hook up.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_003.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_003.png" width=45%, height=45%/>
</p>

**Q:** Is assignment **Alex-Emily**, **Bob-Megan** and **David-Grace** stable?
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_004.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_004.png" width=45%, height=45%/>
</p>

**A:** Yes, they are stable.

## Stable Roomate Problem
**Stable Roommate Problem** is a variation of the Stable Matching Problem, where 2n individuals need to be paired into roommate pairs. Unlike the Stable Matching Problem, where stability can always be guaranteed, stable matchings do not always exist in this scenario.

**Q: Do stable matchings always exist?**  
**A: Not always.**

Unlike the Stable Matching Problem, where a stable matching always exists, the Stable Roommate Problem does not guarantee a stable matching.
### Example
Given four individuals (**Alex, Bob, Chris, David**) and their ranked preferences, determine whether a stable roommate assignment exists.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_001.png" width=40%, height=40%/>
</p>

- **Paring 1**: **Alex-Bob** and **Chris-David**  
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_002.png" width=40%, height=40%/>
</p>

**Instability**: Bob prefers Chris over Alex. Chris prefer Bob over David. Bob and Chris both prefer each other over their assigned roommates (Alex and David). So, this is **Unstable**.

- **Paring 2**: **Alex-Chris** and **Bob-David**  
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_003.png" width=40%, height=40%/>
</p>

**Instability**: Alex prefers Bob over Chris. Bob prefer Alex over David. Alex and Bob both prefer each other over their assigned roommates (Chris and David). So, this is **Unstable**.

- **Paring 3**: **Alex-David** and **Bob-Chris**  
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_004.png" width=40%, height=40%/>
</p>

**Instability**: Alex prefers Chris over David. Chris prefer Alex over Bob. Alex and Chris both prefer each other over their assigned roommates (David and Bob). So, this is **Unstable**.

**Conclusion:**  
Every possible pairing leads to instability, meaning no stable matching exists for this set of preferences.

**Observation**  
Stable matchings **do not always exist** for the **Stable Roommate Problem**.
Unlike the Stable Matching Problem, the inherent preferences in the roommate setup can create situations where stability is impossible, as shown in the example.

## Propose and Reject Algorithm (Gale-Shapley)
The **Propose-and-Reject Algorithm (Gale-Shapley, 1962)** is a simple and logical method designed to ensure a stable matching between two groups.
```python
Initialize each person to be free.
while (some man is free and has not prposed to every woman) {
     Choose such a man m
     w = 1st woman on m's list to whom m has not yet proposed
     if (w is free)
        assign m and w to be engaged
     else if (w prefers m to her fiancé m')
        assign m and w to be engaged, and m' to be free
     else
        w rejects m
}
```
### Gale-Shapley Algorithm
The **Gale-Shapley Algorithm** (also called the "Propose-and-Reject" algorithm) is a method to find a stable matching. This method is still widely used today to **assign residents to hospitals**, highlighting its effectiveness and practicality as a solution.

### How It Works:
1. Start with all participants unmatched.
2. While there is an unmatched man:
   - The man proposes to the highest-ranked woman on his preference list who hasn’t rejected him.
   - If the woman is unmatched, she accepts.
   - If the woman is matched but prefers the new proposer over her current partner, she switches to the new proposer.
   - Otherwise, she rejects the proposal.
3. Repeat until everyone is matched.

### Example
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_001.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_001.png" width=45%, height=45%/>
</p>

- **Alex** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_002.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_002.png" width=45%, height=45%/>  
</p>

- **Bella** accepts **Alex** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_003.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_003.png" width=45%, height=45%/>  
</p>

- **Bob** propses to **Diana**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_004.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_004.png" width=45%, height=45%/>  
</p>

- **Diana** accepts **Bob** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_005.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_005.png" width=45%, height=45%/>  
</p>

- **Chris** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_006.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_006.png" width=45%, height=45%/>  
</p>

- **Bella** rejects **Alex** and accepts **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_007.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_007.png" width=45%, height=45%/>  
</p>

- **Alex** propses to **Amy**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_008.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_008.png" width=45%, height=45%/>  
</p>

- **Amy** accepts **Alex** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_009.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_009.png" width=45%, height=45%/>  
</p>

- **David** propses to **Amy**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_010.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_010.png" width=45%, height=45%/>  
</p>

- **Amy** rejects **David** because she prefers **Alex**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_011.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_011.png" width=45%, height=45%/>  
</p>

- **David** propses to **Diana**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_012.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_012.png" width=45%, height=45%/>  
</p>

- **Diana** rejects **Bob** and accepts **David**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_013.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_013.png" width=45%, height=45%/>  
</p>

- **Bob** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_014.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_014.png" width=45%, height=45%/>  
</p>

- **Bella** rejects **Bob** because she prefers **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_015.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_015.png" width=45%, height=45%/>  
</p>

- **Bob** propses to **Amy**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_016.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_016.png" width=45%, height=45%/>  
</p>

- **Amy** rejects **Bob** because she prefers **Alex**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_017.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_017.png" width=45%, height=45%/>  
</p>

- **Bob** propses to **Caitlin**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_018.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_018.png" width=45%, height=45%/>  
</p>

- **Caitlin** accepts **Bob** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_019.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_019.png" width=45%, height=45%/>  
</p>

- **Eric** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_020.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_020.png" width=45%, height=45%/>  
</p>

- **Bella** rejects **Eric** because she prefers **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_021.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_021.png" width=45%, height=45%/>  
</p>

- **Eric** propses to **Diana**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_022.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_022.png" width=45%, height=45%/>  
</p>

- **Diana** rejects **David** because she prefers **Eric**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_023.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_023.png" width=45%, height=45%/>  
</p>

- **David** propses to **Caitlin**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_024.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_024.png" width=45%, height=45%/>  
</p>

- **Caitlin** rejects **David** because she prefers **Bob**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_025.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_025.png" width=45%, height=45%/>  
</p>

- **David** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_026.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_026.png" width=45%, height=45%/>  
</p>

- **Bella** rejects **David** because she prefers **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_027.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_027.png" width=45%, height=45%/>  
</p>

- **David** propses to **Emily**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_028.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_028.png" width=45%, height=45%/>  
</p>

- **Emily** accepts **David** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_029.png" width=45%, height=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_029.png" width=45%, height=45%/>  
</p>

- Now, **everyone is matched**, and the result is a **stable matching**.

### Proof of Correctness: Termination
- **Observation 1**: Men propose to women in decreasing order of their preference lists. This ensures that men systematically move through their preferences without skipping anyone.
- **Observation 2**: Once a woman is matched, she never becomes unmatched but may "trade up" to a more preferred proposer. This guarantees progress toward stability.
- **Claim**: The algorithm terminates after at most **n²** iterations of the while loop.
- **Proof**: Each man proposes to a new woman each time, and there are at most **n²** possible proposals (**n men × n women**).
     - This ensures the algorithm is efficient and terminates in finite time.

### Proof of Correctness: Perfection
- **Claim**: All men and women get matched.
- **Proof (by contradiction)**:
     - **Assume a man, say Eric, is unmatched at the end of the algorithm.**
          - This is the opposite of the claim (that everyone is matched).
          - If Eric is unmatched, it means the algorithm couldn't find a partner for him.
     - **If Eric is unmatched, then some woman, say Amy, must also be unmatched.**
          - The algorithm pairs each man with one woman, so if Zeus is unmatched, there must be an unmatched woman as well.
     - **Observation 2: Amy was never proposed to during the process.**
          - If **Amy** is **unmatched**, it means no man ever proposed to her, because if she had been proposed to, she would have accepted the best proposal.
     - **However, Eric, being unmatched, would have proposed to all women, including Amy.**
          - Eric would have worked his way down his entire preference list, proposing to every woman, because the algorithm requires men to propose to every woman until they are matched or until no women are left to propose to.
          - This means Eric must have proposed to Amy at some point.
     - **Contradiction**:
          - If Eric proposed to Amy, she should not be unmatched because she would have accepted him if she had no other proposals.
          - This contradicts the earlier assumption that Amy is unmatched.

### Proof of Correctness: Stability
- **Claim**: No unstable pairs exist in the final matching.
     - An unstable pair exists if two individuals (let's call them Amy and Eric) both prefer each other over their assigned partners. The proof aims to show that no such pair can exist.
- **Proof (by contradiction)**:
     - **Assume there is an unstable pair, Amy and Eric.**
          - Both Amy and Eric prefer each other over their current partners in the matching.
          - This violates the stability condition, so we proceed to check the possible scenarios.
     - **Case 1: Eric never proposed to Amy.**
          - If Eric never proposed to Amy, it means that Eric must have preferred his current partner over Amy.
          - This is because men propose in decreasing order of preference, so if Eric skipped Amy, it was intentional.
          - This directly contradicts the assumption that Eric prefers Amy over his current partner.
          - Therefore, the pair Amy and Eric cannot be unstable in this case.
     - **Case 2: Eric proposed to Amy.**
          - If Eric did propose to Amy, Amy must have rejected Eric either immediately or later in favor of a better match.
          - The Gale-Shapley algorithm ensures that once a woman is matched, she only "trades up" (moves to a partner she prefers more).
          - This means Amy prefers her current partner over Eric.
          - This also contradicts the assumption that Amy prefers Eric over her current partner.
     - In both scenarios, the pair Amy and Eric is not unstable.
     - This disproves the assumption that an unstable pair exists in the final matching.
  
Since the assumption of instability leads to contradictions in all cases, it proves that **no unstable pairs exist**. Therefore, the **Gale-Shapley algorithm guarantees a stable matching** where all pairs follow the stability rules.

### Summary
- **Stable Matching Problem**: The task is to find a stable matching between two groups of size n, ensuring no unstable 
  pairs exist.
- **Gale-Shapley Algorithm**: Guarantees to find a stable matching for any instance of the problem in **O(n²)** time.
- **Questions**:  
     **Q:** How can the Gale-Shapley algorithm be implemented efficiently in terms of computation?  
       
     **Q:** If multiple stable matchings exist, which one does the algorithm produce?  

### Efficient Implementation of Gale-Shapley Algorithm
- **Representation**: Men and women are indexed from 1 to n.
- **Engagement Tracking**:
     - Maintain a list of free men (queue or stack can be used).
     - Use arrays (wife[m] and husband[w]) to track who is engaged to whom. If a person is unmatched, the entry is 0.
- **Proposal Management**:
     - Each man has a list of women ranked by preference.
     - Use an array (count[m]) to track the number of proposals a man has made.
- **Efficiency Insight**: The naive implementation can lead to **O(n³)** complexity, but using structured data, we achieve **O(n²)**
- **Women Rejecting/Accepting**
     - **Acceptance Criteria**:
          - Each woman decides whether to accept a man’s proposal by comparing him to her current partner.
     - **Optimization**:
          - Precompute an "inverse preference list" for each woman, mapping each man to his rank in her list. This allows constant-time checks during comparisons.
     - **Example**:
          - A preference list for Amy is given, and its inverse is shown. Using this, we see that Amy prefers **Man 3** over **Man 6** because inverse[3]<inverse[6].  
          - Using the **preference list**: You'd need to find 3 and 6 in the list, which takes **O(n)** time.  
          - Using the **inverse list**: Simply compare inverse[3] and inverse[6] (constant time lookup for both).      
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Amy_Pref_Inverse.png" height=70%, width=70%/>
</p>

```python
for i = 1 to n
   inverse[pref[i]] = i
```

### Understanding the solution(Multiple Stable Matchings)
**Q:** Does Gale-Shapley always produce the same stable matching, and if not, which one does it find?  

**Observation:**  
- There can be multiple stable matchings.  
- Example instance: Two stable matchings are shown where pairs differ slightly.  
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Multiple_Stable_Matching_003.png" height=45%, width=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Multiple_Stable_Matching_004.png" height=45%, width=45%/>

<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Multiple_Stable_Matching_005.png" height=45%, width=45%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Multiple_Stable_Matching_006.png" height=45%, width=45%/>
</p>

**Key Insight:** Gale-Shapley finds the man-optimal stable matching when men propose.

### Python Example:
```python
def gale_shapley(men_prefs, women_prefs):
    free_men = list(men_prefs.keys())
    engaged = {}
    women_ranks = {
        woman: {man: rank for rank, man in enumerate(prefs)}
        for woman, prefs in women_prefs.items()
    }
    proposals = {man: 0 for man in men_prefs}

    while free_men:
        man = free_men.pop(0)
        woman = men_prefs[man][proposals[man]]
        proposals[man] += 1

        if woman not in engaged:
            engaged[woman] = man
        else:
            current_man = engaged[woman]
            if women_ranks[woman][man] < women_ranks[woman][current_man]:
                engaged[woman] = man
                free_men.append(current_man)
            else:
                free_men.append(man)

    return {man: woman for woman, man in engaged.items()}

# Example Usage
men_preferences = {
    "A": ["X", "Y", "Z"],
    "B": ["Y", "X", "Z"],
    "C": ["Z", "X", "Y"],
}
women_preferences = {
    "X": ["B", "A", "C"],
    "Y": ["A", "C", "B"],
    "Z": ["C", "B", "A"],
}
result = gale_shapley(men_preferences, women_preferences)
print("Stable Matching:", result)
```

**1. Termination:**
The algorithm always terminates because men propose in decreasing order of preference, and there are a finite number of proposals (n^2, where n is the number of participants).

**2. Perfect Matching:**
Every participant is eventually matched because proposals continue until all participants are paired.

**3. Stability:**
No unstable pairs exist because a woman only trades up during the algorithm, and a man cannot pair with a woman who has rejected him.

**Applications**
Stable matching has many real-world applications:

- **Resident-Hospital Matching:** Assigning medical residents to hospitals.
- **College Admissions:** Matching students to universities based on preferences.
- **Job Recruitment:** Matching candidates to jobs or companies.

**Summary**
- The Gale-Shapley Algorithm guarantees a stable matching in O(n^2) time.
- The resulting matching is man-optimal: Each man is paired with the best possible partner they could achieve in any stable matching.
- This comes at the expense of woman-pessimality: Each woman is paired with their worst valid partner.

Stable matching is a foundational problem in algorithms, demonstrating how preferences and fairness can be balanced in a mathematically sound way.
