
## 🧩 **1. Selection Sort**

### 📝 Problem / Objective

Sort an array by repeatedly finding the minimum element (for ascending order) from the unsorted part and putting it at the beginning.

### 💡 Intuition

You divide the array into two parts:

* **Sorted** (left part)
* **Unsorted** (right part)

In each iteration, find the **smallest element** in the unsorted part and **swap** it with the first element of the unsorted part.

### 🔍 Step-by-step Process

For array `[29, 10, 14, 37, 14]`

* Pass 1: Find min → 10 → swap with 29 → `[10, 29, 14, 37, 14]`
* Pass 2: Find min from index 1 → 14 → swap with 29 → `[10, 14, 29, 37, 14]`
* Pass 3: Find min from index 2 → 14 → swap with 29 → `[10, 14, 14, 37, 29]`
* Pass 4: Find min from index 3 → 29 → swap with 37 → `[10, 14, 14, 29, 37]`

✅ Final sorted array: `[10, 14, 14, 29, 37]`

### ⚙️ Algorithm (Pseudo/Java)

```java
void selectionSort(int arr[]) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex])
                minIndex = j;
        }
        int temp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = temp;
    }
}
```

### ⏱️ Complexity

* Time: **O(n²)** — always (best, avg, worst same)
* Space: **O(1)** — in-place
* Stability: ❌ Not stable

### 💭 Key Takeaways

* Easy to understand but inefficient for large data.
* Fewer swaps compared to Bubble Sort.
* Good when memory writes are costly.

---

## 🫧 **2. Bubble Sort**

### 📝 Problem / Objective

Repeatedly compare adjacent elements and swap them if they are in the wrong order. The largest element “bubbles up” to the end of the array each pass.

### 💡 Intuition

Like bubbles rising to the top — the largest element gets pushed to the end in each pass.

### 🔍 Step-by-step Process

For `[5, 3, 8, 4, 2]`

* Pass 1: Compare & swap → `[3, 5, 4, 2, 8]`
* Pass 2: `[3, 4, 2, 5, 8]`
* Pass 3: `[3, 2, 4, 5, 8]`
* Pass 4: `[2, 3, 4, 5, 8]`

✅ Sorted: `[2, 3, 4, 5, 8]`

### ⚙️ Algorithm

```java
void bubbleSort(int arr[]) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        boolean swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        if (!swapped) break; // optimization
    }
}
```

### ⏱️ Complexity

* Best: **O(n)** (already sorted, with optimization)
* Average: **O(n²)**
* Worst: **O(n²)**
* Space: **O(1)**
* Stability: ✅ Stable

### 💭 Key Takeaways

* Very simple but inefficient for large arrays.
* Optimization using the `swapped` flag is important.
* Good for small datasets or teaching purposes.

---

## 🧠 **3. Insertion Sort**

### 📝 Problem / Objective

Builds the sorted array one element at a time by inserting each element into its correct position among previously sorted elements.

### 💡 Intuition

Like sorting playing cards in your hands — you pick one card and place it in the right position among the sorted ones.

### 🔍 Step-by-step Process

For `[5, 3, 4, 1, 2]`

* Start with 2nd element (3): insert before 5 → `[3, 5, 4, 1, 2]`
* Next element (4): insert between 3 and 5 → `[3, 4, 5, 1, 2]`
* Next (1): insert at start → `[1, 3, 4, 5, 2]`
* Next (2): insert after 1 → `[1, 2, 3, 4, 5]`

✅ Sorted: `[1, 2, 3, 4, 5]`

### ⚙️ Algorithm

```java
static void insertion_sort(int[] arr, int n) {
    for (int i = 0; i <= n - 1; i++) {   // iterate over each element
        int j = i;
        while (j > 0 && arr[j - 1] > arr[j]) {  // move backward
            int temp = arr[j - 1];              // swap if out of order
            arr[j - 1] = arr[j];
            arr[j] = temp;
            j--;                                // continue moving left
        }
    }
}

```

### ⏱️ Complexity

* Best: **O(n)** (already sorted)
* Average: **O(n²)**
* Worst: **O(n²)**
* Space: **O(1)**
* Stability: ✅ Stable

### 💭 Key Takeaways

* Efficient for small or nearly sorted arrays.
* Used in hybrid algorithms like **TimSort** (used in Python & Java).
* Good for online sorting (sorting as elements come).

---

## ⚖️ Comparison Table

| Algorithm      | Best Case | Average Case | Worst Case | Space | Stable | When to Use                  |
| -------------- | --------- | ------------ | ---------- | ----- | ------ | ---------------------------- |
| Selection Sort | O(n²)     | O(n²)        | O(n²)      | O(1)  | ❌ No   | Few swaps needed             |
| Bubble Sort    | O(n)      | O(n²)        | O(n²)      | O(1)  | ✅ Yes  | Simple implementation        |
| Insertion Sort | O(n)      | O(n²)        | O(n²)      | O(1)  | ✅ Yes  | Small / nearly sorted arrays |

# 🧩 **4. Merge Sort**

---

### 🧾 **Problem / Objective**

Sort an array using the **Divide and Conquer** approach — split the array into halves, sort each half recursively, and then merge them back in sorted order.

---

### 💡 **Core Intuition**

Instead of trying to sort the whole array at once:

1. **Divide** → Split the array into two halves.
2. **Conquer** → Recursively sort both halves.
3. **Combine** → Merge the two sorted halves into one sorted array.

This ensures that we’re always merging **already sorted** lists.

---

### ⚙️ **Code Explanation**

```java
public void mergeSort(int[] arr, int low, int high) {
    if (low >= high) return; // Base condition: single element is sorted

    int mid = (low + high) / 2;

    // Sort left half
    mergeSort(arr, low, mid);

    // Sort right half
    mergeSort(arr, mid + 1, high);

    // Merge both halves
    merge(arr, low, mid, high);
}
```

#### 🔹 Merge Function

```java
public void merge(int[] arr, int low, int mid, int high) {
    List<Integer> temp = new ArrayList<>();
    int left = low, right = mid + 1;

    // Merge sorted halves
    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) temp.add(arr[left++]);
        else temp.add(arr[right++]);
    }

    // Copy remaining elements
    while (left <= mid) temp.add(arr[left++]);
    while (right <= high) temp.add(arr[right++]);

    // Copy back to original array
    for (int i = low; i <= high; i++)
        arr[i] = temp.get(i - low);
}
```

---

### 🔍 **Dry Run Example**

**Input:** `[38, 27, 43, 3, 9, 82, 10]`

1️⃣ Split → `[38, 27, 43]` and `[3, 9, 82, 10]`
2️⃣ Further divide → `[38] [27, 43]` and `[3, 9] [82, 10]`
3️⃣ Merge small parts:

* `[27, 43] → [27, 43]`
* `[82, 10] → [10, 82]`
  4️⃣ Merge next level:
* `[38] + [27, 43] → [27, 38, 43]`
* `[3, 9] + [10, 82] → [3, 9, 10, 82]`
  5️⃣ Final merge → `[27, 38, 43] + [3, 9, 10, 82]` → `[3, 9, 10, 27, 38, 43, 82]`

✅ Sorted array: `[3, 9, 10, 27, 38, 43, 82]`

---

### ⏱️ **Complexity Analysis**

| Case    | Time Complexity | Explanation                                  |
| ------- | --------------- | -------------------------------------------- |
| Best    | **O(n log n)**  | Always splits equally and merges efficiently |
| Average | **O(n log n)**  | Consistent divide & merge                    |
| Worst   | **O(n log n)**  | Still same — not input dependent             |

🔹 **Space Complexity:** O(n) (temporary array used in merge)
🔹 **Stable:** ✅ Yes
🔹 **In-place:** ❌ No (uses extra space)

---

### 🧭 **Key Takeaways**

* Works well for large datasets.
* Guaranteed O(n log n).
* Stable sorting algorithm.
* Used in external sorting (like files or linked lists).

---

# ⚡ **5. Quick Sort**

---

### 🧾 **Problem / Objective**

Sort an array using the **Divide and Conquer** technique by partitioning around a **pivot** element — elements smaller go to the left, larger go to the right.

---

### 💡 **Intuition**

Instead of merging like Merge Sort, Quick Sort:

1. **Chooses a pivot** (often last element).
2. **Partitions** the array so that:

   * All elements smaller than pivot are on the left.
   * All greater are on the right.
3. **Recursively sorts** both halves.

It works **in-place**, making it memory efficient.

---

### ⚙️ **Code Explanation**

```java
public void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int pivotIndex = partition(arr, low, high);
        quickSort(arr, low, pivotIndex - 1);
        quickSort(arr, pivotIndex + 1, high);
    }
}
```

#### 🔹 Partition Function

```java
private int partition(int[] arr, int low, int high) {
    int pivot = arr[high]; // choose pivot
    int i = low - 1;       // boundary for smaller elements

    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) { // element smaller than pivot
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }

    // place pivot in correct position
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;

    return i + 1; // return pivot index
}
```

---

### 🔍 **Dry Run Example**

**Input:** `[10, 7, 8, 9, 11, 5]`
**Pivot:** 5

1️⃣ Partition step:

* Compare each element with pivot (5).
* All > 5 → no swaps.
* Place pivot at correct position → `[5, 7, 8, 9, 11, 10]`
  Pivot index = 0

2️⃣ Left part = `[]`, Right part = `[7, 8, 9, 11, 10]`
Recurse → choose pivot 10, partition again → `[7, 8, 9, 10, 11]`

✅ Final sorted array: `[5, 7, 8, 9, 10, 11]`

---

### ⏱️ **Complexity Analysis**

