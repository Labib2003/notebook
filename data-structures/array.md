[Home](../README.md)

# Array

A contiguous, fixed length block of memory that can store a collection of elements of similar data types.

### Advantages

- Ability to index elements in O(1) time, necessary for algorithms like Binary Search.

### Disadvantages

- Fixed length.

## Index Calculation (all calculations are for 0 indexing)

Arrays don't keep track of all of the elements of the list, instead it uses the first elements address and an offset value to index any element of the array.

$$LOC(A[I]) = Base(A) + (I * W)$$

```c
int arr[] = {1, 2, 3};
printf("%d %d %d\n", *arr, *arr + 1, *arr + 2);
// under the hood, *arr + 1 = *arr + (1 * sizeof(int))
// output: 1 2 3
```

## 2D Array Indexing

A two dimensional array is m x n array A, is a collection of m \* n elements such that each element is specified by a pair of integers, like I and J, called subscripts such that,

$$1 <= I <= m$$
$$1 <= J <= n$$

Just like linear arrays, in a two dimensional m x n array A, the computer does not keep track of the addresses of every element. It only keeps track of the base address of A, Base(A), the address of element A[J, K] are computed as the address LOC(A[J, K]) using the following formulas,

// for column major order
$$LOC(A[J, K]) = Base(A) + w((J - 1) + m(K - 1))$$
// for row major order
$$LOC(A[J, K]) = Base(A) + w(n(J - 1) + (K - 1))$$

Whether an array is represented in row major or column major order depends on the specific language.

## Dynamic Arrays

Normally arrays have a fixed length. But it is possible to implement an array that grows and shrinks as the number of elements changes.

C++ Vector is an example of a dynamic array.

A simple implementation of a dynamic array

```cpp
class MyVector {
private:
  int len = 0, cap = 16;
  int *arr = new int[cap];

  void resize(double mod) {
    if (mod < 0)
      cout << "Invalid modifier: Only positive numbers are allowd." << endl;
    cap = cap * mod;
    arr = (int *)realloc(arr, sizeof(int) * cap);
  }

public:
  int size() { return len; }

  int capacity() { return cap; }

  bool is_empty() { return len == 0; }

  int at(int idx) {
    if (idx < len)
      return *(arr + idx);
    else {
      cout << "Invalid index." << endl;
      return '\0';
    }
  }

  void push(int val) {
    if (len >= cap)
      resize(2);
    *(arr + len) = val;
    len++;
  }

  void insert(int idx, int val) {
    if (idx > len || idx >= cap * 2) {
      cout << "Invalid index." << endl;
      return;
    }

    if (idx >= cap)
      resize(2);

    for (int i = len; i >= idx; i--)
      *(arr + i + 1) = *(arr + i);
    *(arr + idx) = val;
    len++;
  }

  void prepend(int val) { insert(0, val); }

  int pop() {
    if (len == 0) {
      cout << "Underflow: List is empty." << endl;
      return '\0';
    }
    int val = *(arr + len - 1);
    len--;

    if (len <= cap / 4)
      resize(.5);

    return val;
  };

  void del(int idx) {
    if (len == 0) {
      cout << "Underflow: List is empty." << endl;
      return;
    }

    for (int i = idx; i < len; i++)
      *(arr + i) = *(arr + i + 1);
    len--;

    if (len <= cap / 4)
      resize(.5);
  }

  void remove(int val) {
    for (int i = 0; i < len;) {
      if (*(arr + i) == val)
        del(i);
      else
        i++;
    }
  };

  int find(int val) {
    for (int i = 0; i < len; i++) {
      if (*(arr + i) == val)
        return i;
    }
    return -1;
  }

  ~MyVector() { delete[] arr; }
};
```
