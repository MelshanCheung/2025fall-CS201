# Assignment #3: Stack, DP & Backtracking

Updated 2226 GMT+8 Sep 22, 2025  
2025 fall, Complied by 张珊珊，基础医学院  

>**说明：**  
>  
>1. **解题与记录：**  
>  
> 对于每一个题目，请提供其解题思路（可选），并附上使用 Python 或 C++编写的源代码（确保已在  
OpenJudge ， Codeforces，LeetCode 等平台上获得 Accepted “）。请将这些信息连同显示 Accepted”的  
截图一起填写到下方的作业模板中。（推荐使用 Typora https://typoraio.cn 进行编辑，当然你也可以选  
择 Word。）无论题目是否已通过，请标明每个题目大致花费的时间。  
>  
>2. **提交安排：**提交时，请首先上传 PDF 格式的文件，并将.md 或.doc 格式的文件作为附件上传至右侧的  
“ ”作业评论 区。确保你的 Canvas 账户有一个清晰可见的本人头像，提交的文件为 PDF “ ”格式，并且 作业评论 区  
包含上传的.md 或.doc 附件。  
>  
>3. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可  
能为你提供适当的延期或其他帮助。  
>  
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。  
## 1. 题目  
### 1078: Bigram 分词  
https://leetcode.cn/problems/occurrences-after-bigram/  
思路：  看到这种想到双指针
代码：  用时十分钟



	class Solution:
	  def findOcurrences(self, text: str, first: str, second: str) -> List[str]:
	
	    s = text.split()
	
	    left = 0
	
	    right = 1
	
	    res = []
	
	    while right<=len(s)-2:
	
	      if s[left]==first and s[right]==second:
	
	        res.append(s[right+1])
	
	      left+=1
	
	      right+=1
	
	    return res

![image-20251004015754845](/Users/rebecca/Library/Application Support/typora-user-images/image-20251004015754845.png)

### 283.移动零

stack, two pinters, https://leetcode.cn/problems/move-zeroes/

思路：  `left` 和 `right` 的关系：

- 在 `left` 之前的所有位置都是整理好的非零
  
- 在 `left` 和 `right` 之间的都是零
  
- `right` 负责探索未知区域
  

这样理解：**left标记了非零元素的边界，right负责寻找新的非零元素来扩充这个边界**。
代码：  

用时十五分钟

```  python

class Solution(object):

  def moveZeroes(self, nums):

  """

  :type nums: List[int]

  :rtype: None Do not return anything, modify nums in-place instead.

  """

  	left = 0

  	for right in range(len(nums)):

  		if nums[right]!=0:

  	nums[left],nums[right]=nums[right],nums[left]

  	left+=1
```
代码运行截图 <mark>（至少包含有"Accepted"）</mark> 
![image-20251004015900664](/Users/rebecca/Library/Application Support/typora-user-images/image-20251004015900664.png)

### 20.有效的括号  
stack, https://leetcode.cn/problems/valid-parentheses/  
思路：  用栈来解决的经典题目，二十分钟
代码：  

```python  
class Solution:

  def isValid(self, s: str) -> bool:

    pairs = []

    for c in s:

    if c in '([{':

    	pairs.append(self.pair(c))

    else:

    	if pairs and c==pairs[-1]:

    		pairs.pop()

    	else:

    		return False

    return not pairs

  		def pair(self,c):

  			if c =='(':

  					return ')'

  			if c=='[':

  					return ']'

  			return '}'
```
代码运行截图 <mark>（至少包含有"Accepted"）</mark>  
![image-20251004015929202](/Users/rebecca/Library/Application Support/typora-user-images/image-20251004015929202.png)

### 118.杨辉三角  
dp, https://leetcode.cn/problems/pascals-triangle/  
思路：  关键在于对齐数字
代码：  

```python  
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        ans = [[1]*(i+1) for i in range(numRows)]
        for i in range(2,numRows):
            for j in range(1,i):
                ans[i][j]=ans[i-1][j-1]+ans[i-1][j]
        return ans

        
```
代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20251004015457760](/Users/rebecca/Library/Application Support/typora-user-images/image-20251004015457760.png)

### 46.全排列  
backtracking, https://leetcode.cn/problems/permutations/  
思路：  用时二十分钟，标准的回溯题目
代码  

```python  
class Solution(object):
    def __init__(self):
        self.res = []
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        track = []
        used = [False]*len(nums)

        
        self.backtrack(track,nums,used)
        return self.res
    def backtrack(self,track,nums,used):
        if len(track)==len(nums):
            self.res.append(track[:])
            return
        for i in range(len(nums)):
            if used[i]:
                continue
            track.append(nums[i])
            used[i] = True
            self.backtrack(track,nums,used)
            track.pop()
            used[i] = False
        
        
```
<mark>（至少包含有"Accepted"）</mark>  

![image-20251004013445028](/Users/rebecca/Library/Application Support/typora-user-images/image-20251004013445028.png)

### 78.子集

backtracking, https://leetcode.cn/problems/subsets/  
思路：  用时二十五分钟，这道题不一样在于一时间没有想到base条件，子集问题中顺序不重要，用start控制即可。相当于每次递归都要append到res里面记录，刚好和上一道题目对比
代码  