| Case        | Time Complexity | Explanation                                                    |
| ----------- | --------------- | -------------------------------------------------------------- |
| **Best**    | **O(n log n)**  | Pivot divides array evenly                                     |
| **Average** | **O(n log n)**  | Random pivot — typical case                                    |
| **Worst**   | **O(n²)**       | When pivot is smallest/largest every time (e.g., sorted input) |

🔹 **Space Complexity:** O(log n) (recursive stack)
🔹 **Stable:** ❌ No
🔹 **In-place:** ✅ Yes

---

### ⚖️ **Merge Sort vs Quick Sort**

| Feature      | **Merge Sort**                 | **Quick Sort**          |
| ------------ | ------------------------------ | ----------------------- |
| Approach     | Divide & Merge                 | Divide & Partition      |
| Worst Case   | O(n log n)                     | O(n²)                   |
| Average Case | O(n log n)                     | O(n log n)              |
| Space        | O(n)                           | O(log n)                |
| Stability    | ✅ Stable                       | ❌ Not stable            |
| In-place     | ❌ No                           | ✅ Yes                   |
| Usage        | Linked lists, external sorting | Arrays, internal memory |

---

### 🧭 **Key Takeaways**

* **Quick Sort** is faster in practice for arrays due to better cache locality.
* **Merge Sort** is more predictable with guaranteed O(n log n).
* Many languages use a **hybrid approach** (like Java’s Dual-Pivot QuickSort or Python’s TimSort).

## 🧩 **1. Largest Element in an Array**

### 💡 Intuition

Scan the array and keep track of the **maximum** element found so far.

### ⚙️ Code

```java
int largestElement(int[] arr) {
    int max = arr[0];
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    return max;
}
```

### 🧮 Dry Run

`arr = [5, 9, 3, 15, 2]`

* Start `max = 5`
* Compare each → final `max = 15`

✅ Output → `15`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 **2. Second Largest Element (Without Sorting)**

### 💡 Intuition

We find the **largest** and **second largest** in one pass using comparison.

### ⚙️ Code

```java
int secondLargest(int[] arr) {
    int largest = Integer.MIN_VALUE;
    int second = Integer.MIN_VALUE;

    for (int num : arr) {
        if (num > largest) {
            second = largest;
            largest = num;
        } else if (num > second && num != largest) {
            second = num;
        }
    }
    return second;
}
```

### 🧮 Dry Run

`arr = [5, 9, 3, 15, 2]`

* largest=15, second=9
  ✅ Output → `9`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 **3. Check if Array is Sorted**

### 💡 Intuition

For ascending order, check if each element ≤ next one.

### ⚙️ Code

```java
boolean isSorted(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] < arr[i - 1])
            return false;
    }
    return true;
}
```

### 🧮 Dry Run

`[1, 2, 3, 4, 5] → true`
`[1, 3, 2] → false`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 **4. Remove Duplicates from Sorted Array**

### 💡 Intuition

Use **two pointers** — one for the position of the next unique element.

### ⚙️ Code

```java
int removeDuplicates(int[] arr) {
    int i = 0;
    for (int j = 1; j < arr.length; j++) {
        if (arr[j] != arr[i]) {
            i++;
            arr[i] = arr[j];
        }
    }
    return i + 1; // length of unique part
}
```

### 🧮 Dry Run

`[1,1,2,2,3]` → `[1,2,3]`, returns `3`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 **5. Left Rotate Array by One Place**

### 💡 Intuition

Store first element, shift all elements left by one, place first element at the end.

### ⚙️ Code

```java
void leftRotateByOne(int[] arr) {
    int first = arr[0];
    for (int i = 1; i < arr.length; i++) {
        arr[i - 1] = arr[i];
    }
    arr[arr.length - 1] = first;
}
```

### 🧮 Dry Run

`[1,2,3,4,5] → [2,3,4,5,1]`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 **6. Left Rotate Array by D Places**

### 💡 Intuition

Rotate array D times → or reverse parts smartly using the **reversal algorithm**.

### ⚙️ Code (Reversal method)

```java
void rotateLeft(int[] arr, int d) {
    int n = arr.length;
    d = d % n; // handle d > n
    reverse(arr, 0, d - 1);
    reverse(arr, d, n - 1);
    reverse(arr, 0, n - 1);
}

void reverse(int[] arr, int start, int end) {
    while (start < end) {
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
}
```

### 🧮 Example

`[1,2,3,4,5,6,7], d=2`
→ `[3,4,5,6,7,1,2]`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 **7. Move All Zeros to End**

### 💡 Intuition

Use a pointer to track where the next non-zero should go.

### ⚙️ Code

```java
void moveZeros(int[] arr) {
    int j = 0;
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] != 0) {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            j++;
        }
    }
}
```

### 🧮 Dry Run

`[0,1,0,3,12] → [1,3,12,0,0]`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 **8. Linear Search**

### 💡 Intuition

Check each element until you find the target.

### ⚙️ Code

```java
int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target)
            return i;
    }
    return -1;
}
```

### 🧮 Example

`arr = [4,2,1,7,9], target = 7` → Output: index `3`

### ⏱️ Complexity

* Time: O(n)
* Space: O(1)

---

## 🧩 1️⃣ Maximum Consecutive Ones

### ✅ Problem Statement

Given a binary array (`nums` containing 0s and 1s), find the **maximum number of consecutive 1s** present in the array.

---

### 💡 Intuition

We need to count continuous sequences of `1`s and track the **longest streak**.
Whenever a `0` appears, the current streak ends.

---

### 🧠 Approach

1. Maintain two counters:

   * `count`: keeps track of the current number of consecutive 1s.
   * `ans`: stores the **maximum** value of `count` so far.
2. Traverse through the array:

   * If the current element is `1`, increment `count` and update `ans`.
   * If it’s `0`, reset `count` to `0`.
3. Finally, return `ans`.

---

### 🧾 Code

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int count = 0;
        int ans = 0;
        for (int n : nums) {
            if (n == 1) {
                count++;
                ans = Math.max(ans, count);
            } else {
                count = 0;
            }
        }
        return ans;
    }
}
```

---

### 🧮 Dry Run

Input: `[1, 1, 0, 1, 1, 1]`

| Step | n | count | ans | Action    |
| ---- | - | ----- | --- | --------- |
| 1    | 1 | 1     | 1   | Increment |
| 2    | 1 | 2     | 2   | Increment |
| 3    | 0 | 0     | 2   | Reset     |
| 4    | 1 | 1     | 2   | Increment |
| 5    | 1 | 2     | 2   | Increment |
| 6    | 1 | 3     | 3   | Increment |

✅ Output → `3`

---

### ⏱️ Time Complexity

**O(n)** — single pass through the array.

### 💾 Space Complexity

**O(1)** — no extra space used.

---

### 🧩 Key Takeaways

* Classic example of **sliding counting logic**.
* Good starter problem for **array traversal patterns**.

---

## 🧩 2️⃣ Single Number (Every element appears twice except one)

### ✅ Problem Statement

Given an array of integers where every element appears **twice except one**, find that single element.

---

### 💡 Intuition

We can use a **HashSet** to track duplicates:

* Add each number if not seen.
* If seen again, remove it.
  After the loop, the **remaining number** in the set is the single one.

---

### 🧠 Approach

1. Create a `HashSet<Integer>`.
2. Traverse the array:

   * If the number is in the set → remove it.
   * Else → add it.
3. The only remaining number in the set is the **unique** one.

---

### 🧾 Code

```java
import java.util.*;

class Solution {
    public int singleNumber(int[] arr) {
        Set<Integer> set = new HashSet<>();
        for (int n : arr) {
            if (set.contains(n))
                set.remove(n);
            else
                set.add(n);
        }
        return set.iterator().next();
    }
}
```

---

### 🧮 Dry Run

Input: `[2, 2, 1]`

| Step | n | Set | Action |
| ---- | - | --- | ------ |
| 1    | 2 | [2] | Add    |
| 2    | 2 | []  | Remove |
| 3    | 1 | [1] | Add    |

✅ Output → `1`

---

### ⏱️ Time Complexity

**O(n)** — single traversal.

### 💾 Space Complexity

**O(n)** — HashSet may store up to `n/2 + 1` elements.

---

### ⚡ Optimized Approach (Bit Manipulation)

We can find the single number using **XOR**:

```java
int res = 0;
for (int n : arr)
    res ^= n;
return res;
```

⏱️ O(n), 💾 O(1)

Because XOR cancels out identical numbers (`x ^ x = 0`), leaving only the single element.

---

### 🧩 Key Takeaways

* XOR is an elegant way to solve such problems.
* HashSet is easier to understand, but XOR is more optimized.

---

## 🧩 3️⃣ Longest Subarray with Sum = K (Positive Numbers Only)

### ✅ Problem Statement

Given an array of positive integers `a[]` and an integer `k`, find the **length of the longest subarray** whose elements sum up to `k`.

---

### 💡 Intuition

Try all possible subarrays and check their sum.
Though brute force, it helps us understand the logic before optimizing (like prefix sum + hashmap).

---

### 🧠 Approach

1. Use two nested loops:

   * Outer loop `i` → start index of subarray.
   * Inner loop `j` → end index of subarray.
2. Keep a running sum `s` for each subarray.
3. If `s == k`, update `len = max(len, j - i + 1)`.

---

### 🧾 Code

```java
class SortAlgo {
    public static int getLongestSubarray(int[] a, int k) {
        int n = a.length;
        int len = 0;
        for (int i = 0; i < n; i++) {
            int s = 0;
            for (int j = i; j < n; j++) {
                s += a[j];
                if (s == k)
                    len = Math.max(len, j - i + 1);
            }
        }
        return len;
    }

