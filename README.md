# 程序设计学习

`Hello World!`


## 怎样解题  
* 分解问题
* 找到问题的核心、特点      
* 观察示例并寻找模式：尝试自己举例，寻找相似性和规律性    
* 回忆实践经验      
* 创新性解决问题    
* 实践和经验总结


 

## 算法

### 算法设计思想

1.模拟法：  
适用情形：模拟问题的实际情况，常常用于解决那些难以通过传统的数学推导或已知算法解决的问题。  
方法：根据问题的特点和要求来设计相应的模拟过程。  
eg：螺旋顺时针遍历二维数组。 

```

int* spiralOrder(int** matrix, int matrixSize, int* matrixColSize, int* returnSize) {
    int up=0,right=*(matrixColSize)-1,down=matrixSize-1,left=0;
    *returnSize=matrixSize*(*matrixColSize);
    int *m=(int*)malloc(sizeof(int)*(*returnSize));
    int j=0;
    while(left<=right&&up<=down){
        for(int i=left;i<=right;i++){
            m[j++]=matrix[up][i];
        }
        up++;
        for(int i=up;i<=down;i++){
            m[j++]=matrix[i][right];
        }
        right--;
        if(up<=down){
            for(int i=right;i>=left;i--){
                m[j++]=matrix[down][i];
            }
            down--;

        }
        if(left<=right){
            for(int i=down;i>=up;i--){
                m[j++]=matrix[i][left];
            }
            left++;
        }
    }
    return m;
    
}
 


```







### 经典算法

1.二分法：根据情况不断改变边界，大大提升搜查速度。     
eg：搜索旋转排序数组。  

```


int search(int* nums, int numsSize, int target)
{
    int change,left=0,right=numsSize-1,mid;
    
    for(int i=0;i<numsSize-1;i++)//找到中间的最大值并改变边界
    {
        if(nums[i]>nums[i+1])//细节：为防止i+1溢出，i<numsSize-1
        {
             change=i;
            if(nums[change]==target)
             {return i;
              }
            else
             {if(target<nums[0])
                 {left=change+1;}
              else
                 {right=change;}
              break;
             }
             
        }
    }
     while(left<=right)//二分法查找
     {
         mid=(left+right)/2;
         if(nums[mid]==target)
         {
            
             return mid;
             
         }
         if(nums[mid]<target)
         {
            left=mid+1;//left要变，不然当找不到数时会陷入死循环
         }
         if(nums[mid]>target)//相应right也变，满足跳出循环条件
         {
             right=mid-1;
         }
     }
    
     
         return -1;//函数只要遇到return就会终止，因此可以直接输出return=-1作为最后一种情况
     
     
}
    


```


## 典例积累：
### 链表
1. 将链表中的各数放入创建的数组中

```

    while(search){
            *arr=search->val;
            if(search->next){
                search=search->next;
                arr++;
            }
            else{
                break;
            }
        }


```

2. 删除值为val的节点

```

    class Solution {
    public:
        ListNode* deleteNode(ListNode* head, int val) {
            if(head->val==val) return head->next;
            ListNode* pre=head;
            ListNode* cur=pre->next;
            while(cur->next&&cur->val!=val){
                pre=cur;
                cur=cur->next;
            } 
            if(cur)
            pre->next=cur->next;
       
            return head;


        }
    };


```

3. 逆转链表

```
    struct ListNode* trainningPlan(struct ListNode* head) {
    if(head==NULL){
        return head;
    }
    struct ListNode* pre=NULL;//注意尾部的处理
    struct ListNode* cur=head;
    struct ListNode* nex;
    while(cur->next){
        
        nex=cur->next;
        cur->next=pre;
        pre=cur;
        cur=nex;

    }
    cur->next=pre;
    
    return cur;
}

```


4. 升序合并链表

```
struct ListNode* trainningPlan(struct ListNode* l1, struct ListNode* l2) {
    struct ListNode* head=(struct ListNode*)malloc(sizeof(struct ListNode));//注意分配动态内存
    struct ListNode* cur=head;
    if(l1==NULL&&l2==NULL){
        return NULL;
    }
    while(l1&&l2){
        struct ListNode* nex;
        if(l1->val<=l2->val){
            nex=l1;//传递整个节点更好
            l1=l1->next;

        }
        else{
            nex=l2;
            l2=l2->next;
        }
        cur->next=nex;
        cur=cur->next;
    }
    if(l1){
        cur->next=l1;
    }
    if(l2){
        cur->next=l2;
    }
    return head->next;//head是伪头节点，返回head->next
}

```

