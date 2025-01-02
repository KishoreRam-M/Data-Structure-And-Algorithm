class Solution {
    public int getSecondLargest(int[] arr) {
        int max = Integer.MIN_VALUE;
        for(int i=0;i<arr.length;i++)
        {
            if(max<arr[i])
            {
                max = arr[i];
            }
        }
      int max2 = Integer.MIN_VALUE;
      for(int i=0;i<arr.length;i++)
      {
          if(max2<arr[i] && arr[i]< max)
          {
              max2 = arr[i];
          }
          
      }
      
      
      int a =Integer.MIN_VALUE;
    if(max2==a)
    {
        return -1 ;
    }
      
      return     max2;
      
      
       }
       
    }
