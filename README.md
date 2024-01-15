# 程序设计学习

`Hello World!`


## 怎样解题：  
* 分解问题
* 找到问题的核心、特点      
* 观察示例并寻找模式：尝试自己举例，寻找相似性和规律性    
* 回忆实践经验      
* 创新性解决问题    
* 实践和经验总结


 
## 基础知识  


### 指针
1.指针的定义形式：    
* `int *mat` 表示一个指向整型的指针。在函数中，这个指针可以用来操作一个一维整型数组。（只能将mat当作一维数组使用）    
* `int (*mat)[3]` 表示一个指向包含3个整型元素的数组的指针 mat。（可以将mat当作二维数组使用）  
* `int *mat[3]` 作为形参表示一个包含3个指向整型的指针的数组 mat。（可以将mat当作二维数组使用）

2.*的用法  
* 用于定义指针：`char *p`代表指向字符的指针；`char **p`代表指向字符的指针的指针；`char ***p`代表指向字符的指针的指针的指针，以此类推。  
* 用于解引用：`*p`代表一维解引用；`**p`代表二维解引用，以此类推。


3.良好的指针初始化习惯  
* 如无指向内存先指向NULL  
* 如果需要定义全局数组需要用malloc分配内存空间(头文件#include <stdlib.h>)   
      `int *p=(int*)malloc(sizeof(int));   
       ...   
       free(p);`



## 算法

### 算法设计思想

1.模拟法：  
适用情形：模拟问题的实际情况，常常用于解决那些难以通过传统的数学推导或已知算法解决的问题。  
方法：根据问题的特点和要求来设计相应的模拟过程。  
eg：螺旋顺时针遍历二维数组。 

```

class Solution {
    public int[] spiralArray(int[][] array) {
        if (array == null || array.length == 0 || array[0].length == 0) {
            return new int[0];
        }
        int rows = array.length, columns = array[0].length;
        int[] order = new int[rows * columns];
        int index = 0;
        int left = 0, right = columns - 1, top = 0, bottom = rows - 1;
        while (left <= right && top <= bottom) {
            for (int column = left; column <= right; column++) {
                order[index++] = array[top][column];
            }
            for (int row = top + 1; row <= bottom; row++) {
                order[index++] = array[row][right];
            }
            if (left < right && top < bottom) {
                for (int column = right - 1; column > left; column--) {
                    order[index++] = array[bottom][column];
                }
                for (int row = bottom; row > top; row--) {
                    order[index++] = array[row][left];
                }
            }
            left++;
            right--;
            top++;
            bottom--;
        }
        return order;
    }
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






2.双指针法：指用两个变量在线性结构上遍历而解决的问题，是基于暴力解法的优化。  
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







  ## 常用小技巧：  
1.将字符转换为数字时，使用减去 '0'，而当你需要将数字转换为字符时，使用加上 '0'，运算中不能出现+'0'，字符=字符（要有+'0')。  
2.为防止溢出可善用顺序输入倒序输出。如果是字符串要注意是否将最后一位设为'\0'。     


