### EX3 Implementation of GSP Algorithm In Python
### DATE: 06-02-2026
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>

## Program:

```
from collections import defaultdict
from itertools import combinations

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    c = defaultdict(int)
    for seq in dataset:
        # flatten into list of items (your version mixes strings/lists)
        flat_seq = []
        for itemset in seq:
            if isinstance(itemset, str):
                flat_seq.extend(itemset.split(','))   # split commas
            else:
                flat_seq.extend(itemset)
        # ensure uniqueness per sequence
        for comb in set(combinations(sorted(flat_seq), k)):
            c[comb] += 1
    # collect all frequent patterns
    res = {}
    for item, support in c.items():
        if support >= min_support:
            res[item] = support
    return res

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1
    fp = defaultdict(int)
    seq=dataset
    while True:
        c = generate_candidates(seq, k)
        if not c:
            break
        fp.update(c)
        k += 1
    return fp

# Example dataset for each category
dataset= [
    [["a"],["b"],["c"],["b","e"],["c","f"],["g"],["a","b","e"]],
    [["a"],["d"],["b","c"],["c"],["f","g"],["c","h"]],
    [["b"],["c"],["a","d"],["e"],["b"],["f"],["c","d","f","g","h"]],
    [["c"],["e","c"],["e","h"]]
]

# Minimum support threshold
min_support = 3


# Perform GSP algorithm for each category
dataset_result = gsp(dataset, min_support)


# Output the frequent sequential patterns for each category
print("Frequent Sequential Patterns --> dataset:")
if dataset_result:
    for pattern, support in dataset_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in dataset.")
```
### Output:

<img width="1915" height="797" alt="Screenshot 2026-02-07 130839" src="https://github.com/user-attachments/assets/4ecdbe9c-8202-450c-960c-3a5ca642da7b" />


### Visualization:
```
# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')
```
### Output:

<img width="1140" height="569" alt="5432" src="https://github.com/user-attachments/assets/7e71482c-745a-4fe5-bc98-625432ee7b9e" />


### Result:
Thus the implementation of the GSP algorithm in python has been successfully executed.
