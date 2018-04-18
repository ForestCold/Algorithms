> Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.
>

**Example:** 

Given the string = "abcdzdcab", return "cdzdc".

## 解题思路

**a. 常规解法：动态规划。**

对任意一个子字符串[a, b]而言，它是不是回文串包括三种情况：

 1. 只有一个字符，即a = b，一定是回文串
 2. 只有两个字符，即a + 1 = b，若s[a] = s[b]，一定是回文串
 3. 包含三个以上字符，如果中间的[a+1, b-1]是回文串且s[a] = s[b]，一定是回文串
 
所以，建立二维数组dp，按照这三条规则进行初始化，并在每次赋值时和现有的最大长度比较，如果区间是回文串且长度大于现有最大长度则对它进行更新。需要注意的地方是初始化的顺序，要保证每一步都能走。

**b. Manacher's Algorithm：一个线性时间复杂度的算法。**

首先，为了排除奇偶性的影响，在字符串的各个字符之间插入一个不可能出现的字符，这样所有回文串都是奇数位。叫这个新的字符串newS:

    aba  ———>  #a#b#a#
    abba ———>  #a#b#b#a#

接着，维护一个p数组，其中p[i]表示newS中以i为中心的最大回文串的半径，比如：

    #c#a#b#a#d#  ———>  b在第5位，以b为中心的最长回文串是“#a#b#a#”，最长半径是b到最右边的#，长度为4，因此p[5] = 4

很容易证明，原串中的最长回文子串的长度是p[i] - 1，因为：

    p[i] * 2 - 1 = newS中对应的最长回文子串长度 = #的个数 + 原串中的最长回文子串的长度 = 原串中的最长回文子串的长度 * 2 + 1

遍历一遍newS，边建立p[i]数组边与将p[i] - 1与现有的最长回文子串长度进行比较并动态更新现有的最长回文子串长度。

关键在于如何建立p[i]数组。首先在i之前找到一个回文子串，使它的右边距最靠近i，这个回文子串的中心叫它id,右边距叫它mx:
    
    012345678i
    #a#b#b#a#_
          #a#  ———>  id = 7, mx = 8

可以通过：

    2 * id - i

来表示i基于id这个点的对称点，把这个对称点称为j。因为j是已经扫描过的，所以p[j]保存了以j为中心的最大回文子串的半径。又因为i和j对称，所以假如i在mx之前，
p[i]的值等于min(p[j], mx - i)。如下图：

![](https://raw.githubusercontent.com/longpf/blog.longpf.github.io/master/asset/Manacher1-1.png)

之后，还不能判断p[i]是不是最终结果，所以要向外扩展，直到固定住p[i]。然后对比p[i] + i和mx，如果发现p[i] + i更靠右，则更新mx。

## 核心代码

动态规划:
        
        // 所有长度为1的字符串都是回文串
        // 所有长度为2且两个字符相等的字符串都是回文串
        for (int i = 0; i < s.length(); i++){
            dp[i][i] = true;
            start = i;
            length = 1;
            if (i + 1 < s.length()){
                dp[i][i + 1] = s.charAt(i) == s.charAt(i + 1);
                if (dp[i][i + 1]){
                    start = i;
                    length = 2;
                }
            }
        }
        
        // 所有长度为3以上的字符串[j, i]，如果[j + 1, i - 1]是回文串且j和i处字符相等，则它是回文串
        for (int i = 1; i < s.length(); i++){
            for (int j = 0; j < i; j++){
                dp[i][j] = dp[i - 1][j + 1] && (s.charAt(i) == s.charAt(j));
                if (dp[i][j]){
                    if (i - j + 1 > length){
                        start = j;
                        length = i - j + 1;
                    }
                }
            }
        }
    
Manacher's Algorithm：

        String newS = generateString(s);
        
        int[] p = new int[newS.length()];
        int result = 0, start = 0, mx = 0, id = 0;
        
        for (int i = 0; i < newS.length(); i++){
            // 如果i < mx，利用已知信息就可以计算出p[i]
            p[i] = i < mx ? Math.min(p[2 * id - i], mx - i) : 1;
            // 否则，从i向外扩展，精确计算p[i]
            while (i - p[i] >= 0 && i + p[i] < newS.length() && newS.charAt(i - p[i]) == newS.charAt(i + p[i])) p[i]++;
            // 如果i的右边界比当前右边界更右，更新mx和id
            if (i + p[i] > mx){
                mx = i + p[i];
                id = i;
            }
            // 更新已经存在的最长回文子串
            if (p[i] - 1 > result){
                result = p[i] - 1;
                start = (i - p[i] + 1) / 2;
            }
        }


## 时间空间复杂度

a. O(n^2)
b. O(n)

*n为字符串长度*
