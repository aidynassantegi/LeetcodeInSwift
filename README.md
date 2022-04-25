# Leetcode problems and my solutions

**1. [Two Sum](https://leetcode.com/problems/two-sum/)**

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

```
class MySolution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var arr  = [Int]()
        for i in 0..<nums.count {
            for j in i+1..<nums.count{
                if (nums[i]+nums[j]==target) {
                    arr = [i,j]
                }
            }
        }
        return arr
    }
}
```

**9. Palindrome Number**

Given an integer x, return true if x is palindrome integer.

An integer is a palindrome when it reads the same backward as forward.

For example, 121 is a palindrome while 123 is not.

```
class MySolution {
    func isPalindrome(_ x: Int) -> Bool {
        if (x<0) {return false}
        var num = x
        var digits: [Int] = []
        while num >= 1 {
            let digit = num%10
            digits.append(digit)
            num /= 10
        }
        if digits.count > 1{
            for i in 0...digits.count/2 - 1{
                if digits[i] != digits[digits.count - 1 - i]{
                    return false
                }
            }
            
        }
        return true
    }
}
```

**13. [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)**

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

```
class MySolution {
    func romanToInt(_ s: String) -> Int {
        var romanNumbers: [Int] = []
        var arabicNumber = 0
        for roman in s {
            var number: Int
            switch roman {
            case "I": number = 1
            case "V": number = 5
            case "X": number = 10
            case "L": number = 50
            case "C": number = 100
            case "D": number = 500
            case "M": number = 1000
            default: number = 0
            }
            if number > romanNumbers.last ?? -1 {
                let prevNumber = romanNumbers.popLast() ?? 0
                let newNumberToLast = number - prevNumber
                arabicNumber -= prevNumber
                arabicNumber += newNumberToLast
                romanNumbers.append(newNumberToLast)
            }else {
                arabicNumber += number
                romanNumbers.append(number)
            }
        }
        return arabicNumber
    }
}
```

**14. [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)**

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

```
class MySolution {
    func longestCommonPrefix(_ strs: [String]) -> String {
        if strs.count == 1 {return strs[0]}
        var longestPref = strs[0]
        var index = 1
        while true{
            if longestPref == "" {break}
            if !strs[index].hasPrefix(longestPref){
                longestPref.popLast()
                index = 1
            }else {
                if index == strs.count - 1 {break}
                index += 1
            }
        }
        return longestPref
    }
}
```

**26. [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)**

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

Custom Judge:

The judge will test your solution with the following code:
```
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```
If all assertions pass, then your solution will be accepted.

```
class MySolution {
    func removeDuplicates(_ nums: inout [Int]) -> Int {
        let lastIndex = nums.count - 1
        var k = 0
        if lastIndex == 0 {return 1}
        if nums.count > 0 {
            k = 1
            var prev = nums[0]
            for i in 1...lastIndex {
                if prev != nums[i] {
                    nums[k] = nums[i]
                    prev = nums[i]
                    k += 1
                }
            }
        }
        return k
    }
}
```

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

**35. [Search Insert Position](https://leetcode.com/problems/search-insert-position/)**

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

Leetcode Solution:

```
class Solution {
    // - Complexity:
    //   - time: O(log n), where n is the length of the nums.
    //   - space: O(1), only constant space is used.

    func searchInsert(_ nums: [Int], _ target: Int) -> Int {
        var start = 0
        var end = nums.count

        while start < end {
            let mid = start + (end - start) / 2

            if nums[mid] < target {
                start = mid + 1
            } else {
                end = mid
            }
        }
        return start
    }

}
```

**53. [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)**

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

```
class MySolution {
    func maxSubArray(_ nums: [Int]) -> Int {
        if nums.count == 0 {return 0}
        var maxSum = nums.first!
        var maxBox: [Int] = [nums.first!]
        for i in 1..<nums.count {
            let elem = nums[i] + (maxBox.last! > 0 ? maxBox.last! : 0)
            maxBox.append(elem)
            maxSum = maxSum>elem ? maxSum : elem
        }
        return maxSum
    }
}
```

Leetcode solution
```
class Solution {
    func maxSubArray(_ nums: [Int]) -> Int {
        var curSum = nums[0], maxSum = nums[0]
        for i in 1..<nums.count {
            curSum = max(nums[i], curSum + nums[i])
            maxSum = max(maxSum, curSum)
        }
        return maxSum
    }
}
```

**58. [Length of Last Word](https://leetcode.com/problems/length-of-last-word/)**

Given a string s consisting of some words separated by some number of spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

```
class MySolution {
    func lengthOfLastWord(_ s: String) -> Int {
        if let n = s.split(separator: " ").last?.count {
            return n
        }else {
            return 0
        }
    }
}
```