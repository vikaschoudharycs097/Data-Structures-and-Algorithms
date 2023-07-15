# Array
## Introduction
- Array is ordered collection of same type of values.
- Stored in continuous memory location.
- Support random read operation.
- Can be single or multi dimensional.

**C/C++ Syntax** <br />
`<data_type> arr[size]`

**Java Syntax** <br />
`<data_type>[] arr = new <data_type>[size]` <br /> 
OR <br />
`<data_type> arr[] = new <data_type>[size]` <br /><br />

**Types of array** <br />
- Static array: Size determined during compile time and not able to resize it.
- Dynamic array: Can be resized during runtime time

**Linear Search** <br />
```
int linearSearch(vector<int>vals, int val) {
    for (int i = 0, n = vals.size(); i < n; i++) {
        if (vals[i] == val) {
            return i;
        }
    }

    return -1;
}
```
- Time Complexity: O(n), θ(n), Ω(1) <br />
- Space Complexity: O(1), θ(1), Ω(1) <br />

**Binary Search** <br />
- *Assumption*: array is sorted

```
int binarySearch(vector<int> vals, int val) {
    int low = 0;
    int high = vals.size() - 1;
    int mid;
    while (low <= high) {
        mid = low + (high - low) / 2;
        if (vals[mid] == val) {
            return mid;
        } else if (vals[mid] < val) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    return -1;
}
```
- Time Complexity: O(log n), θ(log n), Ω(1) <br />
- Space Complexity: O(1), θ(1), Ω(1) <br />

**Bubble Sort**
- Also known as Sink sort
```
void sort(vector<int> nums) {
    int n = nums.size();
    bool isSorted = false;
    for (int i = 0; i < n && !isSorted; i++) {
        isSorted = true;
        for (int j = 0; j < n - i - 1; j++) {
            if (nums[j] > nums[j+1]) {
                isSorted = false;
                swap(nums[j], nums[j+1]);
            }
        }
    }
}
```
- Time Complexity: O(n^2), θ(n^2), Ω(n) <br />
- Space Complexity: O(1), θ(1), Ω(1) <br />
- Stable and in-place sorting
- Swap operation(max): n^2
- Comparison operation(max): n^2

**Selection Sort**
```
void sort(vector<int> nums) {
    int n = nums.size();
    int minIndex;
    for (int i = 0; i < n; i++) {
        minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (nums[minIndex] > nums[j]) {
                minIndex = j;
            }
        }

        swap(nums[i], nums[minIndex]);
    }
}
```
- Time Complexity: O(n^2), θ(n^2), Ω(n^2) <br />
- Space Complexity: O(1), θ(1), Ω(1) <br />
- Not Stable and in-place sorting
- Swap operation(max): n
- Comparison operation: n^2

**Insertion Sort**
```
void sort(vector<int> nums) {
    int n = nums.size();
    for (int i = 1; i < n; i++) {
        int j = i - 1;
        int tmp = nums[i];
        while (j >= 0 && nums[j] > tmp) {
            nums[j+1] = nums[j];
            j--;
        }
        nums[j+1] = tmp;
    }
}
```
- Time Complexity: O(n^2), θ(n^2), Ω(n) <br />
- Space Complexity: O(1), θ(1), Ω(1) <br />
- Stable and in-place sorting
- Comparison operation(max): n^2