    public static void main(String[] args) {
        int[] a = {2, 1, 1, 1};
        int k = 5;
        int len = getLongestSubarray(a, k);
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

### 🧮 Dry Run

Input: `[2, 1, 1, 1]`, `k = 5`

| i | j | Subarray  | Sum | len       |
| - | - | --------- | --- | --------- |
| 0 | 0 | [2]       | 2   | 0         |
| 0 | 1 | [2,1]     | 3   | 0         |
| 0 | 2 | [2,1,1]   | 4   | 0         |
| 0 | 3 | [2,1,1,1] | 5   | ✅ len = 4 |

✅ Output → `4`

---

### ⏱️ Time Complexity

**O(n²)** — two nested loops.

### 💾 Space Complexity

**O(1)** — no extra space.

---

### ⚡ Optimized Approach (Prefix Sum + Map)

Use a HashMap to store `(sum, index)` pairs → reduces time to **O(n)**.
(We can cover this when you move to “Longest subarray with sum K — positives + negatives.”)

---

### 🧩 Key Takeaways

* A clear example of **brute-force subarray enumeration**.
* Leads to optimized approaches using **hashmaps and prefix sums**.

---

## 🧩 4️⃣ **Two Sum Problem**

### ✅ Problem Statement

Given an integer array `nums` and an integer `target`,
return *the indices* of the **two numbers** such that they add up to the `target`.

You may assume that **each input has exactly one solution**,
and you may **not use the same element twice**.

---

### 💡 Intuition

We need to find two numbers in the array whose sum equals the target.

The brute-force way is simple:

* Try every possible pair `(i, j)`
* Check if `nums[i] + nums[j] == target`
* If yes → return their indices

---

### 🧠 Approach (Brute Force)

1. Use two nested loops:

   * Outer loop picks the **first number**.
   * Inner loop checks for another number that, when added to the first, equals the target.
2. As soon as we find such a pair, return their indices.

---

### 🧾 Code

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] == target - nums[i]) {
                    return new int[] { i, j };
                }
            }
        }
        // If no pair found (problem guarantees one solution)
        return null;
    }
}
```

---

### 🧮 Dry Run

Input:
`nums = [2, 7, 11, 15]`, `target = 9`

| i | j | nums[i] | nums[j] | target - nums[i] | Match? | Result        |
| - | - | ------- | ------- | ---------------- | ------ | ------------- |
| 0 | 1 | 2       | 7       | 7                | ✅      | Return [0, 1] |

✅ Output → `[0, 1]`

Explanation: `nums[0] + nums[1] = 2 + 7 = 9`

---

### ⏱️ Time Complexity

* **O(n²)** → double loop through the array.
  (Each element is compared with all others once.)
* Fine for small arrays, but inefficient for large inputs.

### 💾 Space Complexity

* **O(1)** → uses constant extra space.

---

### ⚡ Optimized Approach (Using HashMap)

We can solve this in **O(n)** using a **HashMap**:

**Logic:**

* Store numbers as we iterate.
* For each element, check if `(target - current)` exists in the map.
* If yes → return indices.

**Code:**

```java
import java.util.HashMap;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i);
        }
        return null;
    }
}
```

**⏱️ Time Complexity:** O(n)
**💾 Space Complexity:** O(n)

---

### 🧩 Key Takeaways

* Great example of improving from **O(n²)** → **O(n)** using HashMap.
* The pattern is used in many problems involving **pair sums** or **prefix sums**.
* Helps in understanding **space–time tradeoff**:
  using extra memory (HashMap) reduces runtime drastically.

## 🧩 5️⃣ **Sort Colors (Dutch National Flag Problem)**

### ✅ Problem Statement

Given an array `arr` containing only `0`, `1`, and `2`,
sort the array **in-place** so that all `0`s come first,
followed by all `1`s, and then all `2`s.

You must not use any sorting library or extra array — only constant space.

---

### 💡 Intuition

This is known as the **Dutch National Flag Problem**, invented by **Edsger Dijkstra**.

We can think of the array as divided into **three partitions**:

* **Left region** → all 0s
* **Middle region** → all 1s
* **Right region** → all 2s

We’ll use **three pointers** to keep track of these regions and sort in a single pass.

---

### 🧠 Approach (Three Pointer Technique)

1. Initialize three pointers:

   * `low = 0` → boundary for 0s
   * `mid = 0` → current element being checked
   * `high = n - 1` → boundary for 2s

2. Traverse while `mid <= high`:

   * If `arr[mid] == 0`:
     → Swap `arr[low]` and `arr[mid]`, increment both `low` and `mid`.
   * If `arr[mid] == 1`:
     → Move `mid` ahead (already in correct position).
   * If `arr[mid] == 2`:
     → Swap `arr[mid]` and `arr[high]`, decrement `high` (don’t increment `mid` yet, recheck the swapped value).

---

### 🧾 Code

```java
class Solution {
    public void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public void sortColors(int[] arr) {
        int n = arr.length;
        int low = 0, mid = 0, high = n - 1;

        while (mid <= high) {
            if (arr[mid] == 0) {
                swap(arr, low, mid);
                low++;
                mid++;
            } 
            else if (arr[mid] == 1) {
                mid++;
            } 
            else { // arr[mid] == 2
                swap(arr, mid, high);
                high--;
            }
        }
    }
}
```

---

### 🧮 Dry Run

Input: `[2, 0, 2, 1, 1, 0]`

| low | mid | high | arr[mid] | Action                       | Array after step     |
| --- | --- | ---- | -------- | ---------------------------- | -------------------- |
| 0   | 0   | 5    | 2        | swap(mid, high), high--      | `[0, 0, 2, 1, 1, 2]` |
| 0   | 0   | 4    | 0        | swap(low, mid), low++, mid++ | `[0, 0, 2, 1, 1, 2]` |
| 1   | 1   | 4    | 0        | swap(low, mid), low++, mid++ | `[0, 0, 2, 1, 1, 2]` |
| 2   | 2   | 4    | 2        | swap(mid, high), high--      | `[0, 0, 1, 1, 2, 2]` |
| 2   | 2   | 3    | 1        | mid++                        | `[0, 0, 1, 1, 2, 2]` |
| 2   | 3   | 3    | 1        | mid++                        | `[0, 0, 1, 1, 2, 2]` |
| 2   | 4   | 3    | —        | stop (mid > high)            | ✅ Sorted             |

✅ Final Output → `[0, 0, 1, 1, 2, 2]`

---

### ⏱️ Time Complexity

**O(n)** — each element is visited at most once.

### 💾 Space Complexity

**O(1)** — constant extra space.

---

### ⚡ Alternate (Counting Approach)

We can count the number of 0s, 1s, and 2s, and then rewrite the array —
but that requires **two passes**, whereas the Dutch Flag algorithm is **one-pass** and in-place.

---

### 🧩 Key Takeaways

* This is the **classic partitioning algorithm** — foundation for QuickSort and many array segregation problems.
* Uses **three pointers** efficiently — no extra memory, single traversal.
* Practice helps in mastering pointer manipulation and condition management.

## 🧩 6️⃣ **Majority Element (> n/2 times)**

---

### ✅ Problem Statement

Given an array `nums[]` of size `n`,
find the element that appears **more than n/2 times**.

If no such element exists, return `-1`.

---

### 💡 Intuition

If an element occurs **more than n/2 times**,
it will always be the **majority element** —
which means it will “cancel out” all other elements in voting comparison.

This gives rise to the **Moore’s Voting Algorithm**,
a clever way to find the potential candidate in **O(n)** time and **O(1)** space.

---

### 🧠 Approach (Moore’s Voting Algorithm)

1. **Step 1 – Find a candidate**

   * Initialize `count = 0` and `el = 0`.
   * Traverse the array:

     * If `count == 0`, pick the current element as the new candidate.
     * If the current element equals `el`, increment `count`.
     * Otherwise, decrement `count`.
   * After the loop, `el` will hold the **potential majority element**.

2. **Step 2 – Verify**

   * Count the occurrences of `el` in the array.
   * If it appears more than `n/2` times, return it.
   * Else, return `-1`.

---

### 🧾 Code

```java
import java.util.Arrays;

class Solution {
    public int majorityElement(int[] nums) {
        int n = nums.length;
        int count = 0;
        int el = 0;

        // Step 1: Find candidate
        for (int i = 0; i < n; i++) {
            if (count == 0) {
                el = nums[i];
                count = 1;
            } 
            else if (nums[i] == el) {
                count++;
            } 
            else {
                count--;
            }
        }

        // Step 2: Verify candidate
        count = 0;
        for (int num : nums) {
            if (num == el) count++;
        }

        if (count > n / 2) return el;
        return -1;
    }
}
```

---

### 🧮 Dry Run

Input: `[2, 2, 1, 1, 1, 2, 2]`

| i | nums[i] | el | count | Action         |
| - | ------- | -- | ----- | -------------- |
| 0 | 2       | 2  | 1     | pick new el    |
| 1 | 2       | 2  | 2     | increment      |
| 2 | 1       | 2  | 1     | decrement      |
| 3 | 1       | 2  | 0     | decrement to 0 |
| 4 | 1       | 1  | 1     | new candidate  |
| 5 | 2       | 1  | 0     | decrement      |
| 6 | 2       | 2  | 1     | new candidate  |

Candidate = `2`
Verification → Count(2) = 4 > 7/2 → ✅ Output = `2`

---

### ⏱️ Time Complexity

* **O(n)** → single pass to find candidate, one more pass to verify

### 💾 Space Complexity

* **O(1)** → constant extra space

---

### 🧩 Key Takeaways

* **Moore’s Voting Algorithm** works beautifully for > n/2 majority.
* Uses **cancel-out** logic efficiently.
* Foundation for the next version: **> n/3 majority elements**.

---

## 🧩 7️⃣ **Majority Elements (> n/3 times)**

---

### ✅ Problem Statement

Given an integer array `nums[]`,
find all elements that appear **more than n/3 times**.

There can be **at most two such elements**.

---

### 💡 Intuition

* If we need elements occurring more than `n/3` times,
  then there can be at most **2** majority elements.
* Extend the **Moore’s Voting Algorithm** to handle two candidates.

---

### 🧠 Approach

1. Maintain two potential candidates:

   * `el1`, `el2` and their respective counts `count1`, `count2`.
2. Traverse the array:

   * If `nums[i] == el1`, increment `count1`.
   * Else if `nums[i] == el2`, increment `count2`.
   * Else if `count1 == 0`, assign `nums[i]` to `el1`.
   * Else if `count2 == 0`, assign `nums[i]` to `el2`.
   * Otherwise, decrement both counts.
3. After traversal, verify both candidates by counting occurrences.
4. Add to the result list if they appear more than `n/3` times.

---

### 🧾 Code

```java
import java.util.*;

