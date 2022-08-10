## TODO
- [ ] GCD

## Big O
What is the time, space complexity of following code :

```
        int a = 0, b = 0;    
        for (i = 0; i < N; i++) {
            a = a + rand();  
        }

        for (j = 0; j < M; j++) {
            b = b + rand();
        }
```

Assume that rand() is O(1) time, O(1) space function.

First loop runs n times
Second loop runs m times
This makes runtime 0(n + m)

Space is two variables, which is 0(1)

What is the time, space complexity of following code :

```
    int a = 0, b = 0;    
    for (i = 0; i < N; i++) {
        for (j = 0; j < N; j++) {
            a = a + j;
        }
    }

    for (k = 0; k < N; k++) {
        b = b + k;
    } 
```

i loop is done N times
j loop is done N times
k loop is done N times

i and j are nested
Runtime
This is 0(N^2 + N) => 0(N^2)
Space is two variables 0(1)

What is the time complexity of the following code :

```
    int a = 0;
    for (i = 0; i < N; i++) {
        for (j = N; j > i; j--) {
            a = a + i + j;
        }
    }

```
Runtime
i loop is done N times
N = 6
i = 0 => j = 6...0 N
i = 1 => j = 6...1 N - 1
....
N * (N + N - 1 + N - 2 + .... 0)
O(N^2)

Space is one variable 0(1)

What is the time complexity of the following code :

```
  int a = 0, i = N;
  while (i > 0) {
      a += i;
      i /= 2;
  }

```
Runtime
For every iteration a increments by i this doesn't effect the loop though
For every iteration i is cut in half
6 => 3 => 1 => 0
This halfing makes the pattern 0(logN)
Space is two variables which makes it 0(1)

What is time complexity of following code :

```
    int count = 0;
    for (int i = N; i > 0; i /= 2) {
        for (int j = 0; j < i; j++) {
            count += 1;
        }
    }
```
Runtime
i loop is halfing every iteration
j loop is running the same amount as i

For example assume N = 6
i = 6 => j = 0...5  N
i = 3 => j = 0...3  N/2
i = 1 => j = 0...1  N/4
N + N/2 + N/4  => 0(N)
Space is one variable which makes it 0(1)

What is the time complexity of the following code :

```
  int i, j, k = 0;
  for (i = n/2; i <= n; i++) {
      for (j = 2; j <= n; j = j * 2) {
           k = k + n/2;
      }
  }
```
Runtime
i loop is n/2 to n which is reduced to n
j loop is doubling every iteration which reduces to logn
0(N * logN)
Space is one variable 0(1)

Given the following C++ function, let n >= m.
```
    int gcd(int n, int m) {
      if (n%m ==0) return m;
      if (n < m) swap(n, m);
      while (m > 0) {
        n = n%m;
        swap(n, m);
      }
      return n;

    }
```
What is the time complexity of the above function assuming n > m?. 
Θ symbol represents theta notation and Ω symbol represents omega notation.

## TODO

In a competition, four different functions are observed. All the functions use a single for loop and within the for loop, same set of statements are executed.

Consider the following for loops:

  A) for(i = 0; i < n; i++)
  B) for(i = 0; i < n; i += 2)
  C) for(i = 1; i < n; i *= 2)
  D) for(i = n; i > -1; i /= 2)

If n is the size of input(positive), which function is the most efficient? In other words, which loop completes the fastest.

A loops N times 0(N)
B loops N/2 times 0(N)
C loops logN times since it halfs each time 0(logN)
D loops an infinite amount of times since it cannot be less the 0

The answer is C.

Which of the following is not bounded by O(n^2)?

A (15^10) * n + 12099
B n^1.98
C n^3 / (sqrt(n))
D (2^20) * n

A is An + B => 0(n)
B is n^1.98 => 0(n^2)
C is n^3 * (1 / sqrt(n)) => n^(3 - .5) => 0(n^2.5)
D is A*n => 0(n)

The only terms unbounded by n^2 is C

Which of the given options provides the increasing order of complexity of functions f1, f2, f3 and f4:

f1(n) = 2^n
f2(n) = n^(3/2)
f3(n) = nLogn
f4(n) = n^(Logn)

f1 is 0(2^n)
f2 is 0(n^2)
f3 is 0(nlogn)
f4 is 0(n^(logN)) when logN gets high it goes past 2

The order is f3, f2, f4, f1

What is the time complexity of the following code :

```
    int j = 0;
    for(int i = 0; i < n; ++i) {
        while(j < n && arr[i] < arr[j]) {
            j++;
        }
    }
```

