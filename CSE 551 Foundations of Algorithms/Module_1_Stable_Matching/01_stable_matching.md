# Module 1 Stable Matching

In module 1, we will explore **algorithms**, why they matter, and how they help solve problems. We’ll focus on the **Stable Matching Problem**, learning the right algorithmic techniques to solve it and how to evaluate those solutions. You will also get a quick introduction to **five key problems**: **Interval Scheduling**, **Weighted Interval Scheduling**, **Bipartite Matching**, **Independent Set**, and **Competitive Facility Location**.

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
### Example
Given four individuals (A, B, C, D) and their ranked preferences, determine whether a stable roommate assignment exists.

## Gale-Shapley Algorithm
The **Gale-Shapley Algorithm** (also called the "Propose-and-Reject" algorithm) is a method to find a stable matching.

### How It Works:
1. Start with all participants unmatched.
2. While there is an unmatched man:
   - The man proposes to the highest-ranked woman on his preference list who hasn’t rejected him.
   - If the woman is unmatched, she accepts.
   - If the woman is matched but prefers the new proposer over her current partner, she switches to the new proposer.
   - Otherwise, she rejects the proposal.
3. Repeat until everyone is matched.

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