class Solution {
    public List<Integer> majorityElement(int[] nums) {
        int n = nums.length;
        int count1 = 0, count2 = 0;
        int el1 = Integer.MIN_VALUE, el2 = Integer.MIN_VALUE;

        // Step 1: Find potential candidates
        for (int num : nums) {
            if (num == el1) count1++;
            else if (num == el2) count2++;
            else if (count1 == 0) {
                el1 = num;
                count1 = 1;
            } 
            else if (count2 == 0) {
                el2 = num;
                count2 = 1;
            } 
            else {
                count1--;
                count2--;
            }
        }

        // Step 2: Verify candidates
        count1 = 0;
        count2 = 0;
        for (int num : nums) {
            if (num == el1) count1++;
            else if (num == el2) count2++;
        }

        List<Integer> result = new ArrayList<>();
        if (count1 > n / 3) result.add(el1);
        if (count2 > n / 3) result.add(el2);

        return result;
    }
}
```

---

### 🧮 Dry Run

Input: `[3, 2, 3]`, `n = 3`

| num | el1 | el2 | count1 | count2 | Action        |
| --- | --- | --- | ------ | ------ | ------------- |
| 3   | 3   | -   | 1      | 0      | new el1       |
| 2   | 3   | 2   | 1      | 1      | new el2       |
| 3   | 3   | 2   | 2      | 1      | increment el1 |

Verify:
Count(3) = 2, Count(2) = 1
→ n/3 = 1
✅ Output → `[3]`

---

### ⏱️ Time Complexity

* **O(n)** → One pass for candidate selection, one for verification.

### 💾 Space Complexity

* **O(1)** → Only fixed variables used.

---

### 🧩 Key Takeaways

* **Moore’s Voting Algorithm (extended)** can handle `n/3` majority elements.
* Works on the principle that at most `k−1` elements can appear more than `n/k` times.
* Excellent problem to master **count-based pattern logic**.

---
## 🧩 **Problem: Maximum Subarray Sum**

### 🔹 Problem Statement:

Given an integer array `nums`, find the **contiguous subarray (containing at least one number)** that has the **largest sum**, and return its sum.

**Example:**

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

---

## 💡 **Intuition / Core Idea**

When you move through the array:

* At each index `i`, you can **either continue** the current subarray or **start a new subarray** at `i`.
* The decision depends on whether adding the current element improves or worsens the sum.

So, for each element:

```
sum = max(nums[i], sum + nums[i])
```

If continuing the previous subarray makes the sum smaller than starting fresh, **start a new subarray**.

---

## 🧠 **Algorithm (Kadane’s Logic)**

1. Initialize:

   * `maxSum = nums[0]` → stores the maximum subarray sum found so far.
   * `sum = nums[0]` → stores the current subarray sum.

2. Traverse from index `1` to `n-1`:

   * At each step:

     * Update `sum = max(nums[i], sum + nums[i])`
       → decide whether to include `nums[i]` in current subarray or start a new one.
     * Update `maxSum = max(maxSum, sum)`
       → keep track of the global maximum.

3. Return `maxSum`.

---

## 🧩 **Code Implementation**

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int maxSum = nums[0];
        int sum = nums[0];
        for (int i = 1; i < n; i++) {
            sum = Math.max(nums[i], sum + nums[i]);
            maxSum = Math.max(maxSum, sum);
        }
        return maxSum;
    }
}
```

---

## 🧮 **Dry Run Example**

**Input:** `nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]`

| i | nums[i] | sum (max(nums[i], sum+nums[i])) | maxSum |
| - | ------- | ------------------------------- | ------ |
| 0 | -2      | -2                              | -2     |
| 1 | 1       | max(1, -2+1) = 1                | 1      |
| 2 | -3      | max(-3, 1-3) = -2               | 1      |
| 3 | 4       | max(4, -2+4) = 4                | 4      |
| 4 | -1      | max(-1, 4-1) = 3                | 4      |
| 5 | 2       | max(2, 3+2) = 5                 | 5      |
| 6 | 1       | max(1, 5+1) = 6                 | 6 ✅    |
| 7 | -5      | max(-5, 6-5) = 1                | 6      |
| 8 | 4       | max(4, 1+4) = 5                 | 6      |

**Answer:** `6`
**Subarray:** `[4, -1, 2, 1]`

---

## ⏱️ **Complexity Analysis**

* **Time Complexity:** O(n) — single pass through the array
* **Space Complexity:** O(1) — constant extra space

---

## ✨ **Key Takeaways**

* Kadane’s algorithm is a **Dynamic Programming** approach.
* Works by **local optimization** — each step decides whether to continue or restart.
* Handles **negative numbers** gracefully.
* Can be extended to find:

  * The actual subarray (store start & end indices)
  * Circular subarray maximum
  * 2D Kadane (maximum sum rectangle)


# 🧩 Stock Buy and Sell Problems (Kadane’s Variations)

---

## 🧠 1️⃣ **Best Time to Buy and Sell Stock (Single Transaction)**

**(LeetCode 121)**

### 🔹 Problem Statement

You are given an array `arr[]` where each element represents the stock price on that day.
Find the **maximum profit** you can achieve from **a single buy and a single sell**.

You must buy before you sell.

**Example:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy at 1, sell at 6.
```

---

### 💡 Intuition

We need to buy at the **lowest price** and sell at the **highest price after that**.
So, for each price:

* Track the **minimum price so far**.
* Compute the **profit** if you sell today.
* Keep track of the **maximum profit** seen so far.

---

### 🧩 Code

```java
class Solution {
    static int maxProfit(int[] arr) {
        int maxProfit = 0;
        int minPrice = Integer.MAX_VALUE;
        for (int i = 0; i < arr.length; i++) {
            minPrice = Math.min(minPrice, arr[i]);
            maxProfit = Math.max(maxProfit, arr[i] - minPrice);
        }
        return maxProfit;
    }
}
```

---

### 🧮 Dry Run

**Input:** [7,1,5,3,6,4]

| Day | Price | minPrice | Profit Today | maxProfit |
| --- | ----- | -------- | ------------ | --------- |
| 1   | 7     | 7        | 0            | 0         |
| 2   | 1     | 1        | 0            | 0         |
| 3   | 5     | 1        | 4            | 4         |
| 4   | 3     | 1        | 2            | 4         |
| 5   | 6     | 1        | 5            | 5 ✅       |
| 6   | 4     | 1        | 3            | 5         |

✅ **Answer:** 5

---

### ⏱️ Complexity

* **Time:** O(n)
* **Space:** O(1)

---

### ✨ Key Idea

This is essentially **Kadane’s Algorithm applied to stock differences**.
We find the max subarray of daily profit differences.

---

## 🧠 2️⃣ **Best Time to Buy and Sell Stock II (Multiple Transactions Allowed)**

**(LeetCode 122)**

### 🔹 Problem Statement

You can buy and sell multiple times, but you must sell before you buy again.
Find the **maximum profit possible**.

**Example:**

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation:
Buy at 1, sell at 5 → profit = 4  
Buy at 3, sell at 6 → profit = 3  
Total = 7
```

---

### 💡 Intuition

Whenever the **next day’s price is higher**, take profit — as if you sell every time price increases.
So just keep adding all positive differences between consecutive days.

---