5. 找到两条链表的交点（追及问题）
```
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB){
        ListNode *cur1=headA;
        ListNode *cur2=headB;
        while(cur1!=cur2)//若cur1与cur2同时指向NULL也可视为cur1==cur2
        {
        cur1=cur1==NULL?headB:cur1->next;
        cur2=cur2==NULL?headA:cur2->next;
        }
        return cur1;
    }
};

```

6. 用哈希表复制随机链表
```
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head == nullptr) return nullptr;
        Node* cur = head;
        unordered_map<Node*, Node*> map;
        
        while(cur != nullptr) {
            map[cur] = new Node(cur->val);
            cur = cur->next;
        }
        cur = head;
        
        while(cur != nullptr) {
            map[cur]->next = map[cur->next];
            map[cur]->random = map[cur->random];
            cur = cur->next;
        }
        
        return map[head];
    }
};

```

***

### 数组
1. 将奇数放在偶数前
```
class Solution {
public:
    vector<int> trainingPlan(vector<int>& actions) {
        int i=0,j=actions.size()-1;
        while(i<j){
            while(i<j&&actions[i]&1){
                i++;
            }
            while(i<j&&!(actions[j]&1)){
                j--;
            }
            swap(actions[i], actions[j]);
        }
        return actions;

    }
};

```

2. 找出和为target的所有连续排列的升序数组
```
class Solution {
public:
    vector<vector<int>> fileCombination(int target) {
        vector<vector<int>> res;
        for(int i=1;i<target;i++){
        double j= (-1 + sqrt(1 + 4 * (2 * target + (long) i * i - i))) / 2;
        if(j==(int)j&&i<j){
            vector<int> arr;
            for(int k=i;k<=j;k++){
                arr.push_back(k);//创建一个未知长度的数组可用push_back
            }
            res.push_back(arr);

        }

    }
    return res;

    }
};

```
3. 返回除了该数外其他数的乘积构成的数组

```
class Solution {
public:
    vector<int> statisticalResult(vector<int>& arrayA) {
        int len=arrayA.size();
        if(len == 0) return {};
        int tmp=1;
        vector<int> arrayB (len, 1);
        arrayB[0]=1;
        for(int i=1;i<len;i++){
            arrayB[i]=arrayB[i-1]*arrayA[i-1];

        }
        for(int i=len-2;i>=0;i--){
            tmp*=arrayA[i+1];
            arrayB[i]*=tmp;

        }
        return arrayB;

    }
};

```


## 常用小技巧： 
1.双指针法：指用两个变量在线性结构上遍历而解决的问题，是基于暴力解法的优化。  
eg：删除有序数组中的重复项。  
```

int removeDuplicates(int* nums, int numsSize) {
    int m=0;
    for(int i=0;i<numsSize;i++)
    {
        if(nums[i]>nums[m])
        {m++;}
        nums[m]=nums[i];
        
    }
    
    return m+1;
    
}


```


2.为防止溢出可善用顺序输入倒序输出（反转）。如果是字符串要注意是否将最后一位设为'\0'。     


## 查漏补缺 


### 指针
1.指针的定义形式：    
* `int *mat`  表示一个指向整型的指针。在函数中，这个指针可以用来操作一个一维整型数组。（只能将mat当作一维数组使用）    
* `int (*mat)[3]`  表示一个指向包含3个整型元素的数组的指针 mat。（可以将mat当作二维数组使用）  
* `int *mat[3]`  作为形参表示一个包含3个指向整型的指针的数组 mat。（可以将mat当作二维数组使用）

2.*的用法  
* 用于定义指针：`char *p` 代表指向字符的指针；`char **p` 代表指向字符的指针的指针；`char ***p` 代表指向字符的指针的指针的指针，以此类推。  
* 用于解引用：`*p` 代表一维解引用；`**p` 代表二维解引用，以此类推。


3.良好的指针初始化习惯  
* 如无指向内存先指向NULL  
* 如果需要定义全局数组需要用malloc分配内存空间(头文件#include <stdlib.h>)

```
       int *p=(int*)malloc(sizeof(int));   
       ...   
       free(p);`


```

4. 越界访问数组的指针不是空指针，且可能导致溢出，因此最好用下标访问数组。  




