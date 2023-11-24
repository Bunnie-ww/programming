# 算法

## 常用小技巧：
1.变量可用来实时跟踪状态。（空间上）   
2.将字符转换为数字时，使用减去 '0'，而当你需要将数字转换为字符时，使用加上 '0'，运算中不能出现+'0'，字符=字符（要有+'0')。  
3.为防止溢出可善用顺序输入倒序输出。   
4.当循环中涉及[i+1]或[i-1]要注意循环条件的设置，防止溢出数组存储空间。     
5.函数遇到return就会退出（无论是否处于循环），善用此性质可以简化情况讨论。  
5.《怎样解题》：  
* 分解问题、归纳问题、整合问题：参数-->(满足）条件-->(改变)变量。
* 找到问题的特点。    
* 观察示例并寻找模式：尝试自己举例，寻找相似性和规律性  
* 多角度思考（从空间等多角度考虑）。    
* 创新性解决问题。    
* 实践和经验总结。    




## 算法设计思想

### 1.模拟法：  
适用情形：模拟问题的实际情况，常常用于解决那些难以通过传统的数学推导或已知算法解决的问题。  
方法：根据问题的特点和要求来设计相应的模拟过程。  
eg：螺旋顺时针遍历二维数组。 
### 2.循环遍历思想：
适用情形：需要对数组中的每个元素执行相似操作的情况。  
方法：for循环。  
eg：循环遍历字符串，通过比较相邻字符来统计重复次数，然后将其压缩成字符和数字的形式。   
### 3.周期性：
适用情形：字符串比对匹配，周期性出现。  
方法：a[j+k]==b[k%n2]作为k++的条件。   
eg：字符串匹配问题。  

## 算法
1.二分法：根据情况不断改变边界，大大提升搜查速度   
eg：搜索旋转排序数组  