```python  

class Solution:
    def __init__(self):
        self.res = []
    def subsets(self, nums: List[int]) -> List[List[int]]:
        track = []
        
        self.backtrack(nums,track,0)
        return self.res
    def backtrack(self,nums,track,start):
        self.res.append(track[:])
        n = len(nums)
        if len(track)==len(nums):
            return
        for i in range(start,n):
            track.append(nums[i])
            
            self.backtrack(nums,track,i+1)
            
            track.pop()
```
<mark>（至少包含有"Accepted"）</mark>  

![image-20251004014904296](/Users/rebecca/Library/Application Support/typora-user-images/image-20251004014904296.png)

## 2. 学习总结和个人收获  
<mark> “如果发现作业题目相对简单，有否寻找额外的练习题目，如 数算 2025fall ”每日选做 、LeetCode、  
Codeforces、洛谷等网站上的题目。</mark>

## N皇后问题

---

国际象棋中，皇后可以攻击同一行、同一列和同一条对角线上的任意单位。N 皇后问题是指在一个 N×N 的棋盘上摆放 N 个皇后，要求任何两个皇后之间都不能互相攻击。

换句话说，就是让你在一个 N×N 的棋盘上放置 N 个皇后，使得每行、每列和每个对角线都只有一个皇后。

对于任意一个皇后，它所在的行、列和对角线（左上、右上、左下、右下）都没有其他皇后，所以这就是一个符合规则的解。


**51. N 皇后** | [力扣](https://leetcode.cn/problems/n-queens/) | [LeetCode](https://leetcode.com/problems/n-queens/) |  🔴

按照国际象棋的规则，皇后可以攻击与之处在同一行或同一列或同一斜线上的棋子。

**n 皇后问题** 研究的是如何将 `n` 个皇后放置在 `n×n` 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 `n` ，返回所有不同的 **n 皇后问题** 的解决方案。

每一种解法包含一个不同的 **n 皇后问题** 的棋子放置方案，该方案中 `'Q'` 和 `'.'` 分别代表了皇后和空位。

**示例 1：**



**输入：**n = 4
**输出：**[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
**解释：**如上图所示，4 皇后问题存在两个不同的解法。

**示例 2：**

**输入：**n = 1
**输出：**[["Q"]]

**提示：**

- `1 <= n <= 9`

**题目来源：[力扣 51. N 皇后](https://leetcode.cn/problems/n-queens/)。**

## 思路

---

其实n皇后和数独的解法一样，区别在于

1.数独的规则和 N 皇后问题的规则不同，我们需要修改 `isValid` 函数，判断一个位置是否可以放置皇后。
2.要找到所有解，所以要去除提前终止
但 N 皇后问题相对数独游戏还有一个优化：**我们可以以行为单位进行穷举，而不是像数独游戏那样以格子为单位穷举**。

举个直观的例子，在数独游戏中，如果我们设置 `board[i][j] = 1`，接下来呢，要去穷举 `board[i][j+1]` 了对吧？而对于 N 皇后问题，我们知道每行必然有且只有一个皇后，所以如果我们决定在 `board[i]` 这一行的某一列放置皇后，那么接下来就不用管 `board[i]` 这一行了，应该考虑 `board[i+1]` 这一行的皇后要放在哪里。

所以 N 皇后问题的穷举对象是棋盘中的行，每一行都持有一个皇后，可以选择把皇后放在该行的任意一列。

```python
class Solution:
	def __init__(self):
		self.res = []
		
	def solveNQueens(self,n):
		board = ['.' *n for _ in range(n)]
		self.backtrack(board,0)
		return self.res
	
	def backtrack(self,board,row):
		if row==len(board):
			self.res.append(board[:])
			return
		
		n = len(board)
		for col in range(n):
			if not self.isValid(board,row,col):
				continue
			board[row] = board[row][:col]+'Q'+board[row][col+1:]
			self.backtrack(board,row+1)
			board[row] = board[row][:col]+'.'+board[row][col+1:]
	
	def isValid(self,board,row,col):
		n = len(board)
		for i in range(row):
			if board[i][col]=='Q':
				retur False
		for i,j in zip(range(row - 1, -1, -1), range(col + 1, n)):
			if board[i][j]=='Q':
				retur False
		for i, j in zip(range(row - 1, -1, -1), range(col - 1, -1, -1)): 
			if board[i][j] == 'Q': 
				return False 
		return True
```

假设 `n=4`，当前位置是 `(2,2)`，检查从 `(2,2)` 出发的两个对角线：

```
棋盘示意图（Q在(2,2)）：
. . . .
. \ . /
. . Q .
. . . .

右上对角线：从(1,3)开始向上
左上对角线：从(1,1)开始向上
```

## 总结思考

---

`range(row-1,-1,-1)`从`row-1`到`0`，步长为`-1`，向上遍历
`range(col+1,n)`从`col+1`到`n-1`，步长为`1`，向右遍历
`zip()`把两个范围配对形成对角线坐标
`for i, j in zip(range(row-1,-1,-1),range(col+1,n-1,1)`