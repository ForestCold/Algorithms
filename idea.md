# Target Sum 系列

	○ 找所有combination：DFS 
		- 数字有重复：if ( i > startIndex && num[i] == num[i - 1] ) continue;
		- 每个数字取次数不限制：helper() 递归时startIndex = i
		- 全是positive，先sort后pruning
	○ 找combination的个数： DP
		- dp[j] += dp[j - i], j是target循环里的数，i是nums里的数
		- 不同排序算新的：先for循环target，再for循环nums（knapsack解法反过来）
		- 全是positive： 先sort后pruning
		- 每个数字取次数不限制：knapsack内层target的循环从小到大
		- 每个数字只能取一次：knapsack内层target的循环从大到小
		- 每个数加号或减号：用公式转成target sum
		- 结果等于target，初始化dp[0] = 1
		- 最小个数满足target: min(dp[j - nums[i]]) + 1
	○ Expression Add Operation: DFS
		- startIndex = 0没有符号
		- sb.setLength(len), sb.append(sign).append(number)
		- 用long防止overflow, long.valueOf
		- mult记录最后一个乘法组件，加为mult, 减为-mult, 乘法为 number * mult （更新为res - mult + number * mult）
		
# Sub Array/ Sub String 系列
	○ 长度最小的sub array: sliding window
		- sum >= k且都是positive, sum >= k的时候就slow++
	○ 长度最大的满足某种条件的sub array: map记录某个值和index的对应关系
		- sum = k: map记录<sum, index>, 更新max
		- 只包含0和1的数组，0和1的个数相等：把0当作-1，然后转化为求sum = 0
		- sum % k == 0: k != 0的情况map里存sum % k， k = 0的情况map里存sum 
	○ 是否存在满足条件的substring: sliding window
		- 另一个string的permutation: 用一个map记录character和出现次数，用count记录满足条件的字符(map的value为0)，当map某个出现次数被更新为0时count + 1，最后count == 需要的substring长度(map.keySet())即可
		- 包含另一个string的所有character的最短substring: 和（1）的区别是window大小是变化的, 注意算count == 0时的临界点来更新count，在while(count == 0)的循环里更新left指针
		- 存在最多k个不同character的最大子串：int[] arr = new int[256]，同样找时机更新count，count > k的时候移动left指针
	○ 存在多少组满足条件的substring: 
		- sum = k: 用map放sum和count
	○ 存在多少组满足条件的subsequence:
		- subsequence是另一个string: dp[s.len][t.len]存结果，如果s[i] == t[j], dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j], 否则dp[i][j] = dp[i - 1][j]。注意初始化的时候dp[i][0] = 1，因为空的t一定在s里并且只有一个
	○ subarray的最大production: 用max, min记录以num[i]结尾的subarray的max production和min production，更新max和min的时候在num[i], num[i] * max, num[i]  * min中选最大和最小值， 然后用max更新ans
	○ 输出每个位置存其它位置的乘积的数组，要求空间复杂度为1，不能用除法：res[i] = 0到i的积 * i + 1到n的积，所以先从左往右遍历一遍把production放到res里，再从右往左遍历用变量记录i + 1到n的积，和res[i - 1]相乘。最后记得更新res[0]。
	○ 三个互不重叠长度为k和最大的sub array: sum[i]记录以i为结尾的长度为k的数组和，left[i]记录0到i中长度为k并且和最大的数组的起始位置，right[i]记录i到末尾中长度为k并且和最大的数组的起始位置。然后遍历中间数组的起始位置，从k到len - 2 * k，每次计算sum[i + k - 1] + sum[left[i - 1] + k - 1] + sum[right[i + k] + k - 1]和最大值比较
	○ Palindrome:
		- 一个string remove最少元素，使新的string是palindrome：求当前string和reverse string的LCS，结果就是string长度减去LCS的长度
		- 存在多少palindrome: dp，不用初始化，从i = s.len - 1, j = i开始，如果i到j小于三个字符，s(i) == s(j) -> true, 否则dp[i][j] = dp[i + 1][j - 1]
		- 最长palindrome: dp，和上面那题一样

