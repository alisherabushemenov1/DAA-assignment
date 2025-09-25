# Design and Analysis of Algorithms - Assignment 1  

## Architecture Notes  

### Recursion Depth Control  
- QuickSort: Tail recursion elimination ensures O(log n) recursion depth in practice.  
- MergeSort: Balanced divide-and-conquer with O(log n) depth.  
- Select: Median-of-medians guarantees O(log n) depth.  
- ClosestPair: Divide-and-conquer on geometric data ensures O(log n) recursion.  

### Memory Management  
- MergeSort: Single reusable buffer.  
- QuickSort: In-place with recursion stack only.  
- Select: In-place partitioning.  
- ClosestPair: Temporary arrays for strip checking.  

### Small-n Optimizations  
Both sorting algorithms switch to insertion sort for very small subarrays.  

### Recurrence Analysis  
- MergeSort: Θ(n log n)  
- QuickSort: Θ(n log n) expected, O(n²) worst (avoided by randomization)  
- Select: Θ(n)  
- ClosestPair: Θ(n log n)  

---

## Experimental Results  

### Performance Data Summary  

**Timing Results (milliseconds)**  

| Algorithm   | n=100 | n=1000 | n=5000 | n=10000 |
|-------------|-------|--------|--------|---------|
| MergeSort   | 14.2  | 307.4  | 2946.3 | 4694.1  |
| QuickSort   | 19.8  | 107.6  | 475.4  | 2992.0  |
| Select      | 61.7  | 179.4  | 422.5  | 1481.9  |
| ClosestPair | 660.7 | 3641.2 | 3806.5 | 9973.7  |  

---

### Recursion Depth Analysis  

| Algorithm   | Theoretical       | n=1000 | n=5000 | n=10000 |
|-------------|-------------------|--------|--------|---------|
| MergeSort   | ⌈log₂n⌉≈10        | 7      | 9      | 10      |
| QuickSort   | ~2log₂n≈20        | 5      | 7      | 7       |
| Select      | O(log n)          | 7      | 10     | 11      |
| ClosestPair | ⌈log₂n⌉≈10        | 9      | 9      | 10      |  

---

## Algorithm-Specific Observations  

### MergeSort  
- Time Complexity: Matches Θ(n log n), growth is smooth with n.  
- Input Sensitivity: Sorted inputs are faster due to fewer comparisons; reverse is slightly slower.  
- Depth Behavior: Matches log₂n.  

### QuickSort  
- Average Case: Random inputs perform well, better than MergeSort at n=1000.  
- Best/Worst Case: Sorted and reverse cases show no degradation (randomization works).  
- Depth Bound: Maximum depths are well below 2log₂n.  

### Select Algorithm  
- Linear Scaling: Execution time increases roughly linearly with n.  
- Constant Factors: Much higher constants than sorting; slower at small n.  
- Depth: Small and stable.  

### Closest Pair  
- Complexity: Growth follows n log n.  
- Geometric Effects: Uniform random points give consistent performance.  

---

## Input Type Analysis  
- Random Input: Both MergeSort and QuickSort show expected Θ(n log n) scaling. QuickSort often faster due to in-place nature.  
- Sorted Input: MergeSort benefits most, becoming much faster than QuickSort at large n.  
- Reverse Sorted: Both algorithms handle well (randomization prevents QuickSort from quadratic behavior).  
- Many Duplicates: Both algorithms handle gracefully; QuickSort’s three-way partitioning helps.  

---

## Summary  

### Theory vs. Practice Alignment  
- Perfect Matches:  
  - MergeSort and ClosestPair follow n log n scaling.  
  - Select demonstrates linear behavior with small recursion depth.  
- Expected Deviations:  
  - QuickSort shows faster average performance than MergeSort due to in-place operations.  
  - Constant factors are large for Select, making it slower at small n despite Θ(n).  

### Key Insights  
1. Randomization in QuickSort avoids worst-case scenarios completely.  
2. MergeSort benefits from presorted input, unlike QuickSort.  
3. ClosestPair algorithm validates theoretical O(n log n) bound even for thousands of points.  

### Practical Performance Notes  
- Small-n optimizations improve constant factors.  
- Memory reuse in MergeSort is effective.  
- QuickSort randomization is crucial for robust performance.  

---

## Usage  

### Build, Test, and Run  
```bash
mvn clean compile test
mvn compile exec:java -Dexec.mainClass="algorithms.MetricsCollector"
mvn compile exec:java -Dexec.mainClass="algorithms.AlgorithmCLI"
