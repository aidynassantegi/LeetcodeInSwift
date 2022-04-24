# Leetcode problems and my solutions

27. Remove element

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

'''

    class Solution {
        
        // - Complexity:
        //   - time: O(n), where n is the length of the nums.
        //   - space: O(1), only constant space is used.

        func removeElement(_ nums: inout [Int], _ val: Int) -> Int {
            guard !nums.isEmpty else { return 0 }
            var i = 0

            for num in nums {
                guard num != val else { continue }
                nums[i] = num
                i += 1
            }

            return i
        }

    }

'''