# String Matching 系列
	○ 正则匹配： "."匹配单个字符：  如果遇到"."或s(i) == p(j)，dp[i][j] = dp[i - 1][j - 1]，注意dp的大小是s.len + 1, t.len + 1，所以在取字符的时候要-1。"*"的共同点是dp[i - 1][j]可以表示"*"匹配多个字符的情况。
		- "*"匹配所有字符： 如果遇到"*"，dp[i][j] = dp[i - 1][j] || dp[i][j - 1]，前者表示"*"匹配一或多个字符，递归下去，后者表示"*"匹配0个字符。初始化：dp[0][0] = true, dp[i][0] = false, dp[0][j]看p(j)是不是"*"，如果是，由dp[0][j - 1]推出
		- "a*"匹配多个a组成的字符： 如果遇到"*"，分两种种情况： (1) *匹配空集合，此时只要dp[i][j - 2]为true即可（因为x*整个为空）(2) "*"匹配非空，那条件是p(j - 1) == s(i) 或者p(j - 1) == "."。在这种情况下dp[i][j] = dp[i - 1][j] || dp[i][j - 1], 前者表示匹配多个，后者表示匹配一个。 初始化：dp[0][0] = true, dp[i][0] = false, dp[0][j]看p(j)是不是"*"，如果是，由dp[0][j - 2]推出（因为*可以把它自己连同它之前的符号一起消除）
		- 给一串数字求decode成字母有多少种方法：如果substring(i - 1, i + 1) 在10 ~ 26之间，dp[i] += dp[i - 2], 如果substring(i, i + 1) 在1 ~ 9之间，dp[i] += dp[i - 1]
		- 给一串数字，包含可以匹配任意字符的*，求decode成字母有多少种方法：用三个数字e0, e1, e2分别表示以任意数结尾的当前选择总数，以1结尾的当前选择总数和以2结尾的当前选择总数。则e1的更新方法是如果第i个位置为1或'*', e1 = 上一个e0，e2同理。e0的更新方法是如果第i个位置为*，则e0 = 9 * e0 + 9 * e1 + 6 * e2，否则e0 = 第i个位置不为0 ? e0 + e1 + 第i个位置小于6 ? e2
	○ 字符匹配： trie tree
		- 给一个string list，找出所有两个string组合起来是palindrome的组合：用trie存所有string的逆string，再对所有string进行分割，保证一边是palindrome，然后查找另一边在不在trie里，在的话就加入答案。注意：（1）左边是P和右边是P影响答案中index的顺序 （2）注意要把""考虑进来，当某个string自身是P时，要分成"" + string和string + ""两种形式。否则分成"" + string一种形式即可（去重复）。
	
# Traversal 系列
	○ BST
		- 找一个node的下一个node：两种情况，这个node如果没有右子树，下一个node是离它最近的使它成为左子树节点的妈妈，如果有右子树，下一个node是右子树的最小节点。所以，二分法查找时，如果node < root，更新可能的ans为root，并且向root.left查。如果node >= root，向root.right查。当node为root时因为是向右边查并且右边全部大于node，所以找到的一定是右边的最小值。
		- Iterator:  用一个stack，初始化的时候递归存root的所有左边node，hasNext只要判断stack是不是空，next的时候把pop出来的node.right的所有左边node再加stack。原因是在BST里一个node的下一个节点一定是它右子树最左边的点（有右子树）或它的爸爸。
		- 已知preorder还原：O(n)的做法，dfs每次设置min和max，在min和max中间的数字就是当前root，root.left = dfs(这里用root.val作为min带入)，root.right同理。index设置为全局变量每次dfs都++。
		- Convert BST to Circular Doubly LinkedList：(1)recursion做法，全局设置一个curt和一个head，然后inOrderTraversal，每次更新curt，要注意的是如果curt是null要把当前root设置为head。然后root.left = curt, curt.right = root，最后注意首尾相连。(2) iteration做法，用stack，和上面的iterator一样。
	○ 已知两种遍历方式还原树：
		- 已知前 + 中， 还原：对preorder从前往后遍历，然后把inorder的数组分成两半，先left再right
		- 已知中 + 后， 还原：对postorder从后往前遍历，然后把inorder的数组分成两半，先right再left（因为从后往前先碰到right）
		- 已知前 + 后， 不能还原
	○ vertical traverse: BFS存col和node， left的col - 1, right的col + 1，放到map里
	○ vec2D: 设置i和j指针，next和hasNext都要判断i和j的合法性
	○ 包含Iist或Integer的数据结构：用stack反向存最顶层，在hasNext里拆包，递归判断
	○ Serialize & Deserialize binary tree
		- serialize: 用queue，放的时候才放sb，很简单
		- deserialize: 还是用queue，然后记录一个count， count + 1为左， count + 2为右，都放queue里，然后count += 2
	