loop i is run N times
the while loop 
a = [1, 2, 3, 4, 5]

i = 0 ; while exits since arr[i] == arr[j] j = 0
i = 1 ; while j++ j = 1 then it exits on the next loop
i = 2;  while j++ j = 2 then it exits on the next loop
...
The while will only execute once then exit
Runtime => 0(N * 1) => 0(N)

What is the worst case time complexity of the following code :
```
/* 
 * V is sorted 
 * V.size() = N
 * The function is initially called as searchNumOccurrence(V, k, 0, N-1)
 */

    int searchNumOccurrence(vector<int> &V, int k, int start, int end) {
        if (start > end) return 0;
        int mid = (start + end) / 2;
        if (V[mid] < k) return searchNumOccurrence(V, k, mid + 1, end);
        if (V[mid] > k) return searchNumOccurrence(V, k, start, mid - 1);
        return searchNumOccurrence(V, k, start, mid - 1) + 1 + searchNumOccurrence(V, k, mid + 1, end);
    }
```

NOTE : This question involves recursion which will be explained later in topic Backtracking. So, if you are not able to approach this question now, you can give it a try later.

Look at 3 cases:
Case 1: We have no occurences
  Then the algo is logN since this is binarysearch
Case 2: We have one occurance
  Then the algo is still logN for the same reason as case 1
Case 3: We have a filled array of the occurance.
  Then we have to touch every element once and that is N
  
What is the worst case time complexity of the following code:
```
int findMinPath(vector<vector<int> > &V, int r, int c) {
  int R = V.size();
  int C = V[0].size();
  if (r >= R || c >= C) return 100000000; // Infinity
  if (r == R - 1 && c == C - 1) return 0;
  return V[r][c] + min(findMinPath(V, r + 1, c), findMinPath(V, r, c + 1));
}
```
Assume R = V.size() and C = V[0].size().

NOTE : This question involves recursion which will be explained later in topic Backtracking. So, if you are not able to approach this question now, you can give it a try later.
 
Assume a 3 x 3 grid.
1 x x   
x x x
x x 2

1 1 x
1 x x
x x 2
So in 3 x 3 grid we make 
      0 , 0
    /       \
  1, 0      0, 1
  /  \      /  \
2, 0 1, 1 1, 1 0, 2

Level 1 we make 2 calls
Level 2 we make 4 calls
Level 3 we make 8 calls
      i we make 2^i calls

For every index we visit we make two functionl number of calls = 1 + 2 + 4 + ... 2^i + ... 2^(M + N - 2)  = O(2^(M + N)) calls.
      
In worst case , We need to go down till the last square box .
So we need to make r+c -2 (leaving first and last square) .
Now at each move we have 2 choices i.e. either row or column .

So 2^(r-c-2)

What is the worst case time complexity of the following code:

```
  int memo[101][101];

  int findMinPath(vector<vector<int> >& V, int r, int c) {
    int R = V.size();
    int C = V[0].size();
    if (r >= R || c >= C) return 100000000; // Infinity
    if (r == R - 1 && c == C - 1) return 0;
    if (memo[r][c] != -1) return memo[r][c];
    memo[r][c] =  V[r][c] + min(findMinPath(V, r + 1, c), findMinPath(V, r, c + 1));
    return memo[r][c];
  }
```
Callsite : 
memset(memo, -1, sizeof(memo));
findMinPath(V, 0, 0);

Assume R = V.size() and C = V[0].size() and V has positive elements
NOTE : This question involves recursion which will be explained later in topic Backtracking. So, if you are not able to approach this question now, you can give it a try later.1

Assume a 3 x 3 grid.
1 x x   
x x x
x x 2

1 1 1
1 1 1
1 1 2

This is different the previous function is that there is no overlap in calls.
Each location is visited only once.
0(N * M)

```
function performOps(A){

    m= A.length
    n=A[0].length
    B=[]

    for(i = 0; i < m;i++){
        B.push(new Array(n));
        for(j=0;j< n;j++){
            B[i][n-1-j] = A[i][j]
        }
    }
    return B

}

Lets say performOps was called with A : [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]] .
What would be the output of the following call :


B = performOps(A)
for (i = 0; i < B.length; i++) {
    for (j = 0; j < B[i].length; j++) 
        process.stdout.write(B[i][j]+" ");
}
```
A[0][0] -> B[0][4-1-0]
i V j ->
1,2,3 4               4,3,2,1  
5,6,7,8        =>     8,7 .. 
9,10,11,12             

It just reverses the arrays

What would print out is this:
4 3 2 1 8 7 6 5 12 11 10 9


