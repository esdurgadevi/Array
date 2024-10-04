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
### 1. Two Sum
[Leetcode link](https://leetcode.com/problems/two-sum/description/)
<br>
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result=new int[2];
        Map <Integer,Integer> map = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            if(map.containsKey(target-nums[i]))
            {
                result[0]=map.get(target-nums[i]);
                result[1]=i;
                return result;
            }
            map.put(nums[i],i);
        }
        return result;
    }
}
```
- Using Hash map i solve the above problem.
### 75. Sort Colors
[LeetCode link](https://leetcode.com/problems/sort-colors/description/)
<br>
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.
You must solve this problem without using the library's sort function.

Example 1:
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]

Example 2:
Input: nums = [2,0,1]
Output: [0,1,2]
```java
class Solution {
    public void sortColors(int[] nums) {
        int s=0;
        for(int i=1;i<nums.length;i++)
        {
            for(int j=0;j<nums.length-i;j++)
            {
                if(nums[j]>nums[j+1])
                {
                    int t= nums[j];
                    nums[j]=nums[j+1];
                    nums[j+1]=t;
                    s=1;
                }
            }
            if(s==0) break;
        }
    }
}
```
- I use bubble sort to sort the array elements.
#### Other Method 
```java
class Solution {
    public void sortColors(int[] nums) {
        int low=0,mid=0,high=nums.length-1;
        while(mid<=high)
        {
            if(nums[mid]==0)
            {
                int temp=nums[low];
                nums[low]=nums[mid];
                nums[mid]=temp;
                low++;
                mid++;
            }
            else if(nums[mid]==1) mid++;
            else 
            {
                int temp=nums[high];
                nums[high]=nums[mid];
                nums[mid]=temp;
                high--;
            }
        }
    }
}
```
**Algorithm : Dutch National Flag**
- This algorithm consist of three pointers low mid high so low pointer decide the 0's place high pointer decide the 2's place mid pointer will check if the nums[i] is 0 or 1 or 2.
- This algorithm gives the small time complexity.
> Reference : Take U orward A2Z series. video 22
### 169. Majority Element
[Leetcode link](https://leetcode.com/problems/majority-element/description/)
<br>
Given an array nums of size n, return the majority element.
The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

Example 1:
Input: nums = [3,2,3]
Output: 3

Example 2:
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```java
class Solution {
    public int majorityElement(int[] nums) {
        for(int i=0;i<nums.length;i++)
        {
            int c=1;
            for(int j=i+1;j<nums.length;j++)
            {
                if(nums[i]==nums[j]) c++;
            }
            if(c>(nums.length/2)) return nums[i];
        }
        return 0;
    }
}
```
- Also this is a not a optimal solution this is a brute force solution.
#### Other method
```java
class Solution {
    public int majorityElement(int[] nums) {
        int element=nums[0],count=1;
        for(int i=1;i<nums.length;i++)
        {
            if(count==0)
            {
                element=nums[i];
                count=1;
            }
            else if(nums[i]==element) count++;
            else count--;
        }
        return element;
    }
}
```
**Algorithm : moore's Algorithm**
- This algorithm states that we first assign the element and that element count by 1.
- Then iterate over the loop if we get the same element then increase the count otherwise decrease it.
- Whenever we reah the count by zero then we change the element by the loops iteration element and the count by 1.
- finally we return the element.
- This is possible because n/2 times the element is appear so whenever we get the small small sub array that array containe the element surely.
> Reference : Take U orward A2Z series. video 23
### 2392. Find the number that appear ones
[Leetcode link](https://leetcode.com/problems/single-number/)
<br>
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.
You must implement a solution with a linear runtime complexity and use only constant extra space.

Example 1:
Input: nums = [2,2,1]
Output: 1

Example 2:
Input: nums = [4,1,2,1,2]
Output: 4

Example 3:
Input: nums = [1]
Output: 1
```java
class Solution {
    public int singleNumber(int[] nums) {
        Arrays.sort(nums);
        for(int i=0;i<nums.length;i=i+2)
        {
            if(i+1>=nums.length) return nums[i];
            if(nums[i]!=nums[i+1]) return nums[i];
        }
        return 0;
    }
}
```
- Find single element in a array other elements are twice in a array there is only one element single in a array.
- so i sort the array initially.
- then i iterate the loop by +2.
- If the first and the second is not equal then we return that element in the other hand we check if i+1 is exceed the array index then that element is the single element say for example
after sorting the some array the array become 1 1 2 2 4 the 4 is single element so that is also a last element so ireturn that element.
### 53. Maximum Subarray
[Leetcode link](https://leetcode.com/problems/maximum-subarray/description/)
<br>
Given an integer array nums, find the subarray with the largest sum, and return its sum.

Example 1:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.

Example 2:
Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.

Example 3:
Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum=0,max=Integer.MIN_VALUE;
        for(int i=0;i<nums.length;i++)
        {
            if(sum<0) sum=0;
            sum=sum+nums[i];
            if(max<sum) max=sum;
        }
        return max;
    }
}
```
**Algorithm : Kadane's Algorithm**
- In the above program uses the kadanes's Algorithm.
- initialize sum to zero and max to the integers minimum values.
- iterate through all the elements add the element to the sum.
- Whenever sum is less than zero then we re initialize to zero and each time we check if max<sum if it is then set max by sum.
- Finally return the max.
> Reference : Take U orward A2Z series. video 24.