# Sell Stock 系列
	○ 只准买入卖出一次，求最大利润： 从右向左遍历，找当前值之后最大的值
	○ 允许买入卖出多次：只要上升（prices[i +1] > prices[i]）就加
	○ 允许买入卖出多次，但每次操作都有手续费：动态规划，own表示当天如果有股票最大利润是多少，noOwn表示当天如果没股票最大利润是多少
		- own = Math.max(own, noOwn - prices[i]); //要么昨天就有了，要么昨天没有今天买入
		- noOwn = Math.max(noOwn, own + prices[i] - fee);//要么昨天没有，要么昨天有今天卖出
	○ 只允许两次操作，循环遍历分割点，转换为a。注意从 i  -> i+1时分割点左边的利润不需要重新算，只需要算（新增的prices[i] - 之前的最小值， 之前的最大利润）的最大值就行。
	○ 只允许k次操作: 动态规划, own[i][j]代表第i天手上有这只股票，并进行了j次交易的最大利润。sell[i][j]代表代表第i天手上没有这只股票，并进行了j次交易的最大利润。每天只有三个动作：卖出或者买入或者不动。注意k < prices.length / 2时转化成b
	
# Calculate类
	○ Pow: 递归计算num = pow(x, n / 2)，如果n为奇数，返回num * num，否则返回num * num * x
		- 坑一：n可能为负数，所以当n为负数时，n = -n, x = 1 / x
		- 坑二：因为存在n = -n这个操作，所以当n为Integer.MIN_VALUE时-n会溢出，要用一个long来存n或者特殊处理n
		- 注意：n为0作为终止条件
	○ Divide:  对于被除数m和除数n，可以写成m = n (a1 2^0 + a2 2^1 + ... + ax 2 ^ x)的形式。因此通过一个循环，首先找出使得 n 2^i <= m 的最大i, 比如11 / 3, 3 2^1 = 6， 3 2^2 = 12 > 11, 所以2^1是要求的最大数。之后将2^1加入结果，并用11-6替换原来的11， 再进行第二次循环：3 2^0 = 3 < 5, 将2 ^ 0加入结果，剩下的2小于被除数3了，表示2是余数，停止循环。
		- while (a >= b){
			c = b;
			k = 1;
			while (a >= c){
				c = c << 1;
				k = k << 1;
			}
			result += k >> 1;
			a -= c >> 1;            
		}
		- 坑一：除数为0，要返回Integer.MAX_VALUE
		- 坑二： 存在负数时，先算出sign，再取绝对值算
		- 坑三：刚开始全部转为long，因为如果ans是Integer.MIN_VALUE并且sign是-1的时候会溢出
	○ Add: 如果是二进制，每次直接carry = num / 2, sb.append(num % 2)
	○ (xy)%z == ((x%z)y)%z == (x*(y%z))%z 
	○ 第K个丑数：三个queue分别存2,3,5的倍数，每次比较头部取最小数字，分别乘以2，3，5放入三个queue，如果头部数字和当前数字相等则移除
	○ 求a, b的最大公约数，a大于b，则递归a = b, b = a % b, 直到a % b == 0，最大公约数为b
		- 求最小公倍数，a * b / (a和b的最大公约数)
		- 如果mx + ny = d存在整数解，则d % (m和n的最大公约数) = 0（倒水问题）
	○ Boyer-Moore: 好处是可以分布式计算，把数组分成很多份分别计算一个结果， map reduce
		- 出现大于1/2:  用count记录出现次数，遍历到的值为当前候选值时+1，否则-1，当count为0时候选值变成新的数。因为majority number数量必定过半，所以一旦遇到，count不可能被减成0。
		- 出现大于1/3:  用两个count和两个候选值记录，当当前遍历到的值都不等于这两个候选值时两个count才-1。找出现次数大于1/k的数同理。最后需要验证这两个值是不是都出现超过1/3次。
	
