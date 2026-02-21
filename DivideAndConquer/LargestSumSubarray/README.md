


# 🧠 Largest Sum Subarray (Divide & Conquer)

## 📌 Problem Statement
Given an array of numbers, find the **contiguous subarray** that has the **maximum sum**.

**Example:**
```
Array: -6, -2, 8, 3, 4, -2
Maximum Subarray: [8, 3, 4]
Sum = 15
```

---

## 🔶 Divide & Conquer Rule
Divide & Conquer works in **3 steps**:

1. ✂️ **Divide** → Split the array into two halves  
2. ⚔️ **Conquer** → Solve each half recursively  
3. 🔗 **Combine** → Merge results to get the final answer  

---

## 🔷 How It Works
For any subarray `[left … right]`, we divide at:
```
mid = (left + right) / 2
```

The maximum subarray must be one of these:
1️⃣ Entirely in the **Left Half**  
2️⃣ Entirely in the **Right Half**  
3️⃣ **Crossing the middle**  

---

### 🔵 Case 1: Left Subarray
Maximum sum lies completely inside `[left … mid]`.

### 🔵 Case 2: Right Subarray
Maximum sum lies completely inside `[mid+1 … right]`.

### 🔵 Case 3: Crossing Subarray (Important!)
- Starts in left half  
- Ends in right half  
- **Must include the middle element**  

**Steps:**
- Start at `mid` → move left → find best left sum  
- Start at `mid+1` → move right → find best right sum  
- Add both → `Cross Sum = Left + Right`

---

## 🔷 Final Decision
We compare:
```
max( Left Sum, Right Sum, Cross Sum )
```
Whichever is maximum → that’s the answer for that segment.

---

## ⏱️ Time Complexity
Recurrence:
```
T(n) = 2T(n/2) + O(n)
```
- 2 recursive calls  
- O(n) to compute crossing sum  

Using **Master Theorem**:
```
T(n) = O(n log n)
```

---

# 🧩 Code Walkthrough

### 1️⃣ `maxCrossing()` Function
Purpose: Find the best subarray that **crosses the middle**.

- **Step 1:** Move left from `mid` → track best left sum  
- **Step 2:** Move right from `mid+1` → track best right sum  
- **Return:**  
```js
{ sum: leftSum + rightSum, start: maxLeft, end: maxRight }
```

---

### 2️⃣ `buildTree()` Function
Main recursive function.

- **Base Case:**  
If `left === right` → single element → return it.  

- **Recursive Division:**  
```js
let mid = Math.floor((left + right) / 2);
let leftTree = buildTree(arr, left, mid);
let rightTree = buildTree(arr, mid+1, right);
```

- **Combine Step:**  
```js
let cross = maxCrossing(arr, left, mid, right);
```

- **Select Maximum:**  
```js
let maxVal = Math.max(leftTree.sum, rightTree.sum, cross.sum);
```

- **HTML Tree Creation:**  
Builds a **visual recursion tree** showing left, right, and crossing results.

---

### 3️⃣ `start()` Function
Triggered by button click:
- Reads input array  
- Calls `buildTree()`  
- Displays final result  

---

### 4️⃣ `animateTree()`
Adds UI enhancements:
- Staggered animation  
- Highlight selected node  
- Fade-in for final result  

---

# 🌳 Big Picture Flow
For input:
```
-6, -2, 8, 3, 4, -2
```

Recursion tree looks like:

```
                 [-6,-2,8,3,4,-2]
               /                  \
        [-6,-2,8]              [3,4,-2]
        /       \               /     \
    [-6,-2]    [8]          [3,4]   [-2]
```

At each level:
- Compute Left  
- Compute Right  
- Compute Cross  
- Select best  

**Final Answer:**  
```
[8, 3, 4] → Sum = 15
```

---

# 🔥 Key Insight
The **crossing case** is essential.  
Without it, the algorithm fails when the best subarray spans both halves.

---

# ✅ Final Summary
- **Concept:** Divide → Conquer → Combine  
- **Cases:** Left, Right, Cross  
- **Time Complexity:** O(n log n)  
- **Code:**  
  - `maxCrossing()` → crossing sum  
  - `buildTree()` → recursion + tree  
  - `start()` → input + run  
  - `animateTree()` → visualization  
```


