1. method but not effecient 
class Solution {
    public static int largest(int[] arr) {
        
        for(int i=1;i<arr.length;i++)
        {
            int temp = arr[i];
            int j =i-1; 
            while(j>=0 && temp<arr[j])
            {
                arr[j+1]=arr[j];
                j--;
            }
            arr[j+1]=temp;
        }
         return arr[arr.length-1];
    }
}


2. efffecient method
  class Solution {
    public static int largest(int[] arr) {
        int max = Integer.MIN_VALUE;
        for(int i=0;i<arr.length;i++)
        {
            if(max<arr[i])
            {
                max = arr[i];
            }
        }
        return max;
    }
}


