// 给定一个单词列表，只返回可以使用在键盘同一行的字母打印出来的单词。
```
var findWords = function(words) {
    let arr=[]
    const obj={q:0,w:0,e:0,r:0,t:0,y:0,u:0,i:0,o:0,p:0,
      a:1,s:1,d:1,f:1,g:1,h:1,j:1,k:1,l:1,
      z:2,x:2,c:2,v:2,b:2,n:2,m:2
    }
    words.map(item=>{
        let str=item.toLocaleLowerCase()
        let n=obj[str[0]]   
        if(item.toLocaleLowerCase().split('').every(c=>obj[c]===n)){    
            arr.push(item)
        }
        }
    )
return arr
};
```
// 给定一个偶数长度的数组，其中不同的数字代表着不同种类的糖果，每一个数字代表一个糖果。你需要把这些糖果平均分给一个弟弟和一个妹妹。返回妹妹可以获得的最大糖果的种类数。
```
var distributeCandies = function(candies) {
    const unique=new Set(candies)
    let n=candies.length
    return unique.size>n/2?n/2:unique.size
};
```
// stack
//用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/
```
var CQueue = function() {
    this.stack1=[]
    this.stack2=[]
};

/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.stack1[this.stack1.length]=value
};

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    if(!this.stack2.length){
        let tep
        while((tep=this.stack1.pop())){
            this.stack2.push(tep)
        }
    }
    if(!this.stack2.length){
        return -1
    }else{
        return this.stack2.pop
    } 
};

/**
 * Your CQueue object will be instantiated and called as such:
 * var obj = new CQueue()
 * obj.appendTail(value)
 * var param_2 = obj.deleteHead()
 */
```
//给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

```
var isValid = function(s) {
    let arr = []
    let len = s.length
    if (len%2) return false
    for (let i = 0; i < len; i++) {
        let letter = s[i]
        switch(letter) {
            case "(": {
                arr.push(letter)
                break;
            }
            case "[": {
                arr.push(letter)
                break;
            }
            case "{": {
                arr.push(letter)
                break;
            }
            case ")": {
                if (arr.pop() !== "(") return false
                break;
            }
            case "]": {
                 if (arr.pop() !== "[") return false
                break;
            }
            case "}": {
                if (arr.pop() !== "{") return false
                break;
            }
        }
    }
    return !arr.length
};
```
// 给定两个 没有重复元素 的数组 nums1 和 nums2 ，其中nums1 是 nums2 的子集。找到 nums1 中每个元素在 nums2 中的下一个比其大的值。

```
var nextGreaterElement = function(nums1, nums2) {
  let stack = []
  let res = []
  let map = new Map()
  let len=nums2.length
  for(let i=len-1;i>=0;i--){
    while(stack.length&&nums2[i]>=stack[stack.length-1]){
      stack.pop()
    }
    map.set(nums2[i],stack.length?stack[stack.length-1]:-1)
    stack.push(nums2[i])
  }
  nums1.forEach(i=>{
    res.push(map.get(i))
  })
  return res
  
};
```
//请设计一个栈，除了常规栈支持的pop与push函数以外，还支持min函数，该函数返回栈元素中的最小值。执行push、pop和min操作的时间复杂度必须为O(1)。


var MinStack = function() {
    this.stack=[]
    this.helpStack=[]
    this.length=0
};

MinStack.prototype.push = function(x) {
    const length=this.length
        this.stack[length]=x
    if (!length || this.helpStack[length - 1] > x) {
        this.helpStack[length]=x
    }else{
        this.helpStack[length]=(this.helpStack[length-1])
    }

    this.length=length+1
};


MinStack.prototype.pop = function() {
    const length=this.length
    this.length=length-1
    return this.stack[length-1]
};


MinStack.prototype.top = function() {
    return this.stack[this.length-1]
};


MinStack.prototype.getMin = function() {
    console.log(this.helpStack)
    return this.helpStack[this.length-1]
};
//输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。
```
var maxDepth = function(root) {
    if(!root) return 0
    return (Math.max(maxDepth(root.left),maxDepth(root.right)))+1
    
};
```

