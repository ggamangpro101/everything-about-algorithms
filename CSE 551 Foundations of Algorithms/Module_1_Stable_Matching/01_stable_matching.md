# Module 1 Stable Matching

**Stable matching** is a concept from algorithms and game theory. It’s about pairing people or groups in a way that respects their **preferences**, so everyone ends up in a stable arrangement where no two participants would rather be matched with each other than their current matches.

## Key Terms
- **Stable Matching:** A pairing where there are no two participants (e.g., a man and a woman, or a student and a school) who would both prefer to be matched with each other over their current partners.
- **Unstable Pair:** A pair of participants who both prefer each other over their current matches. If such a pair exists, the matching is considered unstable.
- **Perfect Matching:** A pairing where every participant is matched to exactly one partner.

## Problem Definition
The **Stable Matching Problem** is defined as:
- **Input:** Two groups of participants (e.g., men and women), each with a preference list ranking members of the opposite group.
- **Output:** A stable matching, if one exists.

### Example
Let’s say there are 3 men (\(A, B, C\)) and 3 women (\(X, Y, Z\)), and their preferences are:

- **Men's Preferences:**
  - \(A: [X, Y, Z]\)
  - \(B: [Y, X, Z]\)
  - \(C: [Z, X, Y]\)

- **Women's Preferences:**
  - \(X: [B, A, C]\)
  - \(Y: [A, C, B]\)
  - \(Z: [C, B, A]\)

A possible **stable matching**:
- \(A-Y, B-X, C-Z\)

This pairing is stable because no man and woman prefer each other over their assigned partners.

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
