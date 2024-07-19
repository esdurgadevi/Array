# Array
### 26. Remove Duplicates from Sorted Array
[Leetcode Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
<br>
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.
Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:
Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.

Example 1:
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
#### Code
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        /*int i=0,i1=0;
        nums[i1++]=nums[i];
        for(int j=i+1;j<nums.length;j++)
        {
            if(nums[i]!=nums[j]){
                nums[i1++]=nums[j];
                i=j;
            }
        }
        return i1;*/
        int i=0;
        for(int j=1;j<nums.length;j++)
        {
            if(nums[i]!=nums[j])
            {
                i++;
                nums[i]=nums[j];
            }
        }
        return i+1;
    }
}
```
> Reference : Take U Forward
### 1752. Check if Array Is Sorted and Rotated
[Leetcode Link](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/)
<br>
Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.
There may be duplicates in the original array.
Note: An array A rotated by x positions results in an array B of the same length such that A[i] == B[(i+x) % A.length], where % is the modulo operation.

Example 1:

Input: nums = [3,4,5,1,2]
Output: true
Explanation: [1,2,3,4,5] is the original sorted array.
You can rotate the array by x = 3 positions to begin on the the element of value 3: [3,4,5,1,2].
```java
class Solution {
    public boolean check(int[] nums) {
        int count=0;
        while(true){
            count++;
            int correct=0;
            for(int i=0;i<nums.length-1;i++){
                if(nums[i]>nums[i+1]){
                    rotate(nums);
                    correct=1;
                }
            }
            if(correct==0) return true;
            if(count>=nums.length) return false;
        }
    }
    public void rotate(int[] arr){
        int temp=arr[arr.length-1];
        for(int i=arr.length-1;i>0;i--) arr[i]=arr[i-1];
        arr[0]=temp;
    }
}
```
### 189. Rotate Array
[Leetcode Link](https://leetcode.com/problems/rotate-array/description/)
```java
class Solution {
    public void rotate(int[] nums, int k) 
    {
        k=k%(nums.length);
        for(int i=0;i<k;i++) rotatenums(nums);
    }
    public void rotatenums(int[] nums)
    {
        int temp=nums[nums.length-1];
        for(int i=nums.length-1;i>0;i--) nums[i]=nums[i-1];
        nums[0]=temp;

    } 
}
```
- This is the brute solution but time limit exceed in this case so we discuss the another solution
- In the above solution rotatenums function will rotate the one element by rigth side
- So we call the same function as k time using for loop
- in the rotatenums function in the temp variable we assume the last element of the array
- other by we assign the elements by previous one like we assign the 6th place by 5th element 1st place by oth element
- finally assign oth place by last element that is the temp
#### Other Solution
```java
class Solution {
    public void rotate(int[] nums, int k) 
    {
        k=k%(nums.length);
        reverse(nums,0,nums.length-1);
        reverse(nums,0,k-1);
        reverse(nums,k,nums.length-1);
    }
    public void reverse(int[] nums,int first,int last)
    {
        while(first<last)
        {
            int t=nums[first];
            nums[first]=nums[last];
            nums[last]=t;
            first++;
            last--;
        }

    } 
}
```
- In the above solution first we do k=k%(nums.length) this is because if k is 3 but the length of the array is 2 so the first two times we rotate the array the original array will come so
the third time we rotate array by one element
- example [1,2] k=3
       first time [2,1]
       second time [1,2]
       third time [2,1]
- so firstly we module the k by length of the array.
- then we reverse the string
- then we reverse the first k elements in a string
- then we reverse the remaining elements in the string
- Ex nums = [1 2 3 4 5 6 7] k = 3
       reverse(0,6) = 7,6,5,4,3,2,1
       reverse(0,3-1) = 5,6,7,4,3,2,1
       reverse(3,6) = 5,6,7,1,2,3,4
- Finally we get the rotated array
> Reference [ref..](https://www.youtube.com/watch?v=gmu0RA5_zxs&t=166s) 
### 283. Move Zeroes 
[Leetcode Link](https://leetcode.com/problems/move-zeroes/description/)
<br>
Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

Example 1:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

Example 2:
Input: nums = [0]
Output: [0]
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int index=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]!=0) nums[index++]=nums[i];
        }
        for(int i=index;i<nums.length;i++) nums[i]=0;
        
    }
}
```
- In the above code we will assign all the zeroes to the end and the non-zero elements to the first not changing the order and not using the extra space
- so Initially i assign the variable called index and assign to 0 so move through all the array and check if the element is non zero so i add the element the element to the first.
- Next we assign the remaining elements to the zero.
> Reference [ref..](https://www.youtube.com/watch?v=1PEncepEIoE)
### 268. Missing Number
[Leetcode link](https://leetcode.com/problems/missing-number/)
<br>
Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

Example 1:
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.

Example 2:
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.

Example 3:
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
```java
class Solution {
    public int missingNumber(int[] nums) {
        int sum=0;
        for(int i=0;i<nums.length;i++)
        {
            sum=sum+nums[i];
        }
        return ((nums.length*(nums.length+1))/2)-sum;
    }
}
```
- In the above code i find the total sum for the length of the array and i subract the sum of the array from so we find the missing element.
> Reference : [ref..](https://www.youtube.com/watch?v=YMYVYSWL93w)
### 485. Max Consecutive Ones
[Leetcode link](https://leetcode.com/problems/max-consecutive-ones/)
<br>
Given a binary array nums, return the maximum number of consecutive 1's in the array

Example 1:
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

Example 2:
Input: nums = [1,0,1,1,0,1]
Output: 2
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max=0,c=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]==1)
            {
                c++;
            }
            else
            {
                if(max<c) max=c;
                c=0;
            }
        }
        return max>c?max:c;
    }
}
```
- In the above program we track the current consequtive ones by c and whenever we reach the zero then we check if c is greater than max or not if it we change the max to c
- Finaaly in the eturn satatement final number is one we didnot check the c so in the return statement we check if c is greater or not if greter then i written the c or else i written the max.
> Reference : Take U forward placement series.


 

