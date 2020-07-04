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
