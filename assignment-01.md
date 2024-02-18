

# CMPS 2200 Assignment 1

**Name:**__Joshua Allison_______________________


In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not? 
.  It is in O(2^n) because if you expand 2^n+1 it can be simplifed to 2*2^n which can be seen as c*2^n which falls in the upper bound of O(n). 
.  
.  
.  
. 
  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     
.  No it is not conatined in O(2^n). 2^2^n grows signifcantly faster so it will be far out of the range of O(2^n) and there is no constant. 
.  
.  
.  
.  
  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    
.  No it is not in O(log^2n). n^1.01 is a polynomial function and will grow faster than any logarithmic function squared. Over time the difference will get much more clear that it grows faster so it does not belong to the set of big O(log^2 n) 
.  
.  
.  

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?  
.  Yes it grows faster as it is a polynomial function and the other is logarithmic making it in the set of the omega(log^2 n). 
.  
.  
.  
  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  
.  No sqrt(n) is not in O((log n)^3) because the sqrt(n) is going to grow faster than the log of n and will grow much faster than (logn) ^3 because it being cubed makes it go even slower. As n becomes large the growth rate will exceed the other
.  
.  
.  
  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  
.  Yes sqrt(n) is in Omega ((logn)^3) because the sqrt(n) is going to grow quicker making it above the Omega when looking at it graphically making it within the set of Omega((logn)^3)


2. **SPARC to Python** (12 pts)

Consider the following SPARC code of the Fibonacci sequence, which is the series of numbers where each number is the sum of the two preceding numbers. For example, 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610 ... 
$$
\begin{array}{l}
\mathit{foo}~x =   \\
~~~~\texttt{if}{}~~x \le 1~~\texttt{then}{}\\
~~~~~~~~x\\   
~~~~\texttt{else}\\
~~~~~~~~\texttt{let}{}~~(ra, rb) = (\mathit{foo}~(x-1))~~,~~(\mathit{foo}~(x-2))~~\texttt{in}{}\\  
~~~~~~~~~~~~ra + rb\\  
~~~~~~~~\texttt{end}{}.\\
\end{array}
$$ 

  - 2a. (6 pts) Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. (6 pts) What does this function do, in your own words?  
This function takes the index of item in the provided list, x, and if it is 1 or less it returns that as the start of the fibonacci sequence and if it is not, then it sets two new variables ra and rb recursively to the indexes 1 anmd 2 behind x. It lastly adds the two together to get the return fibonacci number in the sequence.
.  
.  
.  
.  
.  
.  
.  
.  
  

3. **Parallelism and recursion** (26 pts)

Consider the following function:  

```python
def longest_run(myarray, key)
   """
    Input:
      `myarray`: a list of ints
      `key`: an int
    Return:
      the longest continuous sequence of `key` in `myarray`
   """
```
E.g., `longest_run([2,12,12,8,12,12,12,0,12,1], 12) == 3`  
 
  - 3a. (7 pts) First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. (4 pts) What is the Work and Span of this implementation?  
The work and span of the longest run implemenetation are both the number of elements in the input list. 
.  
.  
.  
.  
.  
.  
.  
.  
.  


  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?  
.  Given a list of size n, the recursion tree will have a height of log(n), where each level splits the list and then combines the results from the two halves. At each level, the total work done across all nodes is O(n) because each element is involved in a constant amount of work for comparison and combining results. Therefore, the total work done by the algorithm is the sum of work done at each level or
W(n) = O(nlogn) 
For the Span, during each level of recursion, the list is divided in half, leading to a recursion tree of depth log(n). Each recursive call is dependent on the completion of the previous calls in its path (need the results from both halves to combine them), leading to a span that is proportional to the depth of the recursion tree. So the span is S(n) = O(logn)
.  
.  
.  
.  
.  
.  
.  
.  
.  
.  


  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  
Work will be the same as before because the total amount of computation does not change when we parrallelize. Each element in the array is still processed a fixed number of times as the array is divided and the results are combined.
The Span now depends on the depth of the recursion tree rather than the work at each level. Each recursive division effectively halves the problem size, and since both halves can be processed in parallel, the Span is dictated by the number of divisions needed to reduce the problem to its base case, which is S(n) = O(logn), the depth of the tree.
.  
.  
.  
.  
.  
.  
.  
.  

