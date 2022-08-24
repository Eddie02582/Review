



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

### linked list vs array

<a href =  "https://medium.com/@maggieliao.cm04g/%E8%B3%87%E7%B5%90%E8%88%87%E6%BC%94%E7%AE%97%E6%B3%95%E7%AD%86%E8%A8%98-1-linked-list-%E8%88%87-array-%E6%96%BCo-n-%E4%B9%8B%E5%B7%AE%E7%95%B0%E6%AF%94%E8%BC%83-badbf08b17ce">Linked list  vs Array</a>



### 問輸出是多少?(MTK)
```c++
#include <stdio.h>

#define SWAP(a,b) tmp = a; a = b ; b= tmp;

int main()
{
    int a = 10;
    int b = 20;
    int tmp = 0;
    int n = 6;
    
    if(n > 6)
    SWAP(a,b);
    
    printf("%d %d %d",tmp,a,b);
        
    return 0;
}
```
因為SWAP並沒有用括號起來實際程式碼
```c++
    int a = 10;
    int b = 20;
    int tmp = 0;
    int n = 6;
    if(n > 6)
         tmp = a;
    a = b ; 
    b= tmp;     
```
所以輸出為 0,20,0


### 問輸出是多少?(MTK)

```c++
int main()
{
    int arr[8] = {0,1,2,3,4,5,6,7};
    int* ptr1 = &arr[0];
    char* ptr2 = (char*) ptr1;
    printf("%d",*ptr2);
    
    return 0;
}
```
ptr1 為arr[0]的address,ptr2 為ptr1的address,所以*ptr2  等於arr[0]的address取値,因此書出為0


## Bitwise Operation

### clearBit
```c++
int clearBit(int n, int k)
{
    return (n & (~(1 << (k - 1))));
}
```

### setBit
```c++
int setBit(int n, int k)
{
    return (n | (1 << (k - 1)));
}
```

### Toggle a bit
```c++
int toggleBit(int n, int k)
{
    return (n ^ (1 << (k - 1)));
}
```

### print kth  bit

```c++
int toggleBit(int n, int k)
{
    return （n >> k）&1;
    //or  return ((1 << 8) & n) ? 1 :0;
}
```


### remove last 1 bit
n = n & (n - 1)

### 取得最高位在哪裡
```c++
unsigned int countBits(unsigned int n){
    int count = 0;    
    while (n){
        n >>= 1; 
        ++count;
    }
    return count;    
}
```

## Link List
```
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};
 ```

### Middle of the Linked List(Leetcode 876)
```c++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *first = head;
        ListNode *slow = head;
        while (first != nullptr && first->next != nullptr){
            first = first->next->next;
            slow = slow->next;
        }
        return slow;
    }
};
```

### 找出前半段的最大值
```c++
    int middleNode(ListNode* head) {
        ListNode *first = head;
        ListNode *slow = head;
        int max = head.val();
        while (first != nullptr && first->next != nullptr){
            if (slow->val > max)         
                max = slow->val;            
            first = first->next->next;
            slow = slow->next;
        }
        return max;
    }
```

### Reverse LinkedList
```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = NULL;
        ListNode* post = NULL;
        while (head){
            post = head->next;
            head->next = prev;            
            prev = head;
            head = post;   
        }
        return prev;
    }
};
```

## Other程式


### Number of 1 Bits(leetcode 191)
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
### is Power Of Two(leetcode 232)

```c++
    bool isPowerOfTwo(int n) {
        return n > 0 && not (n & n - 1)    
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
## implent strcmp

```c
#include <stdio.h>
#include <string.h>
int strcmp(const char *str1, const char *str2)
{
    if(str1 == str2)
        return 0;
        
    while(str1 != NULL && str2 != NULL){
        int n1 = (int)*str1++;
        int n2 = (int)*str2++;
        /*if (n1 != n2){
            return n1 - n2;
        }*/
        if(n1 > n2)
            return 1;
        else if(n1 < n2)
            return -1;
    }
   
    if(str1 != NULL){
        return 1;
    }
    else if (str2 != NULL){
        return -1;
    }
    return 0;
}

