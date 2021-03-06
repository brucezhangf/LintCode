 
 
 
## Review (7)
**0. [Heapify.java](https://github.com/awangdev/LintCode/blob/master/Java/Heapify.java)**      Level: Review      Tags: [Heap, MinHeap]
      

Turn unsorted array into a min-heap array, where for each A[i], 

A[i * 2 + 1] is the left child of A[i] and A[i * 2 + 2] is the right child of A[i].

#### Heap
- Heap用的不多. 得用一下, 才好理解. 通常default 的PriorityQueue就是给了一个现成的min-heap:
- 所有后面的对应element都比curr element 小。
- Heapify里面的**siftdown**的部分:
- 只能从for(i = n/2-1 ~ 0)， 而不能从for(i = 0 ~ n/2 -1): 必须中间开花，向上跑的时候才能确保脚下是符合heap规则的

#### Heapify/SiftDown做了什么?
- 确保在heap datastructure里面curr node下面的两个孩子，以及下面所有的node都遵循一个规律
- 比如在这里，若是min-heap,就是后面的两孩子都要比自己大。若不是，就要swap。    

#### min-heap的判断规律:
- for each element A[i], we will get A[i * 2 + 1] >= A[i] and A[i * 2 + 2] >= A[i].
- siftdown时：在curr node和两个son里面小的比较。如果的确curr < son, 搞定，break while.   
- 但若curr 并不比son小，那么就要换位子，而且继续从son的位子往下面盘查。    



---

**1. [Maximum Subarray III.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Subarray%20III.java)**      Level: Review      Tags: []
      


---

**2. [Valid Perfect Square.java](https://github.com/awangdev/LintCode/blob/master/Java/Valid%20Perfect%20Square.java)**      Level: Review      Tags: [Binary Search, Math]
      

Binary找sqrt. 基本 mid+1, mid-1 template.
注意: define index as long. 



---

**3. [Regular Expression Matching.java](https://github.com/awangdev/LintCode/blob/master/Java/Regular%20Expression%20Matching.java)**      Level: Review      Tags: [Backtracking, DP, String]
      



---

**4. [Maximum Average Subarray II.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Average%20Subarray%20II.java)**      Level: Review      Tags: [Array, Binary Search, PreSum]
      

给int[] nums 和 window min size k. window size可以大于K. 找最大的连续数列average value.

- Binary Search的思想, 用在所要找的这个 average sum 上面. 大小是在[min, max]之中
- 找k的时候, 是>=k都可以, 巧用一个 min(preSum)的概念.
- 找k的时候, 画图, 可以看出来, 其实要的是 k window 里面的sum [x, i], 所以要用 sum[0, i] - sum[0, x]

需要仔细去读下面的notes.



---

**5. [The Skyline Problem.java](https://github.com/awangdev/LintCode/blob/master/Java/The%20Skyline%20Problem.java)**      Level: Review      Tags: [Binary Indexed Tree, Divide and Conquer, Heap, PriorityQueue, Segment Tree, Sweep Line]
      

又叫做skyline. 用Sweep Line做的O(nLogN), 但是貌似还有很多做法: segement tree, hashheap, treeSet?

#### Sweep Line, Time O(nLogN), Space O(n)
- original reference http://codechen.blogspot.com/2015/06/leetcode-skyline-problem.html?_sm_au_=isVmHvFmFs40TWRt
- 画图分析: 需要找到 non-overlaping height point at current index; also height needs to be different than prev height peek to be visible.
- 把所有点分出来， 每个点有index x, 再加上一个height.         
- 在这个list上排序，根据index和height. 注意用负数标记building start point height, 这样保证start在end 之前
- 用负数的height标记start: 在priority queue里面同一个x-pos比较 startPoint.height, endPoint.height 的时候, 因为end height是整数, 所以compare时会自动把start point放在end point前面
- 当然了, 如果两个 start point比较, 第二个point的负数超大的话(也就是height很高), 就会顺理compare return正数, 成章形成倒位
- 在processs时候用max-heap (reversed priorityqueue)，再iterate heightPoints 来存最大的height . 遇到peek,就是一个合理的解    
- heightQueue里面加一个0, 用来在结尾的时候做closure

#### Segment Tree
- 看了一些做法, segment tree写法很复杂, 估计在面试中难以用segment tree来写: https://www.cnblogs.com/tiezhibieek/p/5021202.html

#### HashHeap
- HashHeap template 可以考虑: https://www.jiuzhang.com/solution/building-outline/#tag-highlight-lang-java

Binary Indexed Tree?





---

**6. [Remove Invalid Parentheses.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Invalid%20Parentheses.java)**      Level: Review      Tags: [BFS, DFS, DP]
      

给一个string, 里面有括号和其他字符. 以最少刀 剪出 valid string, 求所有这样的string.

这个题目有多种解法, 最强就是O(n) space and time

#### DFS and reduce input string
- in dfs: remove the incorrect parentheses one at a time
- detect the incorrect parentheses by tracking/counting (similar to validation of the parentheses string): `if(count<0)`
- once detected, remove the char from middle of s, and dfs on the rest of the s that has not been tested yet.

##### Core concept: reverse test
- `if a parenthese string is valid, the reverse of it should also be valid`
- Test s with open='(', close=')' first; **reverse s**, and test it with open=')', close='('

##### Minor details
- only procceed to remove invalid parenthese when `count<0`, and also break && return dfs after the recursive calls.
- The above 2 facts eliminates all the redundant results.
- Reverse string before alternating open and close parentheses, so when returning final result, it will return the correct order.
- Open questions: how does it guarantee minimum removals?

##### Backtracking
- 如果用stringbuffer, 那么久不会每次create new string, 但是需要maintain这个string buffer, 就会backtracking

##### Complexity
- Seems to be O(n), but need to derive

#### BFS
TODO

#### DP



---