# LinkedList类
	○ reverse: 四部曲/recursive
		- 最简单的reverse：
		(a) 不用dummy，直接prev = null然后四部曲最后返回prev
		(b) 递归: helper(curt, newhead), newhead相当于prev (O(n), S(n))
		(c) follow up: 用logn的空间和nlogn的时间，可以在recursion时二分先右后左，每个helper的时候都传入len / 2和 len - len / 2方便找中点
		- k个一组： 主函数里写while (prev)，然后helper每次返回first作为prev。如果不够k个返回null，否则先找出头尾和post, prev四个点，prev.next = last, 四部曲反转，最后first.next = post。

# 转换类
	○ Integer to English word: 三个list，一个存小于二十的词，一个存十的倍数的词，一个存千，百万，千万。先做一个helper，能够处理1000以下的数字，然后对于1000以上的数字，每次处理三位，分别加上单位{"", thousand, million, billion}，再把原来的结果放在后面
		
# 二维数组类
	○ Island:  二循环遇到1则操作 ,操作过的数字置为0
		- Number: DFS/BFS/Union Find -> O(m * n)
		- Area: DFS, 每次面积为1 + 四个方向DFS和，如果越界返回0
		- Perimeter:  每次面积为四个方向DFS和，如果越界返回1（代表是个边），如果visited返回0， 这里的visited是针对于一个island而言的
	○ Largest Area:
		- histogram: 维护一个升序的stack（存index），如果某个index i的height小于stack.peek()，那么把stack中height大于i的都pop出来，每pop一个。此时的height是当前pop出元素的height，此时的width是i和当前元素的index差再减1，然后用w * h更新max。需要注意的是如果stack为空则w直接为i。还要注意循环中要取到 i = heights.length，当 i = heights.length时也要把stack里剩下的东西pop出来算。
		- histogram蓄水池：从左往右扫一次，从右往左扫一次，记录每个位置左边的最大值和右边的最大值（注意这个值要和自身高度比取max），然后小的那个减去当前高度就是可蓄水量
		- rectangle in 2-matrix:  转换成histogram, 维护一个长度为matrix[0]的height数组，遇到0就是0，遇到1就++，然后每次做一次histogram
		- squal in 2-matrix: DP, 左上三个方向的最小值加1
	○ Sum:
		- 找最大和的子矩阵，遍历上下边界，确定上下边界之后循环把中间的部分压缩成一个数组，每个元素代表当前列的元素和，然后用subarray的做法做。在最开始先求数组prefixCol, prefixCol[i][j]代表第j列从0到i的元素和，算压缩数组的时候直接相减。
		- 找和为0的子矩阵，和b类似
	○ 变换：
		- 旋转90度：matrix[i][j] = matrix[n - j - 1][i], 剥洋葱，注意i从[0到n/2)，j从[i到n - j - 1)
		- 返回spiral的顺序：设置边界分别为left, right, up, down。大循环条件left <= right && up <= down。然后里面四个for循环，代表四个不同方向，每个for循环之后对应的边界要移动。后两个for循环之前要额外判断一下while里的条件是否还成立。
		- 给一个n生成一个spiral矩阵：和上一题一样，不同的是在for循环里将matrix[i][j]设置为count
	○ 棋盘：
		- Design tic-tac-toe:  用两个数组存row和col，用两个变量存两个对角线，player one则对应位置++，player two则对应位置--，当abs（某行，列，对角线）为n时代表player胜利。
		- Design mine sweeper（扫雷）: 
			（1）生成下一步状态： 直接DFS （2）生成棋盘：给长宽和雷数，随机生成，reservior sampling
		- Design candy crash:  
		- Sodoku: 
			（1）valid: 三个map分别代表rows, cols和boards, 存出现过的数字（2）solve: 所有可选位置依次放valid的数字

