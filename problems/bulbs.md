[Home](../README.md)

# Bulbs

Given N bulbs (in a row), either on (1) or off (0). Turning on ith bulb causes all remaining bulbs on the right to flip.

Find the min number of switches to turn all the bulbs on.

## Constraints:

- 1 <= N <= 1e5
- A[i] = {0, 1}

## Naive Solution:

Check and flip each bit manually, O(n<sup>2</sup>).

## Optimized Solution:

Flipping even times goes back to the original state (like double negation), so we can check each bit one by one and if the count is odd, flip just that bit. Then if the bit is not 1, we increment count.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
  int bulbs[] = {0, 1, 0, 1, 1, 0, 1, 1}, count = 0;

  // iterate over all the bulbs
  for (int i = 0; i < sizeof bulbs / sizeof bulbs[0]; i++) {
    // if count is odd, that means the current bulb was toggled to the opposite
    // state by the previous bulb (even negation goes back to original state)
    if (count % 2 != 0)
      bulbs[i] = !bulbs[i];

    // if bulb is off, turn it on and increment count
    if (bulbs[i] != 1) {
      bulbs[i] = 1;
      count++;
    }
  }

  cout << count << endl;
}

```
