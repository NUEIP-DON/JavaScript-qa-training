# JavaScript 測驗

## 概述

這是一個基於JavaScript的測驗，旨在評估 QA Team 在 JavaScript 的基礎知識和編程能力。

## 題目

### 1. 基礎知識

1. **變數與資料類型**：請解釋`let`、`const`和`var`的區別。

```javascript
區別1. variable scope:var可以在宣告的block外使用,而let/const不可在宣告的block外使用

{
var x1 = "killua";
}
console.log(x1); //killua

{
let x2 = "killua";
}
console.log(x2);//x2 is not defined

{
const x3 = "killua";
}
console.log(x3);//x3 is not defined

```
```javascript
區別2.hoisting:var會提升宣告,但賦值不提升/let、const不會提升
console.log(x1); // undefined,不會報錯
var x1 = 5 ;

console.log(x1);//Uncaught ReferenceError: Cannot access 'x1' before initialization
let x1 = 5 ;

console.log(x1);//Uncaught ReferenceError: Cannot access 'x1' before initialization
const x1 = 5 ;
```
```javascript
區別3.重複宣告：var重複宣告,後者會覆蓋前者/let、const不允許重複宣告
var x1 = 5;
var x1 = 7;
console.log(x1); var x1可印出7

let x1 = 5;
let x1 = 7;//Uncaught SyntaxError: Identifier 'x1' has already been declared
console.log(x1);

const x1 = 5;
const x1 = 7;//Uncaught SyntaxError: Identifier 'x1' has already been declared
console.log(x1);
```

```javascript
區別4.const 必須賦值

const x1;//Uncaught SyntaxError: Missing initializer in const declaratio

const x1 = 4;
x1 = 5;// 不可修改，Uncaught TypeError: Assignment to constant variable.

const x1 = {name:"killua"};
x1.name = "don";//物件內部屬性可修改
console.log(x1.name); 
x1 = {age:15};//不可修改，Uncaught TypeError: Assignment to constant variable.

```
---

2. **函數**：如何定義一個函數？箭頭函數和傳統函數有何不同？

```javascript
2-1:如何定義一個函數？

方法a.函式宣告（Function Declaration）
function killua(number) {
    return number * number;
}
方法b.函式運算式（Function Expressions）
var killua = function (number) {
    return number * number;
};//匿名函式，不會被hoisted

2-2:箭頭函數和傳統函數有何不同？
傳統函式會有表達式（Expression）和宣告式（Declaration）兩種表達方式。

const killua_Expression = function (arg1) {return console.log(arg1)};//表達式
function killlua_Declaration (arg1) {return console.log(arg1)};//宣告式

// Arrow function僅有表達式（Expression）一種寫法
const Arrow_killua1 = (arg1) => {return console.log(arg1)};
//當參數多於一個的時候，一定要寫小括號
const Arrow_killua2 = (arg1, arg2) => {return console.log(arg1,arg2)};
// 如果參數只有一個，可以選擇是否省略小括號 “()”
const Arrow_killua3 = arg1 => {return console.log(arg1)};
// 如果 return 的值只有一行，則一樣可以省略大括號 {} 和 return，若多餘一行則需維持 {} & return
const Arrow_killua4 = arg1 => console.log(arg1);

// 多於一行的情況如下
const Arrow_killua5 = arg2 => {
    const myName = "killua_0604";
    return console.log(myName);
};
// 如果要 return Object，則需要特別加上小括號
const Arrow_killua6 = arg1 => ({key1: arg1 * 100, key2: arg1 * 200});

```

3. **陣列方法**：請解釋`map`、`filter`和`reduce`的用途。

```javascript
map():將原本的陣列，透過函式內所回傳的值組合成另一個陣列,而不影響原本的陣列，
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(function(item) {
return item * 2;
})
console.log(doubled); // [2, 4, 6, 8]

filter():會回傳一個陣列，條件是return為true的物件
const numbers = [1, 2, 3, 4];
const evens = numbers.filter(function(item){
    return item%2==0;
});
console.log(evens); 

reduce():將一個累加器及陣列中每項元素（由左至右）傳入函式，最後return 一個值。
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce(function (result, item) {
console.log(result);//100,101,103,106
console.log(item);//1,2,3,4
return result + item;
}, 100);//result initial 的值
console.log(sum); // 110
```

### 2. 編程練習

