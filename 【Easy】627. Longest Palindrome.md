> Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.
>
> This is case sensitive, for example "Aa" is not considered a palindrome here.
>
> **Notice**
> Assume the length of given string will not exceed 1010.

**Example:** 

Given s = "abccccdd" return 7

One longest palindrome that can be built is "dccaccd", whose length is 7.

## 解题思路

找出一共有几对，加上一个单身的。

## 核心代码

        Set<Character> set = new HashSet<>();
        int result = 0;
        
        for (int i = 0; i < s.length(); i++){
            if (set.contains(s.charAt(i))){
                set.remove(s.charAt(i));
                result += 2;
            } else {
                set.add(s.charAt(i));
            }
        }
        
        return result + (set.size() > 0 ? 1 : 0);

## 时间空间复杂度

O(n) + S(n)

*n为数组长度*
