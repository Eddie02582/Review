



## 觀念

### p++ and ++p
```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int a[5]={1,2,3,4,5};
    int *p=a;
    *(p++)+=100;  //a[0]+= 100 
    *(++p)+=97;   //a[2]+= 97
    //a[5] = {101,2,100,4,5}
}
```

### 修飾詞
<ul>
    <li>public :成員可以直接使用</li>
    <li>protected:繼承類別准許存取 protected 成員 但外部使用仍然禁止</li>
    <li>private:宣告的函式或變數 只能由自己類別所使用</li>
</ul>






## 程式

### CountBit
題目:給定一個數字判斷2進位有幾個1,利用n & (n - 1)將低位1取出

```c++
#include <iostream>
#include <string>
using namespace std;
int count_bit(int n);
int main()
{    
    cout << count_bit(2020) << endl;
    return 0;
}
int count_bit(int n){
    int count = 0;
    while (n){
        n = n &(n - 1);
        count += 1;  
    }
    return count;    
}
```

### FindZero
題目:一個陣列只包含1,0並且由1,0排序,找出0的位置

分析:一個反向的binary search,因為是要找第一個0,所以需要回傳左邊的指針,


```c++
#include <string>
#include <iostream>
using namespace std ; 
int FindZero (int arr[],int size);

int main()
{
    int arr1 [] = {1,1,1,1,1,1,1,1,1,1,0,0,0,0,0,0,0,0,0,0};
    cout << FindZero (arr1,20) <<endl; 

    int arr2 [] = {1,1,1,1};
    cout << FindZero (arr2,4)<<endl;

    int arr3 []  = {0,0};
    cout << FindZero (arr3,2)<<endl;

    int arr4 []  = {0};
    cout << FindZero (arr4,1)<<endl;

    int arr5 []  = {1,0,0};
    cout << FindZero (arr5,3)<<endl;

}

//user reverser function
int FindZero (int arr[],int size)
{  
    int left  = 0;
    int right = size - 1;  
    while(left < right){        
        int mid = left + (right - left)/2;        
        if(arr[mid] == 0)
            right = mid;        
        else if(arr[mid] == 1)
            left = mid + 1;        
    } 
    if (arr[left] == 0)
        return left;
    return -1;
}
```


```c++
int FindZero(int arr[],int size)
{  
    int left  = 0;
    int right = size - 1;  
    int target = 0;
    while(left <= right){        
        int mid = left + (right - left)/2;    
        if (arr[mid] > target)
            left = mid + 1; 
        else
            right = mid + 1 ;              
    } 
    if (left >= size || arr[left] != target) {
            return -1;
    }
    return left;
}
```
### Print Number Exclude
印出0~500不包含exclue的數字


```c++
#include <iostream>
#include <string>
using namespace std;

int print_exclude(int arr[],int size);

int main()
{
    int a[20]  = {39, 42, 60, 92, 115, 133, 157, 188, 207, 230, 236, 255, 288, 319, 338, 354, 412, 424, 443, 454};
    print_exclude(a,20);
    return 0;
}
int print_exclude(int *arr,int size){
    
    int *ptr = arr;
    for(int i = 0;i <= 500;i++){
        if (i == *ptr)
            ptr++;
        else
            cout << i << " ";
    }
    return 0;
    
}
```
### Print Number Exclude II
印出1~199不包含exclue的數字

```c++
#include <iostream>
#include <string>
using namespace std;

int print_exclude(int *arr,int size,int b);


int main()
{
    int a[20]  = {39, 42, 60, 92, 115, 133, 157, 188, 207, 230, 236, 255, 288, 319, 338, 354, 412, 424, 443, 454};
    print_exclude(a,20,1);
    return 0;
}

int print_exclude(int *arr,int size,int b){
    int rangeL = 100 *b;
    int rangeH = 99 + 100 *b ;
    int *ptr = arr;
    
    while (*ptr < rangeL)
        ptr++;
    
    for (int i = rangeL;i <= rangeH;i++){
        if (i == *ptr)
            ptr++;
        else
            cout << i << " ";
    }
    return 0;    
}
```

### Sort Function

### bubble sort
```c++
void bubbleSort (int arr[],int size){
    int temp = 0;
    for(int i = 0;i < size;i++){
        bool bSwap = false;
        for(int j = 0; j < size - i - 1;j++){
            if(arr[j] > arr[j + 1]){
                temp = arr[j + 1];
                arr[j + 1] = arr[j];
                arr[j] = temp;
                bSwap = true;
            }
        }
        if(!bSwap)
            break;
    }
}
```

### MergeSort

```c++
void mergeSort (int arr[],int front,int end){
    if (front < end)
    {
        int mid = front  + (end  - front)/2;
        mergeSort(arr,front,mid);
        mergeSort(arr,mid + 1,end);
        merge(arr,front,mid,end);
    }
}

void merge(int arr[], int front, int mid, int end) { 
    int n1 = mid - front + 1;
    int n2 = end  - mid;
    int L[n1], R[n2];

    for (int i = 0; i < n1; i++)
        L[i] = arr[front + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid+ 1 + j];

    //merge
    int i, j, k;
    i = 0;
    j = 0;
    k = front;
    while (i < n1 && j < n2){
        if(L[i] < R[j]){
            arr[k++] = L[i++];           
        }
        else{
            arr[k++] = R[j++];      
        }
  
    }
    while (i < n1 ){
        arr[k++] = L[i++];       
    } 
    while (j < n2 ){
        arr[k++] = R[j++];  
    } 
}
```




### Middle of the Linked List










