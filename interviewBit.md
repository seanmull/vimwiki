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


