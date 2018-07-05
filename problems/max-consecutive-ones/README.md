# Leetcode: Max Consecutive Ones     :BLOG:Basic:


---

Max Consecutive Ones  

---

Given a binary array, find the maximum number of consecutive 1s in this array.  

    Example 1:
    Input: [1,1,0,1,1,1]
    Output: 3
    Explanation: The first two digits or the last three digits are consecutive 1s.
        The maximum number of consecutive 1s is 3.

Note:  

-   The input array will only contain 0 and 1.
-   The length of input array is a positive integer and will not exceed 10,000

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/max-consecutive-ones)  

Credits To: [leetcode.com](https://leetcode.com/problems/max-consecutive-ones/description/)  

Leave me comments, if you have better ways to solve.  

---

    class Solution(object):
        ## Blog link: https://code.dennyzhang.com/max-consecutive-ones
        ## Basic Ideas:  counter
        ##               If found one 0, reset the counter to 0. Otherwise counter + 1
        ##
        ## Complexity: Time O(n), Space O(1)
        def findMaxConsecutiveOnes(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            max_count, counter = 0, 0
            for num in nums:
                if num == 1:
                    counter = counter+1
                    max_count = max(max_count, counter)
                else:
                    counter = 0
            return max_count
    
        ## Ideas: Two pointers
        ##              i points to the start of consecutive of 1s
        ##              j points to the next element of the end of consecutive of 1s.
        ##
        ##  Assumption: [1, 0, 1], we should return 1
        ## Complexity: Time O(n) Space O(1)
        def findMaxConsecutiveOnes_v1(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            max_count = 0
            length  = len(nums)
            i = 0
            while i < length:
                if nums[i] == 0:
                    i += 1
                    continue
                # nums[i] == 1
                j = i + 1
                while j < length and nums[j] == 1:
                    j += 1
                # nums[j] == 0 and nums[j-1] == 1
                max_count = max(max_count, j-i)
                # move to next
                i = j + 1
            return max_count
    
    # s = Solution()
    # print s.findMaxConsecutiveOnes([0]) # 0
    # print s.findMaxConsecutiveOnes([1, 0, 1]) # 1
    # print s.findMaxConsecutiveOnes([1]) # 1