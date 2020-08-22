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