int main()
{
    char *a = "aBcDeF";
    char *b = "AbCdEf";
    char *c = "aacdef";
    char *d = "aBcDeF";  
    printf("strcmp(a, b) : %d\n", strcmp_(a, b));
    printf("strcmp(a, c) : %d\n", strcmp_(a, c));
    printf("strcmp(a, d) : %d\n", strcmp_(a, d));   
    return 0;
}
```

c++必須宣告const

```c++
int main()
{
    const char *a = "aBcDeF";
    const char *b = "AbCdEf";
    const char *c = "aacdef";
    char d[] = "aBcDeF";
    
    
    printf("strcmp(a, b) : %d\n", strcmp_(a, b));
    printf("strcmp(a, c) : %d\n", strcmp_(a, c));
    printf("strcmp(a, d) : %d\n", strcmp_(a, d));   
    return 0;
}
```

###費氏數列
遞回
```c++
int Fibonacci(int n){
    if(n == 1)
        return 1;
    if(n == 0)
        return 0;       
    else
        return Fibonacci(n - 1) + Fibonacci(n - 2) ;
}
```


iterative 
```c++
int fib(int n){
    if (n < 2)
        return n;
    int a = 1, b = 0, c = 0;
    for (int i = 2; i <= n; i++) {
        //f(n) = f(n-1) +f(n-2)
        c = a + b;
        b = a;
        a = c;
    }           
    return c;
}
```
or use array
```c++
int fib(int n){
    int f[n + 1] = {0};
    f[1] = 1;  
    for (int i = 2; i <= n; i++) {
        f[n] = f[n-1] +f[n-2]; 
    }           
    return f[n];
}
```






### Print Number Exclude(群聯三題)
給一個int a[20]已排序的陣列，請寫一個function(a, size)能印出0~500的數字，且不包含a陣列內的元素，請用最少的時間和空間複雜度完成


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
### Print Number Exclude II(群聯三題)
```
給一個int a[20]已排序的陣列，請寫一個function(a, size, b)能依照參數b(b = 0~4)印出該區間的數字，且不包含a陣列內的元素
b = 0, 印出0~99
b = 1, 印出100~199
```

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

### find a + b +c = 10
```c++
int threeSum(int n)
{
    int count = 0;
    for (int i = 1; i <= n - 2 ;i++){
        for(int j = 1;j <= n - i - 1;j++)
        {
          printf("%d + %d + %d = %d\n",i,j,n -i-j,n);
          count ++;
        }
    }
    return count;
}
```

考慮不重複(Leetcode 3Sum 簡單吧)
```c++
int threeSum(int n)
{
    int count = 0;
    for (int  i = 1; i <= n/3 ;i++){
        int l = i,r = n - 2 * i;
        while (l <= r){
           printf("%d + %d + %d = %d\n",i,l,r,n);
           l += 1;
           r -= 1;
        }
    }
    
    return count;
}
```
result
```
1 + 1 + 8 = 10
1 + 2 + 7 = 10
1 + 3 + 6 = 10
1 + 4 + 5 = 10
2 + 2 + 6 = 10
2 + 3 + 5 = 10
2 + 4 + 4 = 10
3 + 3 + 4 = 10
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

### prefix(MTK)
給定一個prefix(第一行輸入)，輸出不包含此prefix的string


```c++
void check_prefix(string input, string prefix) {
    
    string sim_input = input.substr(0, prefix.length());
    if (sim_input != prefix) {
        cout << input << "\n";
            return;
    }
}
```

```c++

void check_prefix(string input, string prefix) {
    if(prefix.length() > input.length())
        return;
    for(int i = 0; i < prefix.length();i++)
    {
        if(prefix[i] != input[i])
            return;
    }
    cout << input << endl;
    return;    
}
```









