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
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_001.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_001.png" width=45%, height=50%/>
</p>

**Q.** Is assignment **Alex-Grace**, **Bob-Megan** and **David-Eemily** stable?
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_002.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_002.png" width=45%, height=50%/>
</p>

**A.** No, because Alex and Megan will hook up.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_003.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_003.png" width=45%, height=50%/>
</p>

**Q.** Is assignment **Alex-Emily**, **Bob-Megan** and **David-Grace** stable?
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Mens_Pref_List_004.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Womens_Pref_List_004.png" width=45%, height=50%/>
</p>

**A.** Yes, they are stable.

## Stable Roomate Problem
**Stable Roommate Problem** is a variation of the Stable Matching Problem, where 2n individuals need to be paired into roommate pairs. Unlike the Stable Matching Problem, where stability can always be guaranteed, stable matchings do not always exist in this scenario.

**Q: Do stable matchings always exist?**  
**A: Not always.**

Unlike the Stable Matching Problem, where a stable matching always exists, the Stable Roommate Problem does not guarantee a stable matching.
### Example
Given four individuals (Alex, Bob, Chris, David) and their ranked preferences, determine whether a stable roommate assignment exists.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_001.png" width=50%, height=50%/>
</p>

- **Paring 1**: **Alex-Bob** and **Chris-David**  
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_002.png" width=50%, height=50%/>
</p>

**Instability**: Bob prefers Chris over Alex. Chris prefer Bob over David. Bob and Chris both prefer each other over their assigned roommates (Alex and David). So, this is **Unstable**.

- **Paring 2**: **Alex-Chris** and **Bob-David**  
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_003.png" width=50%, height=50%/>
</p>

**Instability**: Alex prefers Bob over Chris. Bob prefer Alex over David. Alex and Bob both prefer each other over their assigned roommates (Chris and David). So, this is **Unstable**.

- **Paring 3**: **Alex-David** and **Bob-Chris**  
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Roommate_Pref_List_004.png" width=50%, height=50%/>
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
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_001.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_001.png" width=45%, height=50%/>
</p>

- **Alex** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_002.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_002.png" width=45%, height=50%/>  
</p>

- **Bella** accepts **Alex** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_003.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_003.png" width=45%, height=50%/>  
</p>

- **Bob** propses to **Diana**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_004.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_004.png" width=45%, height=50%/>  
</p>

- **Diana** accepts **Bob** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_005.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_005.png" width=45%, height=50%/>  
</p>

- **Chris** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_006.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_006.png" width=45%, height=50%/>  
</p>

- **Bella** rejects **Alex** and accepts **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_007.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_007.png" width=45%, height=50%/>  
</p>

- **Alex** propses to **Amy**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_008.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_008.png" width=45%, height=50%/>  
</p>

- **Amy** accepts **Alex** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_009.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_009.png" width=45%, height=50%/>  
</p>

- **David** propses to **Amy**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_010.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_010.png" width=45%, height=50%/>  
</p>

- **Amy** rejects **David** because she prefers **Alex**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_011.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_011.png" width=45%, height=50%/>  
</p>

- **David** propses to **Diana**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_012.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_012.png" width=45%, height=50%/>  
</p>

- **Diana** rejects **Bob** and accepts **David**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_013.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_013.png" width=45%, height=50%/>  
</p>

- **Bob** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_014.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_014.png" width=45%, height=50%/>  
</p>

- **Bella** rejects **Bob** because she prefers **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_015.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_015.png" width=45%, height=50%/>  
</p>

- **Bob** propses to **Amy**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_016.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_016.png" width=45%, height=50%/>  
</p>

- **Amy** rejects **Bob** because she prefers **Alex**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_017.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_017.png" width=45%, height=50%/>  
</p>

- **Bob** propses to **Caitlin**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_018.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_018.png" width=45%, height=50%/>  
</p>

- **Caitlin** accepts **Bob** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_019.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_019.png" width=45%, height=50%/>  
</p>

- **Eric** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_020.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_020.png" width=45%, height=50%/>  
</p>

- **Bella** rejects **Eric** because she prefers **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_021.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_021.png" width=45%, height=50%/>  
</p>

- **Eric** propses to **Diana**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_022.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_022.png" width=45%, height=50%/>  
</p>

- **Diana** rejects **David** because she prefers **Eric**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_023.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_023.png" width=45%, height=50%/>  
</p>

- **David** propses to **Caitlin**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_024.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_024.png" width=45%, height=50%/>  
</p>

- **Caitlin** rejects **David** because she prefers **Bob**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_025.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_025.png" width=45%, height=50%/>  
</p>

- **David** propses to **Bella**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_026.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_026.png" width=45%, height=50%/>  
</p>

- **Bella** rejects **David** because she prefers **Chris**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_027.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_027.png" width=45%, height=50%/>  
</p>

- **David** propses to **Emily**.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_028.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_028.png" width=45%, height=50%/>  
</p>

- **Emily** accepts **David** because she was not previously matched.
<p align=center>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Men_029.png" width=45%, height=50%/>
<img src="https://github.com/ggamangpro101/everything-about-algorithms/blob/master/CSE%20551%20Foundations%20of%20Algorithms/Module_1_Stable_Matching/png/Gale_Shapley_Women_029.png" width=45%, height=50%/>  
</p>

- Now, **everyone is matched**, and the result is a **stable matching**.


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