# Sort类
	○ 分类: quick sort  
		- Move Zero: index表示在此之前的数字都是合法的，循环遇到不是0的数字就放到index上，最后index之后都set为0
		- Remove duplicates from sorted array: 和move zeros一样，但不合法的num[i] <= num[index - 2]注意右边是index
		- Three color: zero从0开始，two从len - 1开始，循环遇到0和位置zero上的交换，遇到2和位置two上的交换
		- N color: while(left < right)的大循环里，先找min和max，然后sort  min和max，这时候left和right也被自动更新了。以此循环，时间复杂度为什么是n？
	○ Kth largest:
		- quick select: 每次找个pivot，小于pivot的放左边，大于pivot的放右边。下一次只考虑一半。时间复杂度【最好情况O(n): T(n) = T(n / 2) + O(n)， 最差情况O(n^2): T(n) = T(n - 1) + O(n)】最好复杂度是O(n)的原因是每次都只需要考虑一半，和quick sort不同，quick sort每次两边都要考虑所以复杂度是O(nlogn)。
		- pivot可以用num[right]当，然后用remove zero的思想从左向右扫描（不要扫到right），遇到<pivot的就和当前index交换并且index++，注意最后要swap(index, right)
		- PQ: nlogk
		- n个排序数组的中位数： 如果一共偶数个，找第size/2和第size/3个的平均值，否则找第size/2+1个
		- n个排序数组的第k个数：值域二分，对于当前val，找比val小的值一共有几个。如果这个值小于k，证明第k个数是比val大的，把start变成val，反之如果这个值大于等于k，证明第k个数是比val小的，把end变成val。找比val小的值共有几个时，也是用二分。
		
# Permutation
	○ swap两位使得结果最大：max[i]记录i及i之后最大值的下标，循环遍历如果max[i] == i，往后移动，否则交换当前i和max[i]的值并返回
	○ next permutation: 从后往前第一个递增的地方，左边的那个数和从后往前第一个大于它的数交换，再把右边全部反过来
	○ previous permutation: 从后往前第一个递减的地方，左边的那个数和从后往前第一个小于它的数交换，再把右边的全部反过来
		
# 数据结构模拟
	○ Insert, delete, getRandom O(1) : 
		- 无重复：两个map，分别从val到index和从index到val，在remove的时候如果不是remove index最大的那个，则把index最大的那个移过来填坑。然后随机的时候随机max.size()。
	○ 两个stack -> 一个queue: 一个进一个出，出的为空时进的全部倒入出
	○ 两个queue -> 一个stack: 互相倒，交换指针  

# 多元素交集
	○ Total hamming distance: 就是sum（每一位的1的个数 * 当前位0的个数）， 因此外循环从0到32， 内循环算ones += num[i] & 1 ，ans += ones * (nums.len - ones)，记得内循环每次nums要右移一位
	
# 递增递减类
	○ Remove k digits to make smallest num:  用一个递增stack存结果，一个count存当前remove的数字个数，如果当前元素大于栈顶，并且栈的size小于num.len - k，则入栈，如果size大，则count++。如果当前元素小于栈顶，pop栈直到count == k或者栈空，然后push元素。最后记得把前序0都删掉。
		