1. **FizzBuzz**：
  寫一個函數，對於1到100的數字：
  - 如果數字可以被3整除，則輸出"Fizz"
  - 如果數字可以被5整除，則輸出"Buzz"
  - 如果數字可以被3和5都整除，則輸出"FizzBuzz"
  - 否則，輸出該數字。


  ```javascript
  解法1:
  function fizzBuzz() {
    for (let i = 1; i <= 100; i++) {
        if (i % 3 === 0 && i % 5 === 0) {//因為可同時被3與5整除,代表一定可以被3or5整除,所以在最前面先判斷,若滿足條件則輸出FizzBuzz
            console.log("FizzBuzz");
        } else if (i % 3 === 0) {//如果3可以整除則輸出Fizz
            console.log("Fizz");
        } else if (i % 5 === 0) {
            console.log("Buzz");//如果5可以整除則輸出Buzz
        } else {
            console.log(i);//如果都不是代表不能被3or5整除,輸出數字
        }
    }
  }
  ```
  ```javascript
  解法2:建立陣列並使用foreach遍歷陣列
    const emptyArray = [];
    for (let i = 1; i <= 100; i++) {
    emptyArray.push(i);
    }

    const newArray = [];

    emptyArray.forEach(number => {
    if (number % 3 === 0 && number % 5 === 0) {
        newArray.push("FizzBuzz");
    } else if (number % 3 === 0) {
        newArray.push("Fizz");
    } else if (number % 5 === 0) {
        newArray.push("Buzz");
    } else {
        newArray.push(number);
    }
    });

    console.log(newArray);
  ```
  ```javascript
  解法3:建立陣列並利用map將結果存為新陣列
    const emptyArray = [];
    for (let i = 1; i <= 100; i++) {
        emptyArray.push(i);
    }

    const newArray = emptyArray.map(number => {
    if (number % 3 === 0 && number % 5 === 0) {
        return "FizzBuzz";
    } else if (number % 3 === 0) {
        return "Fizz";
    } else if (number % 5 === 0) {
        return "Buzz";
    } else {
        return number;
    }
    });

    console.log(newArray);
  ```

2. **陣列操作**：
  給定一個數字陣列，例如`[1, 2, 3, 4, 5]`，請寫一個函數返回一個新陣列，其中每個元素都乘以2。

  ```javascript
  const array=[1,2,3,4,5];//原始的數字陣列
  const double_array=array.map(function(x){return x*2});//返回原始陣列且每個元素值*2
  //const double_array_2 = array.map(x => x * 2);箭頭函式寫法
  console.log(double_array);//印出返回的陣列
  ```

3. **使用 axios 取得 API 資料**：
  請使用 `axios` 函式庫，從以下的 API 端點取得資料：
  > https://jsonplaceholder.typicode.com/posts

  當資料成功取得後，請將該文章的標題（title）以及內文（body）渲染至畫面上。

```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>使用 axios 取得 API 資料</title>
        <style>
            body {<!-- 設定背景黑色文字白色 -->
                background-color: black; 
                color: white; 
            }
        </style>
    </head>
    <body>
        <div id="container"><!-- 定義容器用於裝文章內容 -->
        </div>

        <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script><!-- 引入Axios套件 -->
        <script>
            axios.get('https://jsonplaceholder.typicode.com/posts')//發送get請求
                .then(function (response) {

                    const hunter = response.data;//獲取文章資料

                    hunter.forEach(function (item) {
                        var container = document.getElementById('container');
                        container.innerHTML += `
                            <div class="content">
                                <h2>${item.title}</h2>
                                <p>${item.body}</p>
                            </div>
                        `;//將文章內容塞進容器
                    });
                })
                .catch(function (error) {
                    console.error(error);
                });
        </script>
</body>
</html>


```

### 3. 進階問題

1. **`this` 關鍵字**：
  - a.請解釋 JavaScript 中的 `this` 關鍵字。
  - b.在哪些情境下，`this` 的值會改變？
  - c.`this` 在箭頭函數和傳統函數中有什麼不同？
  - d.請給出一個例子展示箭頭函數和傳統函數中 `this` 的差異。

```javascript
    a.請解釋 JavaScript 中的 `this` 關鍵字。
    - this 是 JavaScript 的一個關鍵字。
    - this 是 function 執行時，自動生成的一個內部物件。
    - 隨著 function 執行場合的不同，this 所指向的值，也會有所不同。
    - 在大多數的情況下， this 代表的就是呼叫 function 的物件 (Owner Object of the function)。
```