### 🧩 Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }
        return profit;
    }
}
```

---

### 🧮 Dry Run

**Input:** [7,1,5,3,6,4]

| Day | Price | Change | Profit |
| --- | ----- | ------ | ------ |
| 2   | 1     | ↓      | 0      |
| 3   | 5     | +4     | 4      |
| 4   | 3     | ↓      | 4      |
| 5   | 6     | +3     | 7 ✅    |
| 6   | 4     | ↓      | 7      |

✅ **Answer:** 7

---

### ⏱️ Complexity

* **Time:** O(n)
* **Space:** O(1)

---

### ✨ Key Idea

You’re summing **all upward slopes** — each rise contributes profit.
This is a **greedy** approach inspired by Kadane’s continuous gain idea.

---

## 🧠 3️⃣ **Best Time to Buy and Sell Stock III (At Most Two Transactions)**

**(LeetCode 123)**

### 🔹 Problem Statement

You can complete **at most two transactions** (i.e., buy-sell twice).
Find the **maximum total profit** you can achieve.

**Example:**

```
Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation:
Buy at 0, sell at 3 → profit = 3  
Buy at 1, sell at 4 → profit = 3  
Total = 6
```

---

### 💡 Intuition

We extend the single-transaction logic:

* `buy1` = cost of first buy (lowest price)
* `sell1` = profit after first sell
* `buy2` = effective cost for second buy (price - profit from first sell)
* `sell2` = profit after second sell (final answer)

---

### 🧩 Code

```java
class Solution {
    public int maxProfit(int[] arr) {
        int buy1 = Integer.MAX_VALUE;
        int buy2 = Integer.MAX_VALUE;
        int sell1 = 0;
        int sell2 = 0;
        for (int i = 0; i < arr.length; i++) {
            buy1 = Math.min(buy1, arr[i]);           // Lowest price for first buy
            sell1 = Math.max(sell1, arr[i] - buy1);  // Max profit after first sell
            buy2 = Math.min(buy2, arr[i] - sell1);   // Effective cost for second buy
            sell2 = Math.max(sell2, arr[i] - buy2);  // Max profit after second sell
        }
        return sell2;
    }
}
```

---

### 🧮 Dry Run

**Input:** [3,3,5,0,0,3,1,4]

| Day | Price | buy1 | sell1 | buy2 | sell2 |
| --- | ----- | ---- | ----- | ---- | ----- |
| 1   | 3     | 3    | 0     | 3    | 0     |
| 2   | 3     | 3    | 0     | 3    | 0     |
| 3   | 5     | 3    | 2     | 3    | 2     |
| 4   | 0     | 0    | 2     | -2   | 2     |
| 5   | 0     | 0    | 2     | -2   | 2     |
| 6   | 3     | 0    | 3     | -2   | 5     |
| 7   | 1     | 0    | 3     | -2   | 5     |
| 8   | 4     | 0    | 4     | -2   | 6 ✅   |

✅ **Answer:** 6

---

### ⏱️ Complexity

* **Time:** O(n)
* **Space:** O(1)

---

### ✨ Key Idea

This is **Kadane’s extended** logic with two phases — think of `sell1` as the first Kadane, and `sell2` as applying it again after reinvesting the profit.
A **Dynamic Programming** twist built on Kadane’s pattern.

---

## 🧩 Summary Table

| Problem                     | Transactions | Approach                     | Time | Space |
| --------------------------- | ------------ | ---------------------------- | ---- | ----- |
| Best Time to Buy & Sell I   | 1            | Track min price & max profit | O(n) | O(1)  |
| Best Time to Buy & Sell II  | Unlimited    | Add all positive profits     | O(n) | O(1)  |
| Best Time to Buy & Sell III | 2            | DP with two buy/sell pairs   | O(n) | O(1)  |

## 📘 Problem: Subarray Sum Equals K

**LeetCode:** 560
**Topic:** Arrays, Prefix Sum, HashMap
**Goal:** Count the total number of *continuous subarrays* whose sum equals `k`.

---

## 🧠 Concept: Prefix Sum

The **prefix sum** at index `i` is the sum of all elements up to index `i`.

If

```
prefix[j] - prefix[i] = k
```

then the subarray from `(i+1 ... j)` has sum `k`.

So we just need to find **how many previous prefix sums** satisfy this condition while iterating.

---

## ⚙️ Approach 1: Brute Force (O(n²))

### 🔸 Idea

Check every possible subarray and calculate its sum.

### 🔹 Code

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        int count = 0;

        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                sum += nums[j];
                if (sum == k)
                    count++;
            }
        }
        return count;
    }
}
```

### ⏱️ Time Complexity

* Time → O(n²)
* Space → O(1)

---

## ⚙️ Approach 2: Optimized Using Prefix Sum + HashMap (O(n))

### 🔸 Idea

Use a HashMap to store prefix sums and their frequencies.
While traversing:

* Maintain running sum → `sum`
* Check if `(sum - k)` exists in map → if yes, add its frequency to count
* Then, add/update current `sum` in map

### 🔹 Code

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0, sum = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1); // base case: subarray starting from index 0

        for (int num : nums) {
            sum += num;

            if (map.containsKey(sum - k)) {
                count += map.get(sum - k);
            }

            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

---

## 🧩 Example Dry Run

**Input:**
`nums = [1, 2, 3], k = 3`

| Step | num | sum | sum-k | map before    | count | map after         |
| ---- | --- | --- | ----- | ------------- | ----- | ----------------- |
| Init |     | 0   |       | {0=1}         | 0     | {0=1}             |
| 1    | 1   | 1   | -2    | {0=1}         | 0     | {0=1,1=1}         |
| 2    | 2   | 3   | 0     | {0=1,1=1}     | 1     | {0=1,1=1,3=1}     |
| 3    | 3   | 6   | 3     | {0=1,1=1,3=1} | 2     | {0=1,1=1,3=1,6=1} |

✅ Subarrays with sum = 3:
→ `[1, 2]`, `[3]`
**Answer = 2**

---

## 📈 Complexity

| Type  | Complexity |
| ----- | ---------- |
| Time  | O(n)       |
| Space | O(n)       |

---

## 🧩 Similar Problems (Prefix Sum / Kadane Variants)

| Problem                             | Concept              |
| ----------------------------------- | -------------------- |
| 🔹 Maximum Subarray Sum             | Kadane’s Algorithm   |
| 🔹 Longest Subarray with Sum K      | Prefix Sum + HashMap |
| 🔹 Count Subarrays with Given XOR   | Prefix XOR + HashMap |
| 🔹 Subarray Sum Divisible by K      | Prefix Mod + HashMap |
| 🔹 Continuous Subarray Sum (LC 523) | Prefix Mod + HashMap |
| 🔹 Minimum Size Subarray Sum        | Sliding Window       |

---

## 🧠 Key Points to Remember

✅ Initialize map with `{0=1}` for subarrays starting from index 0.
✅ Update map **after** checking condition.
✅ Works with **positive, negative, or zero** elements.
✅ Prefix Sum + HashMap is a **universal pattern** for many subarray problems.

### 🧩 Problem Statement

Given an unsorted integer array `nums`, return the **length of the longest consecutive sequence** of elements.
You must implement an algorithm that runs in **O(n)** time.

---

### 🧠 Intuition

The challenge is to find a **continuous range of numbers** (like 1,2,3,4...) present in the array, **without sorting** it (since sorting = O(n log n)).

So, we use a **HashSet** to achieve O(1) lookups.

---

### 💡 Approach: Using HashSet

#### Steps:

1. **Store all elements in a HashSet**

   * This removes duplicates and allows quick existence checks.
2. **Iterate through each element `n` in the set**

   * If `n - 1` does **not exist**, it means `n` is the **start of a sequence**.
3. **Expand the sequence**

   * Keep checking `n + 1`, `n + 2`, ... until the next number doesn’t exist.
   * Count the length of this streak.
4. **Track the maximum length** seen so far.

---

### 🔹 Code Explanation

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        // Edge case: empty array
        if (nums == null || nums.length == 0) {
            return 0;
        }

        // Step 1: Store all numbers in a set
        Set<Integer> set = new HashSet<>();
        for (int i : nums) {
            set.add(i);
        }

        int maxLength = 1;

        // Step 2: Iterate through the set
        for (int n : set) {
            // Step 3: Only start counting if n is the start of a sequence
            if (!set.contains(n - 1)) {
                int currNum = n;
                int currLen = 1;

                // Step 4: Count consecutive numbers
                while (set.contains(currNum + 1)) {
                    currNum++;
                    currLen++;
                }

                // Step 5: Update max length
                maxLength = Math.max(maxLength, currLen);
            }
        }

        return maxLength;
    }
}
```

---

### 🧮 Dry Run Example

**Input:**
`nums = [100, 4, 200, 1, 3, 2]`

| Step | Element      | `n-1` in set? | Sequence Formed | Current Length | Max Length |
| ---- | ------------ | ------------- | --------------- | -------------- | ---------- |
| 100  | ❌            | [100]         | 1               | 1              |            |
| 4    | ✅ (3 in set) | skip          | -               | 1              |            |
| 200  | ❌            | [200]         | 1               | 1              |            |
| 1    | ❌            | [1, 2, 3, 4]  | 4               | **4**          |            |
| 3    | ✅            | skip          | -               | 4              |            |
| 2    | ✅            | skip          | -               | 4              |            |

✅ **Output:** `4`
The longest consecutive sequence is `[1, 2, 3, 4]`.

---

### ⏱️ Time and Space Complexity

| Type      | Complexity | Explanation                                                                          |
| --------- | ---------- | ------------------------------------------------------------------------------------ |
| **Time**  | O(n)       | Each number is processed at most twice (once for checking and once while expanding). |
| **Space** | O(n)       | For storing elements in the HashSet.                                                 |

---

### 🧠 Key Insights

✅ Using a HashSet avoids sorting → achieves **O(n)** complexity.
✅ Start counting **only when `n - 1` is missing**, to avoid double-counting.
✅ Handles unsorted arrays and duplicates seamlessly.

---

### 🔥 Related Problems

| Problem                           | Concept              |
| --------------------------------- | -------------------- |
| 🟩 Missing Number                 | XOR / Sum approach   |
| 🟩 Longest Increasing Subsequence | Dynamic Programming  |
| 🟩 Longest Subarray with Sum K    | Prefix Sum + HashMap |
| 🟩 Consecutive Numbers Sum        | Math, Sequence       |

---

### 🏁 Final Notes

* This is one of the **most popular HashSet-based problems** in DSA interviews.
* It demonstrates your understanding of **O(1) lookups**, **sequence logic**, and **loop optimization**.
* Often asked by **FAANG** companies.

## 🧩 Problem: **Set Matrix Zeroes**

### 🔍 Problem Statement

You are given an `m x n` matrix.
If any element in the matrix is `0`, set its **entire row and column** to `0`.

You must do this **in place**, i.e., modify the same matrix (not create a new one).

---

### 💡 Example

**Input:**

```
[
 [1, 2, 3],
 [4, 0, 6],
 [7, 8, 9]
]
```

**Output:**

```
[
 [1, 0, 3],
 [0, 0, 0],
 [7, 0, 9]
]
```

---

### 🧠 Intuition

When we find a `0` in the matrix,
→ The **entire row and column** containing that `0` should become `0`.

If we start setting them to `0` immediately,
we’ll **lose information** about other zeroes that might appear later.

So, we:

1. First **mark** which rows and columns need to be zeroed.
2. Then, in a second pass, we **update** the matrix based on those marks.

---

### 🪄 Approach

#### Step 1: Initialize helper arrays

Create two arrays:

* `row[n]` → to mark rows that should be zeroed
* `col[m]` → to mark columns that should be zeroed

Both start with all `0`s.

#### Step 2: Traverse matrix to mark zero positions

Loop through the matrix:
If `matrix[i][j] == 0`, then:

```
row[i] = 1
col[j] = 1
```

This means row `i` and column `j` must be set to `0` later.

#### Step 3: Update matrix

Traverse matrix again.
If `row[i] == 1` **or** `col[j] == 1`,
then set `matrix[i][j] = 0`.

---

### 🧩 Dry Run

**Input:**

```
[
 [1, 2, 3],
 [4, 0, 6],
 [7, 8, 9]
]
```

**After marking zeroes:**

```
row = [0, 1, 0]
col = [0, 1, 0]
```

**After updating matrix:**

```
[
 [1, 0, 3],
 [0, 0, 0],
 [7, 0, 9]
]
```

---

### 🧮 Time & Space Complexity

| Operation                       | Complexity   |
| ------------------------------- | ------------ |
| Traversing matrix twice         | **O(n × m)** |
| Extra space for row[] and col[] | **O(n + m)** |

---

### ⚡ Optimized Approach (In-Place, O(1) Space)

Use the **first row and first column of the matrix** itself as markers
instead of creating extra arrays.

Steps:

1. Use `matrix[0][j]` and `matrix[i][0]` to mark.
2. Keep flags to track if first row or first column originally had zeroes.
3. Update rest of matrix accordingly.

This brings space down to **O(1)**.

---

### 🏁 Final Code (Your Version)

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;
        int row[] = new int[n];
        int col[] = new int[m];

        // Step 1: Mark rows and columns that need to be zeroed
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (matrix[i][j] == 0) {
                    row[i] = 1;
                    col[j] = 1;
                }
            }
        }

        // Step 2: Set elements to zero based on marks
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (row[i] == 1 || col[j] == 1) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

---

### 🧷 Key Takeaways

* Always mark first before modifying.
* Extra arrays help avoid overwriting data.
* Optimized version uses **matrix itself as marker** → saves space.

## 🧩 Problem: **Rotate Image / Matrix by 90° Clockwise**

### 🔍 Problem Statement

You’re given an `n x n` 2D matrix.
Rotate the matrix **90° clockwise**, **in place** (i.e., without using any extra space).

---

### 💡 Example

**Input:**

```
[
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
]
```

**Output:**

```
[
 [7, 4, 1],
 [8, 5, 2],
 [9, 6, 3]
]
```

---

### 🧠 Intuition

A 90° clockwise rotation can be done in **two steps**:

1. **Transpose the matrix** — convert rows into columns.
2. **Reverse each row** — to align elements correctly for the clockwise direction.

That’s exactly what your code does ✅

---

### 🪄 Step-by-Step Approach

#### 🔹 Step 1: Transpose the matrix

Swap `matrix[i][j]` with `matrix[j][i]` for all `i < j`.

After this, rows become columns.

**Example after transpose:**

```
Before:
1 2 3
4 5 6
7 8 9

