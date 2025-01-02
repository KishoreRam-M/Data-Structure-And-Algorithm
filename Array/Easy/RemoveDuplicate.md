class Solution {
    // Function to remove duplicates from the given array
    public int removeDuplicates(int[] arr) {
       int j=0;
       for(int i=1;i<arr.length;i++)
       {
           if(arr[i]!=arr[j])
           {
               arr[j+1]=arr[i];
               j++;
           }
           
       }
        return j+1;
    }
}