### 2149. Rearrange Array Elements by Sign
[Leetcode link](https://leetcode.com/problems/rearrange-array-elements-by-sign/)
<br>
You are given a 0-indexed integer array nums of even length consisting of an equal number of positive and negative integers.
You should return the array of nums such that the the array follows the given conditions:
- Every consecutive pair of integers have opposite signs.
- For all integers with the same sign, the order in which they were present in nums is preserved.
- The rearranged array begins with a positive integer.
Return the modified array after rearranging the elements to satisfy the aforementioned conditions.

Example 1:

Input: nums = [3,1,-2,-5,2,-4]
Output: [3,-2,1,-5,2,-4]
Explanation:
The positive integers in nums are [3,1,2]. The negative integers are [-2,-5,-4].
The only possible way to rearrange them such that they satisfy all conditions is [3,-2,1,-5,2,-4].
Other ways such as [1,-2,2,-5,3,-4], [3,1,2,-2,-5,-4], [-2,3,-5,1,-4,2] are incorrect because they do not satisfy one or more conditions.  

Example 2:
Input: nums = [-1,1]
Output: [1,-1]
Explanation:
1 is the only positive integer and -1 the only negative integer in nums.
So nums is rearranged to [1,-1].
```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int[] result=new int[nums.length];
        int p=0,n=1;
        for(int i=0;i<nums.length;i++)
        {
            if(nums[i]>0) 
            {
                result[p]=nums[i];
                p=p+2;
            }
            else 
            {
                result[n]=nums[i];
                n=n+2;
            }
        }
        return result;
    }
}
```
- In the above program equal no of positive and negative elements will there we rearrang the elements in zig zag order that is + - + - + - +
- So From the ex positives are in the place of 0,2,4,... and negatives are in the place of 1,3,5,...
- So p intialize to zero then n initialize to 1 iterate all the elements and check the element is positive are not.
- If the element is positive then add the element using p and iterate the p by two place [p=0 after add the element p=0+2=2]
- Same for negative.
> Reference : Take U forward video 26.
### 31. Next Permutation
[Leetcode link](https://leetcode.com/problems/next-permutation/)
<br>
A permutation of an array of integers is an arrangement of its members into a sequence or linear order.
For example, for arr = [1,2,3], the following are all the permutations of arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.
Given an array of integers nums, find the next permutation of nums.

The replacement must be in place and use only constant extra memory.

Example 1:
Input: nums = [1,2,3]
Output: [1,3,2]

Example 2:
Input: nums = [3,2,1]
Output: [1,2,3]

Example 3:
Input: nums = [1,1,5]
Output: [1,5,1]

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int index=-1;
        for(int i=nums.length-1;i>0;i--){
            if(nums[i]>nums[i-1]){
                index=i-1;    
                break;
            }
        }
        if(index==-1) rev(nums,0,nums.length-1);
        else{
            for(int i=nums.length-1;i>=index;i--){
                if(nums[i]>nums[index]){
                    int temp=nums[i];
                    nums[i]=nums[index];
                    nums[index]=temp;
                    break;
                }
            }rev(nums,index+1,nums.length-1);
        }
         
    }
    public void rev(int[] nums,int start,int end){
        while(start<end){
            int temp=nums[start];
            nums[start]=nums[end];
            nums[end]=temp;
            start++;
            end--;
        }
    }
}
```
- next permutation meaning the next imediate permutation.
- Say for example the array contain [2,1,3] ( total permutation 3! = 6 )
- Permutation of the above array is [1,2,3] [1,3,2] [2,1,3] [2,3,1] [3,1,2] [3,2,1]
- So the answer is [2,3,1] If the given array is last of it like [3,2,1] then the answer is first one [1,2,3]
- so we acheive this answer what we do is we find the first decreasing index from the last all are in increasing sequence so first we find the decreasing index.
- next we swap the index number to next immediate big number Ex [2,1,5,4,3,0,0] 0<0<3<4<5 but 5>1 so number one place is decreasing index.
- We swap one to any of the number that is greater than one so in the example greater than one is 5,4,3 but we get 3 so we get next immediate greater number.
- After swap the two numbers we get [2,3,5,4,1,0,0] after swaping that also in increasing order so we set the first two place.
- After set the place then reverse the rmainning elements so we get the next permutation [2,3,0,0,1,4,5].
> Reference : Take U forward video 27.
### Leaders in array
[geeksforgeeks link](https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=leaders-in-an-array)
<br>
Given an array arr of n positive integers, your task is to find all the leaders in the array. An element of the array is considered a leader if it is greater than all the elements on its right side or if it is equal to the maximum element on its right side. The rightmost element is always a leader.

Examples
Input: n = 6, arr[] = {16,17,4,3,5,2}
Output: 17 5 2
Explanation: Note that there is nothing greater on the right side of 17, 5 and, 2.
Input: n = 5, arr[] = {10,4,2,4,1}
Output: 10 4 4 1
Explanation: Note that both of the 4s are in output, as to be a leader an equal element is also allowed on the right. side
Input: n = 4, arr[] = {5, 10, 20, 40} 
Output: 40
Explanation: When an array is sorted in increasing order, only the rightmost element is leader.
Input: n = 4, arr[] = {30, 10, 10, 5} 
Output: 30 10 10 5
Explanation: When an array is sorted in non-increasing order, all elements are leaders.
#### Brute Force Opproach
```java
class Solution {
    // Function to find the leaders in the array.
    static ArrayList<Integer> leaders(int n, int arr[]) {
        // Your code here
        ArrayList<Integer> result = new ArrayList<>();
        for(int i=0;i<n;i++)
        {
            int flag=0;
            for(int j=i+1;j<n;j++)
            {
                if(arr[i]<arr[j])
                {
                    flag=1;
                    break;
                }
            }
            if(flag==0) result.add(arr[i]);
        }
        return result;
    }
}
```
#### Optimal Opproach
```java
class Solution {
    // Function to find the leaders in the array.
    static ArrayList<Integer> leaders(int n, int arr[]) {
        // Your code here
        ArrayList<Integer> result = new ArrayList<>();
        int max=Integer.MIN_VALUE;
        for(int i=n-1;i>=0;i--)
        {
            if(arr[i]>max) 
            {
                max=arr[i];
                result.add(arr[i]);
            }
        }
        Collections.reverse(result);
        return result;
    }
}
```
### 128. Longest Consecutive Sequence
[Leetcode link](https://leetcode.com/problems/longest-consecutive-sequence/)
<br>
Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.
You must write an algorithm that runs in O(n) time.

Example 1:
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        HashSet<Integer> set=new HashSet<Integer>();
        for(int num:nums) set.add(num);
        int max_sequence=0;
        for(int i=0;i<nums.length;i++){
            int current_element=nums[i];
            int current_count=1;
            if(!set.contains(current_element-1)){
                while(set.contains(current_element+1)){
                    current_element++;
                    current_count++;
                }max_sequence=Math.max(current_count,max_sequence);
            }
        }
        return max_sequence;
    }
}
```
- In this code create a hashset to store the elements without any reputation.
- Then initialize the max_sequence by zero
- Then iterate over the array each element check if that element is the least element. if the element is the low element then in the while loop chech the next element and also increas
the count by one whenever the next element in the set.
- After completing the while loop then initialize the max_sequence to max(current_count,max_sequence) then return the max_sequence.
> [Reference :](https://www.youtube.com/watch?v=sHrb6phW3IA)
### 1636. Sort Array by Increasing Frequency
[leetcode link](https://leetcode.com/problems/sort-array-by-increasing-frequency/?envType=daily-question&envId=2024-07-23)
<br>
Given an array of integers nums, sort the array in increasing order based on the frequency of the values. If multiple values have the same frequency, sort them in decreasing order.
Return the sorted array.

Example 1:
Input: nums = [1,1,2,2,2,3]
Output: [3,1,1,2,2,2]
Explanation: '3' has a frequency of 1, '1' has a frequency of 2, and '2' has a frequency of 3.

Example 2:
Input: nums = [2,3,1,3,2]
Output: [1,3,3,2,2]
Explanation: '2' and '3' both have a frequency of 2, so they are sorted in decreasing order.

Example 3:
Input: nums = [-1,1,-6,4,5,-6,1,4,1]
Output: [5,-1,4,4,-6,-6,1,1,1]

Constraints:
1 <= nums.length <= 100
-100 <= nums[i] <= 100

```java
class Solution {
    public int[] frequencySort(int[] nums) {
        int[] result = new int[nums.length];
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<nums.length;i++)
        {
            int count=1;
            for(int j=i+1;j<nums.length;j++)
            {
                if(nums[i]==nums[j] && nums[i]!=-200)
                {
                    count++;
                    nums[j]=-200;
                }
            }
            if(nums[i]!=-200) map.put(nums[i],count);
        }
        int[] newnum = new int[200];
        int[] freq = new int[200];
        int index=0;
        for(int i=0;i<nums.length;i++) 
        {
            if(nums[i]!=-200)
            {
                newnum[index]=nums[i];
                freq[index++]=map.get(nums[i]);
            }
        }
        for(int i=1;i<index;i++)
        {
            int swap=0;
            for(int j=0;j<index-i;j++)
            {
                if(freq[j]>freq[j+1])
                {
                    int t1=freq[j];
                    freq[j]=freq[j+1];
                    freq[j+1]=t1;
                    int t2=newnum[j];
                    newnum[j]=newnum[j+1];
                    newnum[j+1]=t2;
                    swap=1;
                }
                else if(freq[j]==freq[j+1])
                {
                    if(newnum[j]<newnum[j+1])
                    {
                        int t1=freq[j];
                        freq[j]=freq[j+1];
                        freq[j+1]=t1;
                        int t2=newnum[j];
                        newnum[j]=newnum[j+1];
                        newnum[j+1]=t2;
                        swap=1;
                    }
                }
            }
            if(swap==0) break;
        }
        int index1=0;
        for(int i=0;i<index;i++)
        {
            for(int j=0;j<freq[i];j++)
            {
                result[index1++]=newnum[i];
            }
        }
        return result;
    }
}
```
### 1365. How Many Numbers Are Smaller Than the Current Number
[Leetcode link](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/)
<br>
Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i]. Return the answer in an array.

Example 1:
Input: nums = [8,1,2,2,3]
Output: [4,0,1,1,3]
Explanation: 
For nums[0]=8 there exist four smaller numbers than it (1, 2, 2 and 3). 
For nums[1]=1 does not exist any smaller number than it.
For nums[2]=2 there exist one smaller number than it (1). 
For nums[3]=2 there exist one smaller number than it (1). 
For nums[4]=3 there exist three smaller numbers than it (1, 2 and 2).

Example 2:
Input: nums = [6,5,4,8]
Output: [2,1,0,3]

Example 3:
Input: nums = [7,7,7,7]
Output: [0,0,0,0]

```java
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {
        int[] result=nums.clone();
        Arrays.sort(result);
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<result.length;i++) map.putIfAbsent(result[i],i);
        for(int i=0;i<nums.length;i++) result[i]=map.get(nums[i]);
        /*Arrays.sort(nums);
        int[] result = new int[nums.length];
        for(int i=0;i<nums.length;i++){
            int count=0;
            for(int j=0;j<nums.length;j++){
                if(nums[i]>nums[j]) count++;
            }
            result[nums.length-i-1]=count;
        }*/
        return result;
    }
}
```
- In this code we find the result array by iterate all the elements in nums and count the number of elements which are smaller than the current element and store the count to result array(commant Code)
- Other way is create a result array and copy the nums element to that result array
- After we sort the array we know first element is the smallest element no other small element did not in the array after sorting so first element have 0 second element have 1 in deeper we think that is index.
- So in the hashmap i put the value if the key is already did not present in the map (putifAbsent)
- After put all the elements we get the count of each original element by nums array.
> [Reference](https://www.youtube.com/watch?v=CKSdHsQyPYk)
### 57. Insert Interval
[Leetcode link](https://leetcode.com/problems/insert-interval/)
<br>
You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.
Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).
Return intervals after the insertion.
Note that you don't need to modify intervals in-place. You can make a new array and return it.

Example 1:
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

Example 2:
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        int i=0;
        List<int[]> arr = new ArrayList<int[]>();
        while(i<intervals.length && intervals[i][1]<newInterval[0]){
            arr.add(intervals[i]);
            i++;
        }
        while(i<intervals.length && intervals[i][0]<=newInterval[1]){
            newInterval[0]=Math.min(intervals[i][0],newInterval[0]);
            newInterval[1]=Math.max(intervals[i][1],newInterval[1]);
            i++;
        }
        arr.add(newInterval);
        while(i<intervals.length){
            arr.add(intervals[i]);
            i++;
        }
        int[][] ans = new int[arr.size()][2];
        for(int j=0;j<arr.size();j++){
            ans[j][0]=arr.get(j)[0];
            ans[j][1]=arr.get(j)[1];
        }
        return ans;
        
    }
}
```
- In this code we return the new 2D array that array will insert the new array without overlapping.
- We reduce in three sub problems.
- First set will b non overlaped and the second will be overlaped and the third will be no overlaped.
- So What we do is whenever the newarray[0] is less than the array[0][1] then no over laping occur.
- So we easily add that row to the list
- Now in overlaping loop.
- and last non overlaping loop.
- we use list because it allocate memory dynamically but array not.
<img width="441" alt="image" src="https://github.com/user-attachments/assets/060653c6-5ce3-46ba-93d2-4e2dd1adcaeb">
 
> [Reference](https://www.youtube.com/watch?v=xxRE-46OCC8)
### 54. Spiral Matrix
[Leetcode link](https://leetcode.com/problems/spiral-matrix/)
Given an m x n matrix, return all elements of the matrix in spiral order.
 
Example 1:
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]

Example 2:
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        int top=0,bottom=(matrix.length)-1,left=0,right=(matrix[0].length)-1;
        while(top<=bottom && left<=right)
        {
            for(int i=left;i<=right;i++) list.add(matrix[top][i]);
            top++;
            for(int i=top;i<=bottom;i++) list.add(matrix[i][right]);
            right--;
            if(top<=bottom){
                for(int i=right;i>=left;i--) list.add(matrix[bottom][i]);
                bottom--;
            }
            if(left<=right){
                for(int i=bottom;i>=top;i--) list.add(matrix[i][left]);
                left++;
            }
        }
        return list;
        
    }
}
```
> Reference : takr u forward
### 2134. Minimum Swaps to Group All 1's Together II
[Leetcode link](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii/description/?envType=daily-question&envId=2024-08-02)
<br>
A swap is defined as taking two distinct positions in an array and swapping the values in them.
A circular array is defined as an array where we consider the first element and the last element to be adjacent.
Given a binary circular array nums, return the minimum number of swaps required to group all 1's present in the array together at any location.

