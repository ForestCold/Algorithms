> Given a string, determine if a permutation of the string could form a palindrome.
>

**Example:** 

Given s = "code", return False.
Given s = "aab", return True.
Given s = "carerac", return True.

## 解题思路

消消乐，碰到一对消灭一对，最后如果只剩下少于一个单身的就返回true，否则返回false。

## 核心代码

        Set<Character> set = new HashSet<>();
        for (int i = 0; i < s.length(); i++){
            if (set.contains(s.charAt(i))) set.remove(s.charAt(i));
            else set.add(s.charAt(i));
        }
        
        return set.size() <= 1;


## 时间空间复杂度

O(n) + S(n)

*n为字符串长度*
