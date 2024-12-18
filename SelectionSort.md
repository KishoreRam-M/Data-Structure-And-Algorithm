# Selection Sort

Selection Sort is a simple and intuitive sorting algorithm. It works by dividing the array into two parts: the sorted portion and the unsorted portion. The smallest element is repeatedly selected from the unsorted portion and moved to the sorted portion.

---

## Algorithm Steps

1. Iterate through the array.
2. For each position, find the index of the minimum element in the unsorted portion.
3. Swap the current element with the minimum element found.
4. Repeat until the array is sorted.

---

## Java Code
     class Solution {
  
    public void insertionSort(int arr[]) {
      for(int i=1;i<arr.length;i++)
      {
          int temp = arr[i];
          int j= i-1;
          while(j>=0&& temp < arr[j])
          {
            arr[j+1] =  arr[j];
              j--;
              
          }
          arr[j+1]=temp;
      }
    }
}
