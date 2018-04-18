> Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
>
>**Notice:** 
>
> Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

**Example:** 

"A man, a plan, a canal: Panama" is a palindrome.

"race a car" is not a palindrome.

## 解题思路

用StingBuilder的reverse方法。注意StringBuilder的append是不会像s+"s"这种方式一样创建新的对象并占用新的内存的，所以可以保证内存空间不泄漏。

## 核心代码
        
        StringBuilder sb = new StringBuilder();
        String ss = s.toLowerCase();
        
        for (int i = 0; i < ss.length(); i++){
            if (ss.charAt(i) >= 'a' && ss.charAt(i) <= 'z'|| (ss.charAt(i) >= '0' && ss.charAt(i) <= '9')) sb.append(ss.charAt(i));
        }
        
        String se = sb.toString();
        StringBuilder re = sb.reverse();

        return (se.equals(re.toString()));

## 时间空间复杂度

O(n) + S(n)

*n为字符串长度*
