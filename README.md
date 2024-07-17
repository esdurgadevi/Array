# Array
### 26. Remove Duplicates from Sorted Array
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

