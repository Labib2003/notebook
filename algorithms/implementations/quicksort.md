[Home](../../README.md)

# Quicksort

A divide and conquer sorting algorithm where after each iteration, one element gets sorted to the right place. In other words, after each iteration, the list gets **weakly sorted** meaning one element is placed where every element to its left is less than or equal and every element to the right is greater but the left and right sub-lists are not necessarily sorted.

## Procedure

Quicksort:

- Take a list, and weakly sort it. The index of the sorted element is called the pivot.
- Recursively sort the left and right sub-lists until the sub-list length is 0.

To weakly sort the list, we define a function called `partition`. There are two main implementations: Hoare's and Lomuto's. The first one is slightly more efficient.

Hoare's partition:

- Take a list and set the first element as the pivot.
- Set two pointers `i` and `j` at the lower and upper bound of the list.
- Keep incrementing `i` until the ith element is greater than or equal to pivot.
- Keep decrementing `j` until the jth element is less than or equal to pivot.
- Swap the ith and jth elements.
- Repeat this process until `i` and `j` overlap.
- Return the jth element as the pivot.

## Simulation

```
p
1, 2, 5, 3, 4

   p
1, 2, 5, 3, 4

            p
1, 2, 4, 3, 5

      p
1, 2, 4, 3, 5
```

## Code

```cpp
// hoare partition
int partition(int arr[], int lb, int ub) {
  int pivot = arr[lb], i = lb, j = ub;

  // until two pointers meet
  while (i < j) {
    // move i until greater than or equal to pivot is found
    while (arr[i] < pivot)
      i++;

    // move j until less than or equal to pivot is found
    while (arr[j] > pivot)
      j--;

    // swap
    swap(arr[i], arr[j]);
  }

  // return the meeting point
  return j;
}

void quick_sort(int arr[], int lb, int ub) {
  if (lb < ub) {
    int partition_idx = partition(arr, lb, ub);
    quick_sort(arr, lb, partition_idx);
    quick_sort(arr, partition_idx + 1, ub);
  }
}
```
