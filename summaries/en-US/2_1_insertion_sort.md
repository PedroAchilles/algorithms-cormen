# Summary: *Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein (CLRS) - 3rd Edition

**By:** [Pedro Achilles Carvalho](https://www.linkedin.com/in/pedro-achilles-carvalho/)

---

# 2.1 Insertion Sort

---

## The problem

The problem to be solved is **sorting**: **Input**: A sequence of n numbers `〈a1, a2, ..., an〉`. **Output**: A permutation (reordering) `〈a'1, a'2,..., a'n〉` of the input sequence, such that `a'1 ≤ a'2≤ ... ≤ a'n`.

## The algorithm

The numbers we want to sort are also known as **keys**. Although conceptually we are sorting a sequence, the input is given as an array with *n* elements.

The idea of the algorithm is to sort the numbers by taking one at a time and shifting the already sorted elements one index forward until the ideal position is found for this key. It resembles the idea of sorting cards in your hand: picking them one by one from the table and always reordering the ones already in your hand to place the new one in the correct spot.

## Pseudocode

```
Insertion-Sort(A)
for j = 2 to A.length
   key = A[j]
   // Insert A[j] into the sorted sequence A[1 .. j - 1].
   i = j - 1
   while i > 0 and A[i] > key
      A[i + 1] = A[i]
      i = i - 1
   A[i + 1] = key
```

## Loop invariant and algorithm correctness

**Loop invariant** is a logical property associated with a loop that determines an unchanging condition throughout the execution of that loop, to prove the correctness of the algorithm.

The loop invariant must satisfy these three properties:

1. **Initialization** The invariant is true before the first iteration.

2. **Maintenance** If the invariant is true at the beginning of an iteration, it remains true after that iteration.

3. **Termination** When the loop ends, the invariant implies the goal of the loop has been achieved.

### Application in insertion-sort

The loop invariant of insertion-sort is: `Before each iteration of the for loop, the subset A[1 .. j−1] is sorted.`

1. **Initialization** Before the first iteration, the subset `A[1..j-1]` equals `A[1]`, which is trivially sorted. Therefore, the invariant is true.

2. **Maintenance** Given that `A[1..j−1]` is sorted, we want to insert `A[j]` so that `A[1..j]` becomes sorted. The while loop moves elements greater than `A[j]` to the right until it finds the correct position to insert it. At the end of the iteration, `A[1..j]` is sorted, meaning the invariant remains true.

3. **Termination** The loop ends when `j > A.length`. The invariant guarantees that `A[1..j−1]` is sorted. Since `j−1 == A.length`, then `A[1..A.length]` is sorted.

---

## Exercises

**2.1-1 Using Figure 2.2 as a model, illustrate the operation of Insertion-Sort on the array A = 〈31, 41, 59, 26, 41, 58〉.** **A:**

```
// This demonstration is more technical and shows the steps considering the comparisons made in the while loop.
// O and S represent the subsets of A for illustration.
// Before the first iteration of the for loop
O = [31, 41, 59, 26, 41, 58]
S = [31] // sorted (trivially)
// First iteration of the for loop
O = [59, 26, 41, 58]
S = [31, 41] // compared with 31
S = [31, 41] // sorted (31 is not greater than 41)
// Second iteration
O = [26, 41, 58]
S = [31, 41, 59] // compared with 41
S = [31, 41, 59] // sorted (41 is not greater than 59)
// Third iteration
O = [41, 58]
S = [31, 41, 59, 26] // compared with 59
S = [31, 41, 26, 59] // smaller, move 59 to the right and compare with 41
S = [31, 26, 41, 59] // smaller, move 41 to the right and compare with 31
S = [26, 31, 41, 59] // smaller, move 31 to the right
S = [26, 31, 41, 59] // sorted (i == 0)
// Fourth iteration
O = [58]
S = [26, 31, 41, 59, 41] // compared with 59
S = [26, 31, 41, 41, 59] // smaller, move 59 to the right and compare with 41
S = [26, 31, 41, 41, 59] // sorted (41 is not greater than 41)
// Fifth iteration
O = []
S = [26, 31, 41, 41, 59, 58] // compared with 59
S = [26, 31, 41, 41, 58, 59] // smaller, move 59 to the right and compare with 41
S = [26, 31, 41, 41, 58, 59] // sorted (41 is not greater than 58)
```

**2.1-2 Rewrite the Insertion-Sort procedure to sort in non-increasing order instead of non-decreasing order.** **A:**

```
Insertion-Sort(A)
for j = 2 to A.length
   key = A[j]
   // Insert A[j] into the sorted sequence A[1 .. j - 1].
   i = j - 1
   while i > 0 and A[i] < key // just invert the condition
      A[i + 1] = A[i]
      i = i - 1
   A[i + 1] = key
```

**2.1-3 Consider the search problem:** ***Input***\*: A sequence of `` numbers `` and a value ``. **Output**: An index `` such that `` or the special value `` if `` does not appear in ``.\* **Write pseudocode for linear search that scans the sequence looking for v. Using a *****loop invariant*****, prove that your algorithm is correct. Make sure your loop invariant satisfies the three required properties.** **A:**

```
Linear-Search(A, v)
for i = 1 to A.length
   if A[i] == v
      return i
return NIL
```

***Loop invariant***\*: Before each iteration, the value `` does not appear in elements *`A[1 .. i − 1]`** ****Correctness proof***:\*

- ***Initialization***\*: Before the first iteration, the subset `` is empty, so `` does not appear.\*
- ***Maintenance***\*: If `` is not equal to ``, the iteration ends keeping the invariant valid. If `` is equal to ``, the loop ends and the invariant holds because it refers to ``, which does not include the found value.\*
- ***Termination***\*: If the loop ends without returning an index, then we examined all elements `` and never found ``. The invariant guarantees that `` did not appear in any index, so returning `` is correct.\*

**2.1-4 Consider the problem of adding two **``**-bit binary integers, stored in two arrays **``** and **``**. The sum of the two integers should be stored in binary form in an array of **``** elements **``**. Formally state the problem and write pseudocode to add the two integers.** **A:** ***Problem***\*: Binary Sum **Input**: Two arrays `` and ``, containing binary bits (0 or 1), representing two ``-bit binary numbers. The most significant bit is at `` and ``. Each binary number represents a non-negative integer. **Output**: An array `` representing the binary sum of `` and ``, also with the most significant bit at ``. **Pseudocode**:\*

```
Binary-Sum(A, B)
n = A.length
allocate array C[1 .. n+1]
carry = 0
i = n
for i to 1 by -1:
   sum = A[i] + B[i] + carry
   C[i+1] = sum % 2
   carry = sum / 2   // integer division
C[1] = carry
return C
```
