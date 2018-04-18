# 关于函数

## 不要在非函数语句块里（if while 等块级语句）声明函数
参考链接：[Airbnb Function][Airbnb]

> Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.

> Note: ECMA-262 defines a block as a list of statements. A function declaration is not a statement. Read ECMA-262's note on this issue.

    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    var test;
    if (currentUser) {
      test = function test() {
        console.log('Yup.');
      };
    }

关于解答：
[segmentFault][sf1]

    console.log(typeof foo);
    function foo(){ return 1; }
    console.log(typeof foo);
    
上面这段代码在各个浏览器中有一样的结果："function"、"function"。

这是没有浏览器差异的行为，原因是函数声明提升（Function Declaration Hoisting）。
不明白函数声明提升，或者连函数声明和函数表达式的分别都不太清楚，可以看看汤姆大叔的《揭秘命名函数表达式》。

表达式和声明存在着十分微妙的差别。函数声明会在任何表达式被解析和求值之前先被解析和求值，即使你的声明在代码的最后一行，它也会在同作用域内第一个表达式之前被解析/求值。

      console.log(typeof foo);
      if (true) {
        function foo(){ return 1; }
      }
      console.log(typeof foo);
      
上面这段代码在Gecko引擎中打印"undefined"、"function"；而在其他浏览器中则打印"function"、"function"。

原因在于Gecko加入了ECMAScript以外的一个feature：条件式函数声明。

> Conditionally created functions
Functions can be conditionally declared, that is, a function declaration can be nested within an if statement.

> Note: Although this kind of function looks like a function declaration, it is actually an expression (or statement), since it is nested within another statement. See differences between function declarations and function expressions.

**注意引用的Note：条件式函数声明跟函数表达式的处理方式一样。因此，条件式函数声明丧失了函数声明提升的特性。**
基于以上原因，请不要在你的代码里将函数声明嵌套在条件语句内。



[Airbnb]:https://github.com/airbnb/javascript/blob/b4d8543f120ba761ae7f39caf850c1e4efdc2727/es5/README.md
[sf1]:https://segmentfault.com/q/1010000000731247/a-1020000000732024
