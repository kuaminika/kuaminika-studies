# Bubble Sort 


## How it goes
Given an unordered array  **Arr**, you do the following:
1. you create a variable **limit** which starts by having a value of  **Arr.length**
1. you iterate **Arr** by comparing **Arr[index]** and **Arr[(index+1)]** while  **limit** >= **index+1**
   1. when iterating and comparing, if  **Arr[index]** > **Arr[(index+1)]**  , you swap them 
   1. make sure that limit is decremented after every iteration
1. you repeat the iteration until **limit** < **index+1**

w
## Coded out
``` javascript
function bubbleSort(arr)
{

    for(let limit = arr.length;limit>0 ; limit-- )
    {
        for(let index =0; (index+1)<=limit;index++ )
        {
            if(arr[index]< arr [index+1]) continue;
            
            swapIndexValues(index,index+1,arr);
        }
        console.log(" pass is done",arr)
    }
}

function swapIndexValues(i,j,arr)
{

    let vali = arr[i];
    let valj = arr[j];
    if(!vali || !valj) return;
    console.log("swapping",vali,valj);
    let tmp = vali;
    arr[i] = valj;
    arr[j] = tmp;
}
```


## Time analysis
Coming soon