> Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.
>
>**Notice:** 
>
> The string will only contain lowercase characters a-z. The maximum length of the string is 50000.

For the purpose of this problem, we define empty string as valid palindrome.

**Example:** 

Given s = "aba" return true

Given s = "abca" return true // delete c

## 解题思路

用双指针从两头像中间对比，第一次出现不一样移动任意一个指针，第二次出现不一样返回false。需要注意的是去掉头尾为回文串的特殊情况。

## 核心代码
        
      public boolean validPalindrome(String s) {

          int start = 0, end = s.length() - 1, err = 0;

          if (isPalindrome(s.substring(0, s.length() - 1)) || isPalindrome(s.substring(1, s.length()))) return true;

          while (start <= end){
              if (s.charAt(start) != s.charAt(end)){
                  start ++;
                  err++;
                  if (err > 1) return false;
                  continue;
              }
              start++;
              end--;
          }

          return true;
      }

      private boolean isPalindrome(String s){
          StringBuilder sb = new StringBuilder(s);
          return sb.reverse().toString().equals(s);
      }

## 时间空间复杂度

O(n) + S(n)

*n为字符串长度*