```javascript
    b.在哪些情境下，`this` 的值會改變？
    
    1.直接呼叫的函式，this 會指向全域
    function hunter() {
    var name = 'function奇犽'
    console.log(this.name)
    }
    var name = '全域奇犽'
    hunter()   // output: 全域奇犽
    -----------------------------------------------------------
    2.哪個物件去呼叫了函式，函式內的 this 就會指向該物件
    function hunter() {
    console.log(this.name)
    }

    var obj1 = {
        name: '揍敵客奇犽',
        hunter:hunter
    }

    var obj2 = {
        name: '獵人奇犽',
        hunter:hunter
    }

    obj1.hunter()//揍敵客奇犽
    obj2.hunter()//獵人奇犽

    - 物件中使用map函式
    const hunter = {
        name: '奇犽',
        family: ['揍敵客'],
        hunterfn: function() {
            this.family.map(function(item){
            console.log(this); // window 物件
            })
        }
    }
    hunter.hunterfn();//this指向window
    /*傳統函式宣告的位置並不會影響 this 指向的值，重要的是呼叫的方法，如果是純粹的呼叫傳統函式的話，無論放在什麼位置，這個 this 都會指向全域，而 map() 方法裡的函式，是 map() 方法內的回調函數，他是一個獨立函數，不是被當作物件的方法調用，這個時候這個獨立函數裡面的 this 就會指向 window 了。*/
        - 改變指向該物件的情況
         - 2.1 間接呼叫：把物件中的方法參考到另一個新變數(call  reference)，當呼叫這個新變數時就會退回到「this 指向全域」的模式。
        function hunter() {
        console.log(this.name)
        }

        var name = '奇犽'

        var obj1 = {
            name: '揍敵客奇犽',
            hunter:hunter
        }

        var obj2 = {
            name: '獵人奇犽',
            hunter:hunter
        }

        var hunter_killua = obj1.hunter
        hunter_killua()//奇犽
        -----------------------------------------------------------
        - 2.2 callback
        function hunter() {
        console.log(this.name)
        }

        var name = '奇犽'

        var obj1 = {
            name: '揍敵客奇犽',
            hunter:hunter
        }

        var obj2 = {
            name: '獵人奇犽',
            hunter:hunter
        }

        function callKillua(x){
            x()
        }
        callKillua(obj1.hunter);//奇犽
         /*
        callKillua(obj1.hunter) 呼叫了 callKillua 函數，並將 obj1.hunter 函數引用作為參數傳遞。
        在 callKillua 函數內部，傳遞進來的函數 x 即為 obj1.hunter。
        x() 在這裡相當於 obj1.hunter()，即調用 obj1 物件內的 hunter 函數。
        由於函數 hunter 內部的 this 關鍵字是在調用時確定的，而在這裡，obj1.hunter 函數是在全局上下文中被調用的，所以 this 指向全局物件。
        全局物件具有一個全局變數 name，其值為 '奇犽'。
        因此，this.name 將訪問全局變數 name 的值，即 '奇犽'。
        所以callKillua(obj1.hunter); 的輸出會是 '奇犽'。
        */
```
       

```javascript
    3.this 會綁定在使用 new 關鍵字所建立的實體物件

    function hunter(name) {
        this.name = name
    }
    var name = '奇犽'

    var killua = new hunter('揍敵客奇犽')
    console.log(killua.name);   // 揍敵客奇犽
```

c. `this` 在箭頭函數和傳統函數中有什麼不同？
   - 傳統函式：this 會依照呼叫的方法而定，並非宣告的時機
   - 箭頭函數：this 會綁定到其定義時所在的物件

d. 請給出一個例子展示箭頭函數和傳統函數中 `this` 的差異。

   - 物件中的方法呼叫 this：this 綁定到 hunter 物件
   ```javascript
   const hunter = {
       name: '奇犽',
       family: ['揍敵客'],
       hunterfn: function() {
           let killua = this; // 需另外宣告一個變數賦與 this 的值
           this.family.map(function(item) {
               console.log(`${killua.name}是${item}家族`);
           })
       }
   }
   hunter.hunterfn(); // 奇犽是揍敵客家族
   ```
   ```javascript
    箭頭函式的 this 值會繼承他的父作用域，跟傳統函式「根據呼叫的方式而定」不同，箭頭函式是在定義時就被指定了，以後也不會隨著呼叫方法改變
    const hunter2 = {
        name: '奇犽',
        family: ['揍敵客'],
        hunterfn: function() {
            this.family.map(item => {
                console.log(this);//{name: '奇犽', family: Array(1), hunterfn: ƒ}
                console.log(`${this.name}是${item}家族`);
            })
        }
    }
    hunter2.hunterfn(); // 奇犽是揍敵客家族
   ```
