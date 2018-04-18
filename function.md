# 关于函数

## 不要在if while等语句声明函数
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

[Airbnb]:https://github.com/airbnb/javascript/blob/b4d8543f120ba761ae7f39caf850c1e4efdc2727/es5/README.md