// 872
```
var leafSimilar = function(root1, root2) {
    function getValue(root,arr){
        if(root===null){
            return
        }
        getValue(root.left,arr)
        getValue(root.right,arr)
        if(root.left===null&&root.right===null){
            arr.push(root.val)
        }
    } 
    let arr1=[]
    let arr2=[]
    getValue(root1,arr1)
    getValue(root2,arr2)
    if(arr2.length!==arr1.length){
        return false
    }
    for(let i=0;i<arr1.length;i++){
        if(arr1[i]!==arr2[i]){
            return false
        }
    }
    return true
};
```
// 现在输入一个公司的所有员工信息，以及单个员工id，返回这个员工和他所有下属的重要度之和。
```
var GetImportance = function(employees, id) {
    let importance=0
    let leader=employees.filter(i=>i[0]===id)[0]
    importance+=leader[1]
    console.log(importance)
    let slaves=leader[2]
    slaves.forEach(item=>{
      importance+=getNumber(employees,item)
    })
    console.log(importance)
};
var getNumber=(employees, id)=>{
    let target=employees.filter(i=>i[0]===id)[0]
   return target[1]
}
GetImportance([[1,2,[2]], [2,3,[]]],2)
```
// 给定一个有序整数数组，元素各不相同且按升序排列，编写一个算法，创建一棵高度最小的二叉搜索树。
```
var sortedArrayToBST = function(nums) {
    if(nums.length===0){
        return null
    }
    let m = parseInt(nums.length/2)
    let root = new TreeNode(nums[m])
    root.left=sortedArrayToBST(nums.slice(0,m))
    root.right=sortedArrayToBST(nums.slice(m+1))
    return root
};
```
// 给定一个二叉树，找出其最小深度。最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
```
var minDepth = function(root) {
    if(root===null){
        return 0
    }
    let left=root.left
    let right=root.right
    if(left && right){
        return 1 + Math.min(minDepth(left),minDepth(right))
    }if(left){
        return 1 + minDepth(left)
    }if(right){
        return 1 + minDepth(right)
    }
    return 1
};
```
// 写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.

```
var fib = function(n) {
    if(n<=1) return n
    let a=b=1,c=0
    while(n-->0){
        a=b,
        b=c,
        c=(a+b)%1000000007
    }
    return c
};
```
//将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。
```
var sortedArrayToBST = function(nums) {
    if(!nums.length){return null}
    var helper=(left,right)=>{
        if(left>right)return null
        let mid=Math.floor((left+right)/2)
        let root=new TreeNode(nums[mid])
        root.left=helper(left,mid-1)
        root.right=helper(mid+1,right)
        return root
    }
    return helper(0,nums.length-1)
};
```
//给定一个二叉树，返回所有从根节点到叶子节点的路径。
```
var binaryTreePaths = function(root) {
    let result=[]
    var xxx=(node,payLoad)=>{
        if(!node) return []
        payLoad.push(node.val)
        if(node.left===null&&node.right===null){
            return result.push(payLoad.join('->'))
        }
        if(node.left){
            xxx(node.left,[...payLoad])
        }
        if(node.right){
            xxx(node.right,[...payLoad])
        }
    }
    xxx(root,[])
    return result
}
```
// 在一个「平衡字符串」中，'L' 和 'R' 字符的数量是相同的。

给出一个平衡字符串 s，请你将它分割成尽可能多的平衡字符串。

返回可以通过分割得到的平衡字符串的最大数量。

```
var balancedStringSplit = function(s) {
    let total = 0
    let count=0
    for(let x of s){
        total += x==='R'?-1:1
        if(total === 0){
            count+=1
        }
    }
    return count
};
```
//判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。
```
var isPalindrome = function(x) {
    if(x<0 || (x%10===0&&x!==0)){return false};
    let reverse=0
    while(x>reverse){
        reverse=reverse*10+x%10
        x=Math.floor(x/10)
    }
    return x===reverse || x===Math.floor(reverse/10)
};
```
//给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。

字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000

```
var romanToInt = function(s) {
    const map = {
        I : 1,
        IV: 4,
        V: 5,
        IX: 9,
        X: 10,
        XL: 40,
        L: 50,
        XC: 90,
        C: 100,
        CD: 400,
        D: 500,
        CM: 900,
        M: 1000
    };
    let ans=0
    for(let i=0;i<s.length;){
        if(i+1<s.length && map[(s.substring(i,i+2))]){
            ans += map[(s.substring(i,i+2))]
            i+=2
        }
        else{
            ans += map[(s.substring(i,i+1))]
            i++
        }
    }
    return ans
};
```
// 编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

