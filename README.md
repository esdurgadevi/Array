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
 