Example 1:
Input: nums = [0,1,0,1,1,0,0]
Output: 1
Explanation: Here are a few of the ways to group all the 1's together:
[0,0,1,1,1,0,0] using 1 swap.
[0,1,1,1,0,0,0] using 1 swap.
[1,1,0,0,0,0,1] using 2 swaps (using the circular property of the array).
There is no way to group all 1's together with 0 swaps.
Thus, the minimum number of swaps required is 1.

Example 2:
Input: nums = [0,1,1,1,0,0,1,1,0]
Output: 2
Explanation: Here are a few of the ways to group all the 1's together:
[1,1,1,0,0,0,0,1,1] using 2 swaps (using the circular property of the array).
[1,1,1,1,1,0,0,0,0] using 2 swaps.
There is no way to group all 1's together with 0 or 1 swaps.
Thus, the minimum number of swaps required is 2.

Example 3:
Input: nums = [1,1,0,0,1]
Output: 0
Explanation: All the 1's are already grouped together due to the circular property of the array.
Thus, the minimum number of swaps required is 0.

Constraints:
1 <= nums.length <= 105
nums[i] is either 0 or 1.

```java
class Solution {
    public int minSwaps(int[] nums) {
        int total = 0;
        for(int i=0;i<nums.length;i++) if(nums[i]==1) total++;
        int l = 0;
        int window = 0,max_one = 0;
        for(int r=0;r<2*nums.length;r++){
            if(nums[r%nums.length]==1) window++;
            if(r-l+1>total){
                window=window-nums[l%nums.length];
                l++;
            }
            max_one = Math.max(max_one,window);
        }
        return total-max_one;
    }
}
```
- The step is to find the sub array with maximum ones
- So how we do this first we find the total number of ones in the array.
- Whenever we get the sub array that array size is must be the count of ones.
- So from the sliding window pattern first we assign l=0 and iterate through the loop
- whenever the r-l+1 that is our sub array is cross the limit of the total ones count.
- then we decrease the window by the left pointer positions value.
- then increse the left pointer by one
- for each iteration we find the max ones by max(maxones and window ones)
- then we return the total ones by the the max_ones.
- Basically the max_ones represents the sub array of size total ones that contain the maximum ones in it.
> [Reference](https://www.youtube.com/watch?v=BueoreUIkcE)
### 1460. Make Two Arrays Equal by Reversing Subarrays
[Leetcode link](https://leetcode.com/problems/make-two-arrays-equal-by-reversing-subarrays/?envType=daily-question&envId=2024-08-03)
<br>
*Array Hash Table Sorting*
You are given two integer arrays of equal length target and arr. In one step, you can select any non-empty subarray of arr and reverse it. You are allowed to make any number of steps.
Return true if you can make arr equal to target or false otherwise. 

Example 1:
Input: target = [1,2,3,4], arr = [2,4,1,3]
Output: true
Explanation: You can follow the next steps to convert arr to target:
1- Reverse subarray [2,4,1], arr becomes [1,4,2,3]
2- Reverse subarray [4,2], arr becomes [1,2,4,3]
3- Reverse subarray [4,3], arr becomes [1,2,3,4]
There are multiple ways to convert arr to target, this is not the only way to do so.

Example 2:
Input: target = [7], arr = [7]
Output: true
Explanation: arr is equal to target without any reverses.

Example 3:
Input: target = [3,7,9], arr = [3,7,11]
Output: false
Explanation: arr does not have value 9 and it can never be converted to target.

```java
class Solution {
    public boolean canBeEqual(int[] target, int[] arr) {
        Arrays.sort(target);
        Arrays.sort(arr);
        for(int i=0;i<arr.length;i++)
        {
            if(target[i]!=arr[i]) return false;
        }
        return true;
    }
}
```
- in this code first we sort the array both.
- if any of this is not equal then return false
- otherwise return true.
### 885. Spiral Matrix III
[Leetcode link](https://leetcode.com/problems/spiral-matrix-iii/description/?envType=daily-question&envId=2024-08-08)
<br>
You start at the cell (rStart, cStart) of an rows x cols grid facing east. The northwest corner is at the first row and column in the grid, and the southeast corner is at the last row and column.
You will walk in a clockwise spiral shape to visit every position in this grid. Whenever you move outside the grid's boundary, we continue our walk outside the grid (but may return to the grid boundary later.). Eventually, we reach all rows * cols spaces of the grid.
Return an array of coordinates representing the positions of the grid in the order you visited them.

Example 1:
Input: rows = 1, cols = 4, rStart = 0, cStart = 0
<br>
![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/08/24/example_1.png)
<br>
Output: [[0,0],[0,1],[0,2],[0,3]]

Example 2:
Input: rows = 5, cols = 6, rStart = 1, cStart = 4
<br>
![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/08/24/example_2.png)
<br>
Output: [[1,4],[1,5],[2,5],[2,4],[2,3],[1,3],[0,3],[0,4],[0,5],[3,5],[3,4],[3,3],[3,2],[2,2],[1,2],[0,2],[4,5],[4,4],[4,3],[4,2],[4,1],[3,1],[2,1],[1,1],[0,1],[4,0],[3,0],[2,0],[1,0],[0,0]]

```java
class Solution {
    public int[][] spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
        int[][] direction = {{0,1},{1,0},{0,-1},{-1,0}};
        int[][] result = new int[rows*cols][2];
        int d=0,count=1,steps=0;
        result[0] = new int[]{rStart,cStart};
        while(count<rows*cols)
        {
            if(d==0 || d==2) steps++;
            for(int i=0;i<steps;i++)
            {
                rStart+=direction[d][0];
                cStart+=direction[d][1];
                if(rStart>=0 && rStart<rows && cStart<cols && cStart>=0)
                {
                    result[count++]=new int[]{rStart,cStart};
                }
                if(count>=rows*cols) return result;
            }
            d=(d+1)%4;
            //if(count>=rows*cols) return result;
        }
        return result;
    }
}
```
Intuition
We're dealing with a 2D grid and a pattern of movement that spirals outward from a given starting point. The key insight here is recognizing the regularity in this spiral pattern.

When we visualize a spiral, we can see that it consists of a series of "arms" that extend in four directions: right, down, left, and up. Each complete rotation of the spiral increases the length of these arms. This observation forms the foundation of our approach.

Another crucial insight is that even though we're spiraling outwards, we're only interested in the cells that fall within our defined grid. This means we need a way to track our position and only record valid coordinates.

Lastly, we need to consider how to efficiently generate this spiral pattern. The regularity of the pattern suggests that we could use a systematic approach, possibly involving direction changes and step counts.

Approach
1. Direction Management
To manage the spiral's direction, we use a 2D array to represent the four possible movements:

int[][] directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
These correspond to moving right, down, left, and up respectively. By cycling through these directions, we can create our spiral pattern.

We use a variable d to keep track of our current direction:

int d = 0;
After each arm of the spiral, we update our direction:

d = (d + 1) % 4;
This clever use of modulo arithmetic ensures that we cycle through our directions array continuously.

2. Step Size Control
A key characteristic of a spiral is that it extends further with each rotation. We manage this with a steps variable:

int steps = 0;
We increment steps after moving east (d = 0) or west (d = 2):

if (d == 0 || d == 2) steps++;
This ensures that our spiral arms grow longer as we progress.

3. Grid Traversal
To traverse the grid, we use our current position (rStart, cStart) and update it based on our current direction and step size:

for (int i = 0; i < steps; i++) {
    rStart += directions[d][0];
    cStart += directions[d][1];
    // ... (boundary checking and result collection here)
}
This loop moves us along one arm of the spiral.

4. Boundary Checking
Not all positions in our spiral will be within the grid boundaries. We check each new position:

if (rStart >= 0 && rStart < rows && cStart >= 0 && cStart < cols) {
    // ... (result collection here)
}
This ensures we only consider valid grid positions.

5. Result Collection
We collect our results in a 2D array:

int[][] result = new int[rows * cols][2];
Each valid position is added to this array:

result[count++] = new int[]{rStart, cStart};
We use a count variable to keep track of how many positions we've added, and to determine when we've filled our result array.

Final Step
The entire process is wrapped in a while loop that continues until we've collected all the positions in our grid:

while (count < rows * cols) {
    // ... (direction management, step size control, grid traversal, 
    //      boundary checking, and result collection here)
}
Complexity Analysis
Time Complexity: O(max(R, C)^2)
The time complexity of this algorithm is O(max(R, C)^2), where R is the number of rows and C is the number of columns in the grid.

To understand this, let's break it down:

The spiral pattern we generate is essentially a square with side length max(R, C) * 2. This is because in the worst case, we need to spiral out far enough to reach the farthest corner of our grid.

The total number of cells in this larger square is (max(R, C) * 2)^2 = 4 * max(R, C)^2.

Our algorithm visits each of these cells exactly once, even though we only record the ones that fall within our actual grid.

Therefore, the number of iterations our algorithm performs is proportional to max(R, C)^2.

Even though we're only interested in R * C cells, our algorithm may need to visit up to 4 * max(R, C)^2 positions to ensure we've covered all the cells in our grid. This is why the time complexity is quadratic in terms of the larger dimension of the grid.

Space Complexity
The space complexity of this algorithm is O(R * C), where R is the number of rows and C is the number of columns in the grid.

This space requirement comes from our result array:

int[][] result = new int[rows * cols][2];
We're storing exactly R * C positions, each represented by a pair of integers.

This space complexity is optimal for this problem, as we need to return all the positions in the grid. We couldn't solve this problem with less space, as the output itself requires O(R * C) space.

Additional space used by our algorithm (for variables like steps, d, rStart, cStart, etc.) is constant and doesn't grow with the size of the input, so it doesn't affect our space complexity analysis.
> [Reference](https://www.youtube.com/results?search_query=885.+Spiral+Matrix+III)
### 840. Magic Squares In Grid
[Leetcode link](https://leetcode.com/problems/magic-squares-in-grid/?envType=daily-question&envId=2024-08-09)
<br>
A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.
Given a row x col grid of integers, how many 3 x 3 contiguous magic square subgrids are there? 
Note: while a magic square can only contain numbers from 1 to 9, grid may contain numbers up to 15.

Example 1:Input: grid = [[4,3,8,4],[9,5,1,9],[2,7,6,2]]
Output: 1
Explanation: 
The following subgrid is a 3 x 3 magic square:
while this one is not:
In total, there is only one magic square inside the given grid.

Example 2:
Input: grid = [[8]]
Output: 0

Constraints:
row == grid.length
col == grid[i].length
1 <= row, col <= 10
0 <= grid[i][j] <= 15

```java
class Solution {
    public int numMagicSquaresInside(int[][] grid) {
        int c=0;
        if(grid.length<3 || grid[0].length<3) return 0;
        for(int i=0;i<=grid.length-3;i++)
        {
            for(int j=0;j<=grid[0].length-3;j++)
            {
                if(valid(grid,i,j)) c++;
            }
        }
        return c;
    }
    public boolean valid(int[][] grid,int i,int j)
    {
        boolean[] seen = new boolean[10];
        for(int x=i;x<i+3;x++){
            for(int y=j;y<j+3;y++){
                int num = grid[x][y];
                if(num<1 || num>9 || seen[num]) return false;
                seen[num]=true;
            }
        }
        int d=0;
        //row sum
        for(int k=i;k<i+3;k++)
        {
            if(15!=grid[k][j]+grid[k][j+1]+grid[k][j+2]) return false;
        }
        //coloumn sum
        for(int l=j;l<j+3;l++)
            if(15!=grid[i][j]+grid[i+1][j]+grid[i+2][j]) return false;
        if(15!=grid[i][j]+grid[i+1][j+1]+grid[i+2][j+2]) return false;
        if(15!=grid[i+2][j]+grid[i+1][j+1]+grid[i][j+2]) return false;
        return true;
    }
}
```
- In this code we tell wheather it is 3X3 square matrix or not
- We already know that the formula for sum for the square matrix is n(n<sup>2</sup>)/2
- so sum=15
- The matrix must contain all nubers from 1 to 9
- So first the size is either row or coloumn is less than 3 we return as false.
- and the number is out of 9 or else any number is twicly appear then also return false.
- Then we check the row sum
- and check coloum sum and two diagnols sum
- based on the value return true or false. 
### 2974. Minimum Number Game
[Leetcode link](https://leetcode.com/problems/minimum-number-game/description/)
<br>
You are given a 0-indexed integer array nums of even length and there is also an empty array arr. Alice and Bob decided to play a game where in every round Alice and Bob will do one move. The rules of the game are as follows:
Every round, first Alice will remove the minimum element from nums, and then Bob does the same.
Now, first Bob will append the removed element in the array arr, and then Alice does the same.
The game continues until nums becomes empty.
Return the resulting array arr.

Example 1:
Input: nums = [5,4,2,3]
Output: [3,2,5,4]
Explanation: In round one, first Alice removes 2 and then Bob removes 3. Then in arr firstly Bob appends 3 and then Alice appends 2. So arr = [3,2].
At the begining of round two, nums = [5,4]. Now, first Alice removes 4 and then Bob removes 5. Then both append in arr which becomes [3,2,5,4].

Example 2:
Input: nums = [2,5]
Output: [5,2]
Explanation: In round one, first Alice removes 2 and then Bob removes 5. Then in arr firstly Bob appends and then Alice appends. So arr = [5,2].

Constraints:
2 <= nums.length <= 100
1 <= nums[i] <= 100
nums.length % 2 == 0

```java
class Solution {
    public int[] numberGame(int[] nums) {
        int[] ans = new int[nums.length];
        Arrays.sort(nums);
        for(int i=1;i<nums.length;i=i+2){
            ans[i]=nums[i-1];
            ans[i-1]=nums[i];
        }
        return ans;
    }
}
```
- In this code first bob will push the select number and then alice but first alice will play the game
- So first we sort the array
- so the first number is selsected by alice second number is selected by bob so the bob will push the number and then alice.
- So iterate the loop by increment two position the first will push to second position of the ans array
- second will push to the first position.
### 229. Majority Element II
[Leetcode link](https://leetcode.com/problems/majority-element-ii/description/)
<br>
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

Example 1:
Input: nums = [3,2,3]
Output: [3]

Example 2:
Input: nums = [1]
Output: [1]

Example 3:
Input: nums = [1,2]
Output: [1,2] 

Constraints:
1 <= nums.length <= 5 * 104
-109 <= nums[i] <= 109

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> arr = new ArrayList<>();
        HashMap<Integer,Integer> map =new HashMap<>();
        int n =nums.length/3;
        for(int i=0;i<nums.length;i++)
        {
            map.put(nums[i],map.getOrDefault(nums[i],0)+1);
            if(map.get(nums[i])>n) 
            {
                if(!arr.contains(nums[i])) arr.add(nums[i]);
            }
            if(arr.size()>2) return arr;
        }
        return arr;
    }
}
```
- In this code we find the count of each element and store in the hash map
- Whenever the count is greater than n/3 then add to the list
- if arr size is greater than 2 we return because there only of two elements present in the array that is greater than appear n/3 times.
- Example n = 9 n/3 = 3 two element 3+3 = 6 elements
### 1894. Find the Student that Will Replace the Chalk
[Leetcode link](https://leetcode.com/problems/find-the-student-that-will-replace-the-chalk/description/?envType=daily-question&envId=2024-09-02)
<br>
There are n students in a class numbered from 0 to n - 1. The teacher will give each student a problem starting with the student number 0, then the student number 1, and so on until the teacher reaches the student number n - 1. After that, the teacher will restart the process, starting with the student number 0 again.
You are given a 0-indexed integer array chalk and an integer k. There are initially k pieces of chalk. When the student number i is given a problem to solve, they will use chalk[i] pieces of chalk to solve that problem. However, if the current number of chalk pieces is strictly less than chalk[i], then the student number i will be asked to replace the chalk.
Return the index of the student that will replace the chalk pieces.

Example 1:
Input: chalk = [5,1,5], k = 22
Output: 0
Explanation: The students go in turns as follows:
- Student number 0 uses 5 chalk, so k = 17.
- Student number 1 uses 1 chalk, so k = 16.
- Student number 2 uses 5 chalk, so k = 11.
- Student number 0 uses 5 chalk, so k = 6.
- Student number 1 uses 1 chalk, so k = 5.
- Student number 2 uses 5 chalk, so k = 0.
Student number 0 does not have enough chalk, so they will have to replace it.

Example 2:
Input: chalk = [3,4,1,2], k = 25
Output: 1
Explanation: The students go in turns as follows:
- Student number 0 uses 3 chalk so k = 22.
- Student number 1 uses 4 chalk so k = 18.
- Student number 2 uses 1 chalk so k = 17.
- Student number 3 uses 2 chalk so k = 15.
- Student number 0 uses 3 chalk so k = 12.
- Student number 1 uses 4 chalk so k = 8.
- Student number 2 uses 1 chalk so k = 7.
- Student number 3 uses 2 chalk so k = 5.
- Student number 0 uses 3 chalk so k = 2.
Student number 1 does not have enough chalk, so they will have to replace it.
 
Constraints:
chalk.length == n
1 <= n <= 105
1 <= chalk[i] <= 105
1 <= k <= 109

```java
class Solution {
    public int chalkReplacer(int[] chalk, int k) {
        long[] longArray = new long[chalk.length];
        for (int i = 0; i < chalk.length; i++) {
            longArray[i] = chalk[i];
        }
        long sum = LongStream.of(longArray).sum();
        sum = k%sum;
        int i = 0;
        while(i<chalk.length)
        {
            sum-=chalk[i];
            if(sum<0) return i;
            i++;
        }
        return 0;
    }
}
```
### 2491. Divide Players Into Teams of Equal Skill
[Leetcode link](https://leetcode.com/problems/divide-players-into-teams-of-equal-skill/?envType=daily-question&envId=2024-10-04)
<br>
You are given a positive integer array skill of even length n where skill[i] denotes the skill of the ith player. Divide the players into n / 2 teams of size 2 such that the total skill of each team is equal.
The chemistry of a team is equal to the product of the skills of the players on that team.
Return the sum of the chemistry of all the teams, or return -1 if there is no way to divide the players into teams such that the total skill of each team is equal.
 
Example 1:
Input: skill = [3,2,5,1,3,4]
Output: 22
Explanation: 
Divide the players into the following teams: (1, 5), (2, 4), (3, 3), where each team has a total skill of 6.
The sum of the chemistry of all the teams is: 1 * 5 + 2 * 4 + 3 * 3 = 5 + 8 + 9 = 22.

Example 2:
Input: skill = [3,4]
Output: 12
Explanation: 
The two players form a team with a total skill of 7.
The chemistry of the team is 3 * 4 = 12.

Example 3:
Input: skill = [1,1,2,3]
Output: -1
Explanation: 
There is no way to divide the players into teams such that the total skill of each team is equal.
 
Constraints:
2 <= skill.length <= 105
skill.length is even.
1 <= skill[i] <= 1000

```java
class Solution {
    public long dividePlayers(int[] skill) {
        Arrays.sort(skill);
        long sum = 0;
        int ans = skill[skill.length-1]+skill[0];
        for(int i =0,j=skill.length-1;i<=j;i++,j--)
        {
            if(ans!=skill[j]+skill[i]) return -1;
            sum+=(skill[i]*skill[j]);
        }
        return sum;
    }
}
```
- In this case we split two members with n/2 teams
- So What we do is first we sort the team. After sorting we find one answer that is the sumation of the two numbers that is first and last.
- Then in the for loop we follow the two pointer algorithm. That is one in the first another one in the last so we find the sum if the sum is not equal to the answer then we return -1 because they did not have the same skill.
- Other wise we multiply that two numbers and added to it.
