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
```C++
int linearSearch(const vector<int>& nums, int target) {
    for (int i = 0, n = nums.size(); i < n; i++) {
        if (nums[i] == target) {
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

```C++
int binarySearch(const vector<int>& nums, int target) {
    int low = 0;
    int high = nums.size() - 1;
    int mid;
    while (low <= high) {
        mid = low + (high - low) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
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
```C++
void sort(vector<int>& nums) {
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
```C++
void sort(vector<int>& nums) {
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
```C++
void sort(vector<int>& nums) {
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

**Merge Sort**
```C++
// Divide array into two halves recursively
void divide(vector<int>& nums, int low, int high) {
    if (low < high) {
        int mid = low + (high - low) / 2;
        divide(nums, low, mid);
        divide(nums, mid+1, high);
        merge(nums, low, mid, high);
    }
}

// Merge two sorted halves into sorted array
void merge(vector<int>& nums, int low, int mid, int high) {
    int i = low;
    int j = mid + 1;
    int k = 0;
    vector<int> tmp(high - low + 1);
    while (i <= mid && j <= high) {
        if (nums[i] <= nums[j]) {
            tmp[k] = nums[i++];
        } else {
            tmp[k] = nums[j++];
        }
        k++;
    }

    while (i <= mid) {
        tmp[k++] = nums[i++];
    }

    // Copy back from temporary array
    for (i = 0; i < k; i++) {
        nums[low + i] = tmp[i];
    }
}

void sort(vector<int>& nums) {
    divide(nums, 0, nums.size() - 1);
}
```
- Time Complexity: O(n * log n), θ(n * log n), Ω(n * log n) <br />
- Space Complexity: O(n), θ(n), Ω(n) <br />
- Stable and Not in-place sorting

**Quick Sort**
```C++
// Select pivot element and move it to proper position
// Left side of pivot element are smaller than it and 
// right side are greater than it.
int partition(vector<int>& nums, int low, int high) {
    int j = low - 1;
    int randIndex = rand() % (high - low + 1) + 1;
    int pivotEle = nums[randIndex];
    nums[randIndex] = nums[high];
    for (int i = low; i < high; i++) {
        if (nums[i] < pivotEle) {
            j++;
            swap(nums[i], nums[j]);
        }
    }
    j++;
    nums[high] = nums[j];
    nums[j] = pivotEle;

    return j;
}

void quickSort(vector<int>& nums, int low, int high) {
    if (low < high) {
        int pivot = partition(nums, low, high);
        quickSort(nums, low, pivot - 1);
        quickSort(nums, pivot + 1, high);
    }
}

void sort(vector<int>& nums) {
    quickSort(nums, 0, nums.size() - 1);
}
```
- Time Complexity: O(n^2), θ(n * log n), Ω(n * log n) <br />
- Space Complexity: O(n), θ(log n), Ω(log n) <br />
- Not Stable and in-place sorting

**Heap Sort**
```C++
void heapify(vector<int>& nums, int i, int n) {
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    int maxPos = i;
    if (left < n && nums[left] > nums[maxPos]) {
        maxPos = left;
    }

    if (right < n && nums[right] > nums[maxPos]) {
        maxPos = right;
    }

    if (i != maxPos) {
        swap(nums[i], nums[maxPos]);
        heapify(nums, maxPos, n);
    }
}

void createHeap(vector<int>& nums) {
    int n = nums.size();
    for (int i = n / 2; i >= 0; i--) {
        heapify(nums, i, n);
    }
}

void sort(vector<int>& nums) {
    createHeap(nums);
    int n = nums.size();
    for (int i = n - 1; i >= 0; i--) {
        swap(nums[i], nums[0]);
        heapify(nums, 0, i);
    }
}

```
- Time Complexity: O(n * log n), θ(n * log n), Ω(n * log n) <br />
- Space Complexity: O(1), θ(1), Ω(1) <br />
- Not Stable and in-place sorting