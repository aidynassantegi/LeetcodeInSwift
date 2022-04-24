# Leetcode problems and my solutions

**27. [Remove element](https://leetcode.com/problems/remove-element/)**

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

```
class MySolution {
    func removeElement(_ nums: inout [Int], _ val: Int) -> Int {
        var size = nums.count - 1
        while (size >= 0) {
            if (val == nums[size]) {
                nums.remove(at: size)
                size -= 1
            }else {
                size -= 1}
        }
        return nums.count
    }
}

```
Leetcode Solutions:

```
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

class Solution {
    func removeElement(_ nums: inout [Int], _ val: Int) -> Int {
        nums = nums.filter { $0 != val }
        return nums.count
    }
}
```

**28. [Implement strStr()](https://leetcode.com/problems/implement-strstr/)**

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

```
class MySolution {
    func strStr(_ haystack: String, _ needle: String) -> Int {
        if haystack == needle {return 0}
        guard haystack.count > needle.count else {return -1}
        guard needle != "" else {return 0}
        let haystackArray = Array(haystack)
        let needleArray = Array(needle)
        for i in 0..<haystackArray.count-needleArray.count+1 {
            if haystackArray[i..<i+needleArray.count] == needleArray[0..<needleArray.count] {
                return i
            }
        }
        return -1
    }
}
```