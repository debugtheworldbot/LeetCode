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
