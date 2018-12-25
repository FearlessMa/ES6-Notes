README#ES6学习
[阮一峰ES6](http://es6.ruanyifeng.com/ES6.md#docs/let)
##1.变量（let&const） 
**变量 es5及以前使用var，ES6新let、const。**
###1.1 var
```
// 变量var
    // a.作用域：函数级
        function v1(){
            var v = 1;
        }
        // console.log(v); //v is not defined
        if(true){
            var m = 2;
        }
        console.log(m); //2
    // b.可重复声明
        var a = 1;
        var a = 2;
        console.log(a); //2
    // a = 2
    // c.常量（无，约定变量名称全大写代表常量）
        var PI = 3.14 ;
    // PI还是可以被重新赋值。
        PI = 123;
        console.log(PI);//123
    //变量提升
    console.log(m);//undefined
    var m = 2;
```
###1.2 let&const 
```
 // es6中let,const
    // a.作用于：块级 - {}花括号
        if(true){
            let m = 1;
            const m1 = 2;
        }
        //console.log(m); // m is not defined
        //console.log(m1); // m1 is not defined
    // b.不可重复声明
    // 变量let
        let a = 1;
        //a = 3 ;         //栈中存储可以改变。
        //let a = 2;      //Uncaught SyntaxError: Identifier 'a' has already been
    // 常量const
        const b = 1;
       // b = 2 ;         //栈中存储不可改变。Uncaught TypeError: Assignment to constant variable
        //const b = 3;    //Uncaught SyntaxError: Identifier 'b' has already been declared
    // 声明引用类型可改变其内部的值。**引用的栈中的地址不可改变，对应堆中存储内容可改变。
        const c = {a:1,b:2};
        c.a=123; //可以修改
        console.log(c);//{a: 123, b: 2}
    //变量提升
        console.log(m1); //报错
        let m1 = 3;
```
##2.变量的解构赋值
**ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。**

    //等号两边结构相同就可以解构
    let [a,b,c] = [1, 2, 3]; //a=1,b=2,c=3
    
    let [f,g,h] = [1,{a:1},[1,2,3]]//f=1, g={a:1}, h=[1,2,3]
    
    let [foo, [[bar], baz]] = [1, [[2], 3]];
    foo // 1
    bar // 2
    baz // 3
    
    let [ , , third] = ["foo", "bar", "baz"];
    third // "baz"
    
    let [x, , y] = [1, 2, 3];
    x // 1
    y // 3
    
    let [head, ...tail] = [1, 2, 3, 4];
    head // 1
    tail // [2, 3, 4]
    
    let [x, y, ...z] = ['a'];
    x // "a"
    y // undefined
    z // []
**解构赋值允许默认值**
    
    let [foo = true] = [];
    foo // true
    
    let [x, y = 'b'] = ['a']; // x='a', y='b'
    let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
    
##3.字符串扩展
###3.1 es6之前字符串方法

    /***
         *  属性
         *      1. str.length
         *      2. str.constructor
         *      3. str.prototype
         *  方法
         *      1. let str = new String('abc');  //或 str = 'abc';
         *      2. str.charAt(1);     //返回索引1处的字符'b'
         *      3. str.charCodeAt(); //返回指定位置字符的Unicode码
         *      3. let newStr = str.concat('def');  //拼接两个或多个字符串，返回新的字符串
         *      4. String.fromCharCode(98); //接受一个或多个Unicode值返回字符
         *      5. str.indexOf('a');    //  返回检索指定字符串第一出现的位置，下标
         *      6. str.lastIndexOf('a');    //返回检索指定字符串最后一次出现的位置
         *      7. str.match();     // 找出一个或多个正则表达式的匹配,参数为想要匹配的正则
         *      8. str.replace(/a/ig,'aaa');  //替换与正则匹配的子串
         *      9. str.search(/b/);     //stringObject 中第一个与 regexp 相匹配的子串的起始位置。
         *     10. str.slice(startNum,endNum);      //提取字符串的片段，并返回新的字符串
         *     11. str.split();     //把字符串分割为字符串数组
         *     12. str.substr();    //从起始索引位置提取指定数目的字符
         *     13. str.substring();     //提取字符串中指定两个索引之间的字符
         *     14. str.toLocaleLowerCase();      //根据主机环境，把字符串转换为小写
         *     15. str.toLocaleUpperCase();      //根据主机环境，把字符串转换为大写
         *     16. str.toLowerCase();
         *     17. str.toUpperCase();
         *     18. any.toString();      //返回任意类型的字符串化值
         *     19. valueOf();       //返回字符串对象的原始值
         *
         ***/

###3.2 es6扩展
**3.2.1 includes(),startsWith(),endsWith()**
- includes()    ——返回布尔值，表示是否找到了参数字符串。
- startsWith()  ——返回布尔值，表示参数字符串是否在元字符串的头部。
- endsWith()    ——返回布尔值，表示参数是否在原字符串的尾部。
    
    
    //新方法
        // startsWith()
        
        let s = 'hello word !';
        let b1 = s.startsWith('hello');
        console.log(b1);    //true
        
        // endsWith()
        
        let b2 = s.endsWith('!');
        console.log(b2);    //true
        
        // includes()
        
        let b3 = s.includes('l');
        console.log(b3);    //true
        
    这三个方法支持第二个参数
        endsWith()第二个参数表示前n个字符。
        startsWith(),includes()表示从第n个字符位置到结束

        // 第二参数
            /***
             * endsWith()第二个参数表示前n个字符。
             * startsWith(),includes()表示从第n个字符位置到结束
             ***/
        
            b1 =s.startsWith('hello',6);
            console.log(b1); //false
        
            b2 = s.endsWith('!',12);
            console.log(b2); //true
        
            b3=s.includes('word',3);
            console.log(b3); //true

**3.2.2 padStart(),padEnd()**
    
    //padStart(),padEnd()
        /***
         *  padStart()在字符串头部补全
         *  padEnd()在字符串尾部补全
         *  方法接受2各参数
         *  1.第一个参数为指定返回字符串的长度
         *  2.第二个参数补全的字符串
         ***/
    
            let p = 'a';
    
            let p1 = p.padStart(3,'s');
            console.log(p1);    //ssa
            p1= p.padStart(3,'ssssss');
            console.log(p1);    //ssa
    
            let p2 = p.padEnd(3,'s');
            console.log(p2);    //ass
            p2 = p.padEnd(3,'ssssss');
            console.log(p2);    //ass
            
**3.2.3 模板字符串**     
    
    //模板字符串
        /***
         *  模板字符串
         *  1.`${变量}字符串`
         *  2.模板字符串中可调用函数
         ***/
         
            let m = 'M';
            let m1 = `${m}hc`;
            console.log(m1);    //Mhc
    
            let fun = m=>m;
            m1 = `${fun('hello')} word !`;
            console.log(m1);       
**3.2.4 repeat()**
```
 //repeat()
    /***
     * let str = str1.repeat(n); n>=0 ; n若为字符串先默认转换成数字
     * repeat方法将返回一个新的字符串，新字符串将原字符串重复n此
     *
     ***/

        let str1 = 'abc';
        let str = str1.repeat(2);
        console.log(str);   //abcabc

        str = str1.repeat('2');
        console.log(str); //abcabc

        str = str1.repeat('abc');
        console.log(str);   // " "
```
##4. Number

**Number比较常用的方法**
```
/***
     *  Number
     *      es6方法
     *          1.Number.isFinite() //判断是否为有限数字
     *          2.Number.isNaN()    //判断一个值是否为NaN
     *          3.Number可以调用 parseInt(),parseFloat()
     *          4.Number.isInteger() //判断是否为整数
     *      Math扩展
     *          Math.trunc() //去除一个值的小数部分
     *          其他省略。。。
     *
     *       es5方法
     *          num.toFixed(x)  //转换为保留x位的小数
     *       Math方法
     *          Math.round(x)   //把x四舍五入为最接近的整数
     *          Math.random()   //随机生成0-1之间的随机数
     *          Math.max(x,y,z,....,n)  //返回最大值
     *          Math.min(x,y,z,....,n)  //返回最小值
     *          Math.floor(x)       //对x进行下取整
     *          其他省略。。。
     *
     *
     ***/
```










##2.箭头函数
        // es5
        function a(m){
            return m;
        }
        console.log(a(1));//1
        // es6箭头函数
        let b = (m)=>{
            return m;
        }
        console.log(b(1));//1
        // 若参数只有一个可省略小括号。
        let c = m=>{
            return m;
        }
        console.log(c(2));//2
        //若函数内部只有一行代码且是返回值 可省略花括号和return
        let d = m=>m+1;
        console.log(d(2));//3
        
        // TODO this的指向问题