After transpose:
1 4 7
2 5 8
3 6 9
```

#### 🔹 Step 2: Reverse each row

Swap elements horizontally (start ↔ end).

**After reversing each row:**

```
7 4 1
8 5 2
9 6 3
```

✅ That’s the 90° rotated matrix!

---

### 🧩 Dry Run

**Input Matrix:**

```
[
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
]
```

#### ➤ After Transpose:

| i | j | swap(matrix[i][j], matrix[j][i]) |
| - | - | -------------------------------- |
| 0 | 1 | swap(2,4) → [1,4,3;2,5,6;7,8,9]  |
| 0 | 2 | swap(3,7) → [1,4,7;2,5,6;3,8,9]  |
| 1 | 2 | swap(6,8) → [1,4,7;2,5,8;3,6,9]  |

**Matrix now:**

```
1 4 7
2 5 8
3 6 9
```

#### ➤ Reverse each row:

Row 1 → [1,4,7] → [7,4,1]
Row 2 → [2,5,8] → [8,5,2]
Row 3 → [3,6,9] → [9,6,3]

**Final Rotated Matrix:**

```
7 4 1
8 5 2
9 6 3
```

---

### 🧮 Time & Space Complexity

| Operation        | Complexity |
| ---------------- | ---------- |
| Transpose matrix | **O(n²)**  |
| Reverse rows     | **O(n²)**  |
| Extra space      | **O(1)**   |

---

### 🏁 Final Code (Your Version)

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // Step 1: Transpose the matrix
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse each row
        int s = 0, e = n - 1;
        while (s < e) {
            for (int i = 0; i < n; i++) {
                int temp = matrix[i][s];
                matrix[i][s] = matrix[i][e];
                matrix[i][e] = temp;
            }
            s++;
            e--;
        }
    }
}
```

---

### ⚡ Alternate (Simpler) Row Reversal Using Built-in Swap Logic

Instead of using two pointers (`s`, `e`),
you can directly reverse each row in a nested loop:

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n / 2; j++) {
        int temp = matrix[i][j];
        matrix[i][j] = matrix[i][n - j - 1];
        matrix[i][n - j - 1] = temp;
    }
}
```

---

### 🧷 Key Takeaways

* **Transpose + Reverse = 90° Clockwise Rotation** ✅
* Both steps take **O(n²)** time and **O(1)** space.
* Works **in place** (no extra matrix needed).


## 🌀 **Spiral Matrix Traversal — Full Notes with Code**

### 💡 **Problem Statement**

Given an `n x m` matrix, return all elements in **spiral order** (clockwise).

---

### ⚙️ **Approach**

We use **four boundary pointers**:

* `top` → starting row
* `bottom` → ending row
* `left` → starting column
* `right` → ending column

We move in **4 directions**:

1. Left → Right
2. Top → Bottom
3. Right → Left
4. Bottom → Top

After completing one full outer layer, we move inward by updating the boundaries.

---

### 🧠 **Algorithm Steps**

```text
1. Initialize: top = 0, bottom = n-1, left = 0, right = m-1
2. While not all elements are visited:
   a. Traverse top row (left → right)
   b. Traverse right column (top → bottom)
   c. Traverse bottom row (right → left)
   d. Traverse left column (bottom → top)
   e. Move inward: top++, bottom--, left++, right--
```

---

### 💻 **Code Implementation (Java)**

```java
class Solution {
    public List<Integer> spiralOrder(int[][] mat) {
        int n = mat.length;       // number of rows
        int m = mat[0].length;    // number of columns
        List<Integer> ans = new ArrayList<>();

        // Define boundaries
        int top = 0, bottom = n - 1, left = 0, right = m - 1;
        int totalElements = 0;

        // Traverse until all elements are covered
        while (totalElements < n * m) {

            // Step 1: Left → Right
            for (int i = left; i <= right && totalElements < n * m; i++) {
                ans.add(mat[top][i]);
                totalElements++;
            }
            top++;

            // Step 2: Top → Bottom
            for (int i = top; i <= bottom && totalElements < n * m; i++) {
                ans.add(mat[i][right]);
                totalElements++;
            }
            right--;

            // Step 3: Right → Left
            for (int i = right; i >= left && totalElements < n * m; i--) {
                ans.add(mat[bottom][i]);
                totalElements++;
            }
            bottom--;

            // Step 4: Bottom → Top
            for (int i = bottom; i >= top && totalElements < n * m; i--) {
                ans.add(mat[i][left]);
                totalElements++;
            }
            left++;
        }

        return ans;
    }
}
```

---

### 🧩 **Dry Run Example**

#### Input Matrix:

```
1   2   3
4   5   6
7   8   9
```

#### Step-by-step Traversal:

| Step | Direction    | Visited Elements            | Boundaries Updated |
| ---- | ------------ | --------------------------- | ------------------ |
| 1    | Left → Right | [1, 2, 3]                   | top = 1            |
| 2    | Top → Bottom | [1, 2, 3, 6, 9]             | right = 1          |
| 3    | Right → Left | [1, 2, 3, 6, 9, 8, 7]       | bottom = 1         |
| 4    | Bottom → Top | [1, 2, 3, 6, 9, 8, 7, 4]    | left = 1           |
| 5    | Left → Right | [1, 2, 3, 6, 9, 8, 7, 4, 5] | top = 2            |

✅ **All elements visited → Stop**

---

### 🔁 **Output**

```
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```

---

### 📊 **Time & Space Complexity**

| Type     | Complexity   | Explanation                                  |
| -------- | ------------ | -------------------------------------------- |
| ⏱ Time   | **O(n × m)** | Every element visited once                   |
| 💾 Space | **O(1)**     | Constant extra space (excluding result list) |

---

### 📘 **Visualization**

```
Initial Matrix:
1 → 2 → 3
↓       ↓
4       6
↓       ↓
7 ← 8 ← 9

