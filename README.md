# Boyer-Moore Voting Algorithm - Majority Element Finder

## Overview
The **Boyer-Moore Voting Algorithm** is an optimal approach used to find the **majority element** in a given array where an element appears **more than N/2 times**. The algorithm efficiently finds the majority element with **O(N) time complexity** and **O(1) space complexity**, making it highly efficient for large datasets.

---

## Dry Run Example
Consider the given array:
```cpp
arr[] = { 1, 1, 1, 1, 2, 3, 5 }
```
### **First Pass - Finding the Candidate**
| Index  | Element | Candidate | Votes |
|--------|---------|------------|--------|
| 0      | 1       | 1          | 1      |
| 1      | 1       | 1          | 2      |
| 2      | 1       | 1          | 3      |
| 3      | 1       | 1          | 4      |
| 4      | 2       | 1          | 3      |
| 5      | 3       | 1          | 2      |
| 6      | 5       | 1          | 1      |

After the **first traversal**, the candidate is `1`.

### **Second Pass - Validating Majority Element**
| Index  | Element | Count of Candidate `1` |
|--------|---------|----------------------|
| 0      | 1       | 1                    |
| 1      | 1       | 2                    |
| 2      | 1       | 3                    |
| 3      | 1       | 4                    |
| 4      | 2       | 4                    |
| 5      | 3       | 4                    |
| 6      | 5       | 4                    |

Since `1` appears **4 times**, and `4 > 7/2 = 3.5`, it is the **majority element**.

---

## Algorithm
1. **First pass:** Find a **candidate element** by iterating through the array and using a voting mechanism.
   - If `votes == 0`, pick the current element as a candidate.
   - If the current element matches the candidate, increase votes.
   - If it does not match, decrease votes.
2. **Second pass:** Verify if the candidate appears more than `N/2` times in the array.
3. **Return the candidate** if it satisfies the majority condition; otherwise, return `-1`.

---

## C++ Implementation
```cpp
#include <iostream>
using namespace std;

// Function to find majority element
int findMajority(int arr[], int n) {
    int candidate = -1, votes = 0;
    
    // Finding majority candidate
    for (int i = 0; i < n; i++) {
        if (votes == 0) {
            candidate = arr[i];
            votes = 1;
        } else {
            votes += (arr[i] == candidate) ? 1 : -1;
        }
    }
    
    // Verifying the candidate
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] == candidate) count++;
    }
    
    return (count > n / 2) ? candidate : -1;
}

int main() {
    int arr[] = { 1, 1, 1, 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int majority = findMajority(arr, n);
    cout << "The majority element is: " << majority;
    return 0;
}
```

---

## Complexity Analysis
- **Time Complexity:** `O(N)` (Two linear passes)
- **Space Complexity:** `O(1)` (Only a few integer variables are used)

---

## Applications
- **Elections & Voting Systems**: To find the winning candidate.
- **Data Stream Processing**: Quickly identifying frequent elements.
- **Stock Market Analysis**: Detecting dominant trends in stock prices.

---

## Conclusion
The **Boyer-Moore Voting Algorithm** is an elegant and efficient way to determine the majority element in an array. It is widely used due to its **linear runtime** and **constant space usage**.