```
var longestCommonPrefix = function(strs) {
    if(strs.length===0)return ''
    let ans=strs[0]
    for(let i=1;i<strs.length;i++){
        let k = 0
        for(;k<ans.length&&k<strs[i].length;k++){
            if(ans[k]!==strs[i][k]){
                break;
            }
        }
        ans=ans.substring(0,k)
        if(ans === "")return ans;
    }
    return ans
};
```
//将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
```
// 迭代
var mergeTwoLists = function(l1, l2) {
    const prehead=new ListNode(-1)
    let pre=prehead
    while(l1!==null && l2!==null){
        if(l1.val<l2.val){
            pre.next=l1
            l1=l1.next
        }
        else{
            pre.next=l2
            l2=l2.next
        }
        pre=pre.next
    }
    pre.next= l1===null?l2:l1
    return prehead.next
};
// 递归
var mergeTwoLists = function(l1, l2) {
    if(l1===null)return l2
    if(l2===null)return l1
    if(l1.val<=l2.val){
        l1.next=mergeTwoLists(l1.next,l2)
        return l1
    }
    l2.next=mergeTwoLists(l1,l2.next)
    return l2
}
```

// 给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

```
var removeDuplicates = function(nums) {
    let n=0
    for(let i=1;i<nums.length;i++){
        if(nums[n]!==nums[i]){
            n++
            nums[n]=nums[i]
        }
    }
    return n+1
};
```
//给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
```
var removeElement = function(nums, val) {
    let n=0
    for(let i=0;i<nums.length;i++){
        if(nums[i]!==val){
            nums[n]=nums[i]
            n++
        }
    }
    return n
};
```
//实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。


```
var strStr = function(haystack, needle) {
    if(!needle) return 0
    let n=0
    let length=needle.length
    for(let i=0;i<=haystack.length-length;i++){
        if(haystack.slice(i,i+length)===needle){
            return i
        }
    }
    return -1
};
```
//给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。
```
var searchInsert = function(nums, target) {
    let n=0
    let m=nums.length-1
    while(n<=m){
        let mid=n+parseInt((m-n)/2)
        if(nums[mid]>=target){
            m=mid-1
        }else{
            n=mid+1
        }
    }
    return n
};
```
//计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。
```
var mySqrt = function(x) {
    if(x<=1)return x
    let r = x>>>1
    let l = 1
    while(l+1<r){
        let mid = (l+r)>>>1
        if(mid*mid===x){
            return mid
        }
        if(mid*mid>x){
            r=mid
        }else{
            l=mid
        }
    }
    return r*r>x?l:r
};
```
//给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。

说明:

返回的下标值（index1 和 index2）不是从零开始的。
你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。
```
//二分
var twoSum = function(numbers, target) {
    for(let i=0;i<numbers.length;i++){
        let left=i+1
        let right=numbers.length
        while(left<right){
            let mid = (left+right)>>>1
            if(numbers[i]+numbers[mid]<target){
                left=mid+1
            }else if(numbers[i]+numbers[mid]>target){
                right=mid
            }else{
                return [i+1,mid+1]
            }
        }
    }
    
};
//双指针
var twoSum = function(numbers, target) {
    let low=0
    let high=numbers.length-1
    while(low<high){
        if(numbers[low]+numbers[high]>target){
            high--
        }else if(numbers[low]+numbers[high]<target){
            low++
        }else{
            return [low+1,high+1]
        }
    }
    
};
```
//假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。
```
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
        let left = 1
        let right = n
        while(left<right){
            let mid= (left+right) >>>1
            if(isBadVersion(mid)){
                right=mid
            }else {
                left=mid+1                
            }
        }
        return right

    };
};
```
// 给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。
```
var isPerfectSquare = function(num) {
    if(num===1)return true
    let left=2
    let right=num>>>1
    while(left<=right){
        let mid = (left+right)>>>1
        if(mid*mid<num){
            left=mid+1
        }else if(mid*mid>num){
            right=mid-1
        }else{
            return true
        }
    }
    return false
};
```
