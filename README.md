# Fenwick


Fenwick Trees, also known as Binary Indexed Trees (BITs), are data structures that provide efficient methods for cumulative frequency tables, cumulative sums, and other operations that require frequent updates and prefix sum queries.


1. Data Structure
A Fenwick Tree is typically used with an array A of size n, where the tree itself is represented as an auxiliary array BIT of size n+1 (1-indexed). The key operations that Fenwick Trees support are:
Update Operation: Increment a value at a specific index in the array.
Prefix Sum Query: Compute the sum of elements from the start of the array up to a specific index.

2. Structure of the Tree
The Fenwick Tree is based on the binary representation of indices:
Each index i in the tree BIT stores the sum of elements from some subarray of A.
The range of the subarray that BIT[i] covers depends on the binary representation of i.
For example, in a 1-indexed array:
BIT[1] covers A[1].
BIT[2] covers A[1] + A[2].
BIT[3] covers A[3].
BIT[4] covers A[1] + A[2] + A[3] + A[4].
The range covered by BIT[i] is determined by the lowest set bit in the binary representation of i.

3. Update Operation
To update the value at index i in the array A, we must update multiple entries in the BIT array. The process is:
Add the update value delta to BIT[i].
Move to the next index that includes A[i] in its sum, which is calculated as i + (i & -i).
Repeat the process until i exceeds the size of the array.
The update operation can be expressed as:
BIT[i] += delta
i = i + (i & -i)

4. Prefix Sum Query
To compute the sum of elements from A[1] to A[i], sum the relevant elements from BIT:
Initialize sum = 0.
Add BIT[i] to sum.
Move to the parent index by subtracting the lowest set bit from i, calculated as i - (i & -i).
Repeat until i becomes 0.
The prefix sum operation can be expressed as:
sum += BIT[i]
i = i - (i & -i)



1. Binary Representation
The binary operation i & -i isolates the lowest set bit of i. This bit determines how much of the array A the BIT[i] covers.

2. Time Complexity
Both the update and prefix sum query operations run in O(log n) time. This is because each operation requires moving from one index to another, which is determined by the number of bits in the index. The number of such moves is proportional to the logarithm of the array size.