Then move inside:
       5
```

## 💡 **Problem: Maximum Product Subarray**

You are given an integer array `arr[]`.
Find the **contiguous subarray** within it that has the **largest product** and return that product.

---

### 🧠 **Key Idea**

Unlike **maximum subarray sum**, here multiplication changes behavior when negatives are involved.

* Multiplying by a **negative number** flips the sign.
* So the **maximum** product so far can become the **minimum**, and vice versa.

Hence, we track **both max and min product** at each step.

---

### ⚙️ **Approach**

We maintain three variables:

1. `maxProduct1` → maximum product ending at current index
2. `minProduct2` → minimum product ending at current index
3. `product` → overall maximum product found so far

At each element:

* Compute:

  ```java
  tempMax = max(arr[i], maxProduct1 * arr[i], minProduct2 * arr[i])
  minProduct2 = min(arr[i], maxProduct1 * arr[i], minProduct2 * arr[i])
  maxProduct1 = tempMax
  product = max(product, maxProduct1)
  ```

This handles:

* Negative numbers (swap effect)
* Zeros (reset point)
* Positives (normal multiplication)

---

### 💻 **Code**

```java
import java.util.*;

class Solution {
    public int maxProduct(int arr[]) {
        int n = arr.length;

        int maxProduct1 = arr[0];  // max product ending here
        int minProduct2 = arr[0];  // min product ending here
        int product = arr[0];      // global max product

        for (int i = 1; i < n; i++) {
            int tempMax = Math.max(arr[i], Math.max(maxProduct1 * arr[i], minProduct2 * arr[i]));
            minProduct2 = Math.min(arr[i], Math.min(maxProduct1 * arr[i], minProduct2 * arr[i]));
            maxProduct1 = tempMax;

            product = Math.max(product, maxProduct1);
        }
        return product;
    }
}
```

---

### 🔁 **Dry Run Example**

#### Input:

```
arr = [2, 3, -2, 4]
```

| i | arr[i] | maxProduct1             | minProduct2              | product | Explanation            |
| - | ------ | ----------------------- | ------------------------ | ------- | ---------------------- |
| 0 | 2      | 2                       | 2                        | 2       | Initialize             |
| 1 | 3      | max(3, 2×3, 2×3)=6      | min(3, 2×3, 2×3)=3       | 6       | 2×3=6                  |
| 2 | -2     | max(-2, 6×-2, 3×-2)= -2 | min(-2, 6×-2, 3×-2)= -12 | 6       | Sign flips             |
| 3 | 4      | max(4, -2×4, -12×4)=4   | min(4, -2×4, -12×4)= -48 | 6       | 4 positive, resets max |

✅ **Output:** `6`

(From subarray `[2, 3]`)

---

### ⚡ **Another Example**

```
arr = [-2, 0, -1]
```

| Step | arr[i] | maxProduct1 | minProduct2 | product |
| ---- | ------ | ----------- | ----------- | ------- |
| 0    | -2     | -2          | -2          | -2      |
| 1    | 0      | 0           | 0           | 0       |
| 2    | -1     | -1          | -1          | 0       |

✅ Output: `0`
(Best subarray is `[0]`)

---

### 📊 **Complexity Analysis**

| Type     | Complexity | Explanation               |
| -------- | ---------- | ------------------------- |
| ⏱ Time   | **O(n)**   | Single pass through array |
| 💾 Space | **O(1)**   | Constant extra space      |

---

### 🧩 **Summary**

| Variable      | Meaning                         |
| ------------- | ------------------------------- |
| `maxProduct1` | Max product up to current index |
| `minProduct2` | Min product up to current index |
| `product`     | Overall max product             |

✅ Handles positives, negatives, and zeros efficiently.
✅ Works in one pass.


# 🚀 **Problem: 3Sum**

### 🧠 Problem Statement:

Given an integer array `nums`, return **all unique triplets** `[nums[i], nums[j], nums[k]]`
such that:

```
i != j, i != k, j != k
and
nums[i] + nums[j] + nums[k] == 0
```

The solution set must **not contain duplicate triplets**.

---

## ⚙️ Approach — Two Pointer after Sorting

### 🔍 Intuition:

We need 3 numbers whose sum is **0**.
If we fix one number (`nums[i]`), the problem reduces to **2-sum** for the remaining array:

```
Find two numbers whose sum = -nums[i]
```

We can efficiently find this using the **two-pointer technique** after sorting.

---

## 🪜 Step-by-Step Approach

### Step 1️⃣ — Sort the Array

We sort the array to:

* Make it easier to skip duplicates.
* Use two-pointer traversal for the remaining elements.

Example:

```
Input: nums = [-1, 0, 1, 2, -1, -4]
Sorted: [-4, -1, -1, 0, 1, 2]
```

---

### Step 2️⃣ — Fix one element (nums[i])

For each element `nums[i]` (up to `n-2`):

* Set `p1 = i + 1` (left pointer)
* Set `p2 = n - 1` (right pointer)

Now, check the sum:

```
sum = nums[i] + nums[p1] + nums[p2]
```

---

### Step 3️⃣ — Apply Two-Pointer Logic

We adjust pointers based on the sum:

| Case         | Condition          | Action                               |
| ------------ | ------------------ | ------------------------------------ |
| ✅ `sum == 0` | Found a triplet    | Add it to result set; increment `p1` |
| 🔼 `sum < 0` | Need a larger sum  | Move `p1++` (right → higher value)   |
| 🔽 `sum > 0` | Need a smaller sum | Move `p2--` (left → smaller value)   |

---

### Step 4️⃣ — Avoid Duplicates

To prevent repeated triplets:

* Use a **Set** (like `HashSet<List<Integer>>`) since Lists with same elements are equal in a set.
* Alternatively, after sorting, you can skip repeated `nums[i]` and `nums[p1]`.

---

## 🧩 Example Dry Run

### Input:

```
nums = [-1, 0, 1, 2, -1, -4]
```

### After Sorting:

```
[-4, -1, -1, 0, 1, 2]
```

| i | nums[i] | p1 | p2 | sum | Action                | Result                    |
| - | ------- | -- | -- | --- | --------------------- | ------------------------- |
| 0 | -4      | 1  | 5  | -3  | sum<0 → p1++          | —                         |
| 0 | -4      | 2  | 5  | -3  | sum<0 → p1++          | —                         |
| 0 | -4      | 3  | 5  | -2  | sum<0 → p1++          | —                         |
| 0 | -4      | 4  | 5  | -1  | sum<0 → p1++          | —                         |
| 1 | -1      | 2  | 5  | 0   | ✅ triplet (-1, -1, 2) | [[-1, -1, 2]]             |
| 1 | -1      | 3  | 4  | 0   | ✅ triplet (-1, 0, 1)  | [[-1, -1, 2], [-1, 0, 1]] |
| 2 | -1      | 3  | 5  | 1   | sum>0 → p2--          | —                         |

✅ Final Output: `[[ -1, -1, 2 ], [ -1, 0, 1 ]]`

---

## 🧮 Code Implementation

```java
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums); // Step 1: sort the array
        Set<List<Integer>> ans = new HashSet<>();

        for (int i = 0; i < nums.length - 2; i++) {
            int p1 = i + 1;
            int p2 = nums.length - 1;

            while (p1 < p2) {
                int sum = nums[i] + nums[p1] + nums[p2];
                if (sum == 0) {
                    ans.add(List.of(nums[i], nums[p1], nums[p2]));
                    p1++;
                    p2--;
                } else if (sum < 0) {
                    p1++;
                } else {
                    p2--;
                }
            }
        }
        return new ArrayList<>(ans);
    }
}
```

---

## ⏱️ Time & Space Complexity

| Complexity       | Explanation                                                           |
| ---------------- | --------------------------------------------------------------------- |
| **Time:** O(n²)  | Sorting = O(n log n), and for each element, we use two-pointer = O(n) |
| **Space:** O(n²) | In worst case, storing all unique triplets in the set                 |

---

## 🧠 Key Takeaways

✅ Sort the array first → simplifies duplicate handling
✅ Use two-pointer technique for O(n²) solution
✅ A `Set` automatically filters duplicate triplets
✅ Better than brute force O(n³)


# 📘 4Sum Problem — Notes

---

## 🧩 Problem Statement

Find all unique quadruplets `[a, b, c, d]` in the array such that:

```
a + b + c + d == target
```

---

## 💡 Key Idea

This problem is an **extension of the 2Sum and 3Sum problems**.
We use sorting + two-pointer technique.

---

## 🔧 Approach

1. **Sort the array** to handle duplicates and apply two-pointer logic easily.
2. **Fix first two numbers** using nested loops:

   * Outer loop → `i` (0 to n−4)
   * Inner loop → `j` (i+1 to n−3)
3. **Apply two-pointer** on the remaining array:

   * `k = j + 1`
   * `l = n - 1`
4. Compute sum:

   ```
   sum = nums[i] + nums[j] + nums[k] + nums[l]
   ```
5. **Compare with target:**

   * If `sum == target` → store the quadruplet
   * If `sum < target` → move `k++`
   * If `sum > target` → move `l--`
6. Use `Set` or skip duplicates manually to ensure unique quadruplets.

---

## 🧠 Important Points

✅ Sort array before processing
✅ Use `long` for sum to avoid overflow
✅ Handle duplicates using Set or conditions
✅ Use two-pointer for efficiency

---

## ⏱️ Complexity

| Type  | Complexity                     |
| ----- | ------------------------------ |
| Time  | O(n³)                          |
| Space | O(k) — for storing quadruplets |

---

## 🧾 Example

### Input:

```
nums = [1, 0, -1, 0, -2, 2]
target = 0
```

### Sorted:

```
[-2, -1, 0, 0, 1, 2]
```

### Output:

```
[[-2, -1, 1, 2],
 [-2, 0, 0, 2],
 [-1, 0, 0, 1]]