# 实际应用
	○ The Skyline problem:
	○ Sparse Matrix  Multipulation:
		- C[i][j] = Sum(A[i][k] * B[k][j]), where k from 0 to A[0].length - 1
		- 先循环i，再循环k，最后循环j (brute force 是按照ijk的顺序循环)，这样当A[i][k]为0时就可以避免j的循环
		- 二分法？
	- Excel sheet column title: 要注意的点是A映射为1而不是0，所以while循环中每一次都要先n--，然后存'A' + n % 26，再n /= 26
	○ 文字/路径简化
		- Simplify Path:  deque初始化为linkedlist，并且接口为addFirst(), pollFirst(), offerFirst()等
		- Encode & Decode Tiny URL:  （1）tiny URL 是一个base url加上一个六位的短url，每一位可以存储[a-z][0-9][A-Z]共62个字符，所以一共可以存62^6个，足够了。（2）所以循环六次用random取一个index字符 （3）做两个map，一个存长到短的映射，一个存短到长的映射
		- Text Jusyification：
		- Prefix自动补全：trie的使用条件是structure比较稳定，search比add多，build trie is costly， 空间复杂度是n^2, worst case m * n^2（所有字都没交集）, n为字符平均长度，m为字符数量
		- 如果同时给了prefix和suffix，让返回最长的满足的word：
	○ 旅行家
		- Dijkstra: （1）普通 （2）最多走k次：k次循环，每次cost[i ] = Math.min(cost[i], cost[某个能到i的j] + cost[i到j])
	○ 输入输出
		- Read4: 实现read(buff, n)，n代表最多有多少东西，返回实际读了多少东西
		- 简单版：如果read4返回的东西小于4代表到头了，要结束循环。最后返回的是index和n的最小值，因为n有可能小于4。
		- 升级版（可以被call很多次）：设置head和tail初始化为0，在循环中如果head == tail，表示当前buffer4中内容都处理完了， head归0，再次read4，如果返回0则return i。然后一旦head < tail表示buffer4中还有元素没读，依次读入buff。
	○ 任务调度 
		- Function's exclusive time:  和interval有关的题，两个stack一个存开始时间一个存id，每次遇到结束时间就更新当前函数的ans（加time - start + 1）以及当前函数下面那个函数的ans（减time - start + 1）。
		- Task Scheduler: （1）先找出frequency最大的task， 做frequency - 1个桶，每个桶长度为n + 1，每个桶放一个这个task，然后再慢慢安插别的task。最后frequency最大的所有task再排在后面。（2）特殊情况是not enough space，这种情况下只需要task.len，因为最后剩下的task一定能够每隔n个插入，所有task中间没有缝隙 （3）所以结果为Math.max(task.length, (maxFreq - 1) * (n + 1) + maxCount)，时间复杂度为O(n)
		- Task Scheduler（FIPO）: 用一个map去记录每个task和最终的完成时间，每次取max(time, lasttime + n) + 1
		- LRU Cache: Map + 双链表, 最开始把head和tail设置成dummy
	○ reservior sampling pick:  第p个元素被取的概率是 k /（p + 1）
		- 取k个，先把前k个当作候选元素，从第k + 1个开始遍历，第i个candidate有k/i的概率代替当前ans, Random r = new Random(),if ( r.nextInt(++count) == 0) ans = current;
		- random pick index: 遇到不是target的就跳过
		- 生成扫雷棋盘：先转换1-D再转成2-D， if (r.nextInt(i + 1)  < count) 选中第i个为雷
		- Random return number according to weight: 先把total weight算出来，然后random = rand.nextInt(weight)，然后二分法找random落在哪个区间里。刚开始要生成一个weight的数组，weight[i]代表所有0到i的和，这样weight[i]就是第i个的又边界。

# 注意事项
	○ 如果让设计一个数据结构，一开始要问清楚requirement和function signature，然后画图过一遍过程
	○ DFS和BFS的比较：iterate会更省memory，因为recursion会allocate stack的内存，而iteration allocate的是heap的内存，heap比stack大很多，如果recursion量太多的话会stack overflow（visited的时候定义成boolean会比定义成int更省空间）
怎么解释topological sort? b排在a后面，表示先完成a才能完成b
