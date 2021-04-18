# Merge sort

## How it goes
Given an unordered array  **Arr**, you do the following:
1. Separate the array in two parts. (left and right)
2. You sort both parts 
3. You then merge the two together in a new array 

### Example
 let **Arr** = [8,1,3,10,4,5]
 
 #### step 1:  Separating the array in two parts. (left and right)
- we then have **Arr_left** = [8,1,3] and **Arr_right** = [10,4,5]


 #### step 2:  Sorting both parts
- we then have **Arr_left** = [1,3,8] and **Arr_right** = [4,5,10]


 #### step 3:   merging the two together in a new array 
- from **Arr_left** = [1,3,8] and **Arr_right** = [4,5,10]
- we iterate both and insert the smallest ammount in a new array 
  - we would start with comparing **Arr_left[i-left]** and **Arr_right[i-right]**
    - note: *i-left* and *i-right* are indexes. These indexes are incremented when their respective values are inserted inside the new array 
      - example : if(**Arr_left[i-left]** <**Arr_left[i-right]** )==> then *i-left* is incremented not *i-rght*

## Coded out
- This was coded out in c#
``` csharp
static string[] mergeSort(int startIndex, int endIndex, string [] arr)
    {  
        int diff = (endIndex-startIndex);
         string [] result;
        if(diff<=0)
          {
              result = new string[1];
              result[0]=arr[startIndex];
               return result;
          }
        if(diff == 1)
        {
         result = new string[2];
            string val1 = arr[startIndex];
            string val2 = arr[endIndex];
            if(IsNumericallyGreaterThan(val2, val1))
            {
                result[0] = val1.ToString();
                result[1] = val2.ToString();
                return result;
            }
            result[0] = val2.ToString();
            result[1] = val1.ToString();
            return result;            
        }
        
         result = new string[diff+1];
        int leftEndIndex = startIndex + ((result.Length/2)-1);
        int rightStartIndex = leftEndIndex+1;
        
        
        string [] leftPart = mergeSort(startIndex, leftEndIndex, arr);
       
        
        string [] rightPart = mergeSort(rightStartIndex, endIndex, arr);
       
        
      
        int leftIterationIndex = 0;
        int rightIerationIndex = 0;
        
        int i = 0;
        while(i<result.Length && 
           !(leftIterationIndex>=leftPart.Length ||
            rightIerationIndex>=rightPart.Length  )       
        )
        {
               
            string leftVal = leftPart[leftIterationIndex];
            string rightVal = rightPart[rightIerationIndex];
            
            bool takeLeft = IsNumericallyGreaterThan(rightVal, leftVal);            
            if(takeLeft)
            {
                leftIterationIndex ++;
                result[i] =  leftVal.ToString();
               
            }
            else
            {rightIerationIndex++;
            result[i] = rightVal.ToString(); }
            i++;
        }
  
        bool leftPartIsIterated = (leftIterationIndex) >= leftPart.Length;
        bool rightPartIsIterated = (rightIerationIndex) >= rightPart.Length;
      
        if(leftPartIsIterated)
        {
            Array.Copy(rightPart,rightIerationIndex, result, i,
                       rightPart.Length-rightIerationIndex );
      
                       
            return result;
        }
        if(rightPartIsIterated)
        {
            Array.Copy(leftPart,leftIterationIndex, result,i, 
                        leftPart.Length-leftIterationIndex );
            
            logArr(result);
            return result;
        }
        
        return result;
        
    }

```