```

---

## 🧰 Code (Using Set)

```java
import java.util.*;

class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        Set<List<Integer>> set = new HashSet<>();

        for (int i = 0; i < n - 3; i++) {
            for (int j = i + 1; j < n - 2; j++) {
                int k = j + 1, l = n - 1;
                while (k < l) {
                    long sum = (long) nums[i] + nums[j] + nums[k] + nums[l];
                    if (sum == target) {
                        set.add(List.of(nums[i], nums[j], nums[k], nums[l]));
                        k++;
                        l--;
                    } else if (sum < target) {
                        k++;
                    } else {
                        l--;
                    }
                }
            }
        }
        return new ArrayList<>(set);
    }
}
```

---

## 🚀 Optimized Version (Without Set)

```java
import java.util.*;

class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        int n = nums.length;

        for (int i = 0; i < n - 3; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1; j < n - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;
                int k = j + 1, l = n - 1;

                while (k < l) {
                    long sum = (long) nums[i] + nums[j] + nums[k] + nums[l];
                    if (sum == target) {
                        res.add(Arrays.asList(nums[i], nums[j], nums[k], nums[l]));
                        while (k < l && nums[k] == nums[k + 1]) k++;
                        while (k < l && nums[l] == nums[l - 1]) l--;
                        k++; l--;
                    } else if (sum < target) k++;
                    else l--;
                }
            }
        }
        return res;
    }
}
```

---

## 🧩 Summary Table

| Step | Action              | Purpose                   |
| ---- | ------------------- | ------------------------- |
| 1    | Sort the array      | Enables two-pointer logic |
| 2    | Fix two numbers     | Reduce problem size       |
| 3    | Two-pointer on rest | Find matching pairs       |
| 4    | Handle duplicates   | Avoid repeated results    |
| 5    | Store valid sets    | Return final result       |

---

# 📘 Pascal’s Triangle — Notes

---

## 🧩 Problem Statement

Generate the first `n` rows of **Pascal’s Triangle**, where:

* Each number is the sum of the two numbers directly above it.
* The first and last element of each row is always **1**.

Example:
For `n = 5`,

```
[
 [1],
 [1, 1],
 [1, 2, 1],
 [1, 3, 3, 1],
 [1, 4, 6, 4, 1]
]
```

---

## 💡 Approach Used — Combinatorics Formula

Each element in Pascal’s Triangle can be computed using the formula for **nCr**:

[
C(n, r) = \frac{n!}{r! (n - r)!}
]

But instead of recomputing factorials every time (which is inefficient), we use the **relation between consecutive elements** in a row:

[
C(n, r) = C(n, r-1) \times \frac{(n - r)}{r}
]

---

## 🔧 Step-by-Step Logic

### 1️⃣ `generateRow(int n)`

Generates a single row of Pascal’s Triangle.

* Start with `1` (C(n,0) = 1).
* Use the above formula iteratively to compute each element:

  ```java
  ans = ans * (n - i) / i
  ```
* Add each computed value to the list.

For example:
If `n = 5`, the row = `[1, 4, 6, 4, 1]`

---

### 2️⃣ `generate(int n)`

Generates all rows up to row `n`.

* Loop from `1` to `n`
* For each iteration, call `generateRow(i)`
* Add the resulting row to the final list

---

## 🧮 Dry Run Example

For `n = 5`:

| i (Row no.) | Row Generated   |
| ----------- | --------------- |
| 1           | [1]             |
| 2           | [1, 1]          |
| 3           | [1, 2, 1]       |
| 4           | [1, 3, 3, 1]    |
| 5           | [1, 4, 6, 4, 1] |

Final Output:

```
[
 [1],
 [1, 1],
 [1, 2, 1],
 [1, 3, 3, 1],
 [1, 4, 6, 4, 1]
]
```

---

## 🧾 Code

```java
import java.util.*;

class Solution {

    // Function to generate one row of Pascal's Triangle
    public static List<Integer> generateRow(int n) {
        int ans = 1;
        List<Integer> list = new ArrayList<>();
        list.add(1);
        for (int i = 1; i < n; i++) {
            ans = ans * (n - i);
            ans = ans / i;
            list.add(ans);
        }
        return list;
    }

    // Function to generate n rows of Pascal's Triangle
    public static List<List<Integer>> generate(int n) {
        List<List<Integer>> ans = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            ans.add(generateRow(i));
        }
        return ans;
    }
}
```

---

## 🧠 Key Points

✅ Uses mathematical relation between combinations
✅ Avoids factorial computation (efficient)
✅ Time Complexity: **O(n²)**
✅ Space Complexity: **O(n²)**

---

## 🔍 Alternate Approach

You can also generate Pascal’s Triangle using **dynamic programming** by building each row from the previous one:

```java
for (int i = 1; i <= n; i++) {
    List<Integer> row = new ArrayList<>();
    row.add(1);
    for (int j = 1; j < i - 1; j++) {
        row.add(prevRow.get(j - 1) + prevRow.get(j));
    }
    if (i > 1) row.add(1);
    ans.add(row);
}
```

# 📘 **Count Inversions in an Array**

---

## 🧩 **Problem Statement**

Given an array `arr[]`, count the number of **inversions** in it.
An inversion is a pair `(i, j)` such that:

[
i < j \text{ and } arr[i] > arr[j]
]

### Example:

```
Input: arr = [5, 4, 3, 2, 1]
Output: 10
Explanation:
All pairs are inverted because array is sorted in descending order.
```

---

## 💡 **Intuition**

* Inversions indicate how far the array is from being sorted.
* A sorted array has `0` inversions.
* A completely reverse-sorted array has maximum inversions = `n*(n-1)/2`.

Naive solution would be to check every pair → **O(n²)**.
We can optimize it using **Merge Sort**, which counts inversions while sorting → **O(n log n)**.

---

## ⚙️ **Approach (Using Merge Sort)**

### 🔹 Step 1: Divide and Conquer

We recursively divide the array into two halves:

* Left half
* Right half

### 🔹 Step 2: Count inversions

There are 3 types of inversions:

1. **Left inversions** → counted in left half recursion.
2. **Right inversions** → counted in right half recursion.
3. **Split inversions** → counted while merging both halves.

A split inversion occurs when an element in the left half is greater than an element in the right half.

---

## 🧠 **Key Insight**

When merging two sorted halves:

If
[
arr[left] > arr[right]
]
then all remaining elements in the left half
(from `left` to `mid`)
will also be greater than `arr[right]`.

Hence,
[
\text{count} += (mid - left + 1)
]

---

## 🧾 **Code Explanation**

```java
private static int merge(int[] arr, int low, int mid, int high) {
    ArrayList<Integer> temp = new ArrayList<>();
    int left = low, right = mid + 1;
    int cnt = 0;

    // Merge while counting inversions
    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.add(arr[left]);
            left++;
        } else {
            temp.add(arr[right]);
            cnt += (mid - left + 1); // <-- key step
            right++;
        }
    }

    // Copy remaining elements
    while (left <= mid) temp.add(arr[left++]);
    while (right <= high) temp.add(arr[right++]);

    // Copy sorted elements back to arr
    for (int i = low; i <= high; i++) arr[i] = temp.get(i - low);

    return cnt;
}

public static int mergeSort(int[] arr, int low, int high) {
    int cnt = 0;
    if (low >= high) return cnt;

    int mid = (low + high) / 2;

    cnt += mergeSort(arr, low, mid);       // Left half
    cnt += mergeSort(arr, mid + 1, high);  // Right half
    cnt += merge(arr, low, mid, high);     // Count cross inversions

    return cnt;
}

public static int numberOfInversions(int[] a, int n) {
    return mergeSort(a, 0, n - 1);
}
```

---

## 🧮 **Dry Run**

### Input:

`arr = [5, 4, 3, 2, 1]`

#### Step 1: Split recursively

```
[5,4,3,2,1]
 -> [5,4,3] and [2,1]
 -> [5,4], [3] and [2], [1]
```

#### Step 2: Merge and Count

1. Merge [5] and [4]:

   * 5 > 4 → count = 1
     → [4,5]

2. Merge [4,5] and [3]:

   * 4 > 3 → +2 (since both 4 and 5 > 3)
     → count = 3
     → [3,4,5]

3. Merge [2] and [1]:

   * 2 > 1 → +1
     → count = 4
     → [1,2]

4. Merge [3,4,5] and [1,2]:

   * 3 > 1 → +3
   * 3 > 2 → +3
   * 4 > 2 → +2
   * 5 > 2 → +2
     → total = 10 inversions

Final count = **10**

---

## ⏱️ **Time & Space Complexity**

| Operation        | Complexity                 |
| ---------------- | -------------------------- |
| Merge Sort Split | O(log n)                   |
| Merge Operation  | O(n)                       |
| **Overall**      | **O(n log n)**             |
| **Space**        | **O(n)** (temporary array) |

---

## ✅ **Output**

```
The number of inversions are: 10
```

---

## 🧠 Summary

| Concept          | Description                    |
| ---------------- | ------------------------------ |
| Problem Type     | Array, Divide & Conquer        |
| Algorithm        | Modified Merge Sort            |
| Time Complexity  | O(n log n)                     |
| Space Complexity | O(n)                           |
| Key Idea         | Count inversions while merging |

---
