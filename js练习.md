1.99乘法表

```html
<script>
        for (var i = 1; i <= 9; i++) {
            for (var j = 1; j <= i; j++) {
                document.write(j + "*" + i + "=" + i * j + "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;")
            }
            document.write("<br/>");
        }
    </script>
```

2.  求任意个数的最大值

   ```html
   <script>
   function maxEvery() {
               var max = 0;
               //遍历所有的实参，一个个的和max进行比较，如果比max大，则覆盖max的值，遍历完成之后，max的值就是整个实参最大的值
               for (var i = 0; i < arguments.length; i++) {
                   if (max < arguments[i]) {
                       max = arguments[i];
                   }
               }
               return max;
           }
           var re = maxEvery(3, 5, 6, 4, 8, 6, 9, 3, 4);
           console.log(re);
   </script>
   ```

3. 打印出3-100之间所有的质数    遍历拿到3-100的值，用来判断 

   

   ```html
   <script>
   /*  outer:
                for (var i = 3; i <= 100; i++) {
                    //外边的for循环拿到的值 进行依次判断
                    inner: for (var j = 2; j < i; j++) {
                        if (i % j === 0) {
                            //只要当前的i有出现整除为0的，说明当前的i不是质数
                            continue outer;
                        }
                    }             
                    console.log(i);
   
            } */
   </script>
   ```

   

   ```html
   <script>  
   /* for (var i = 3; i <= 100; i++) {
           //每次拿到一个值，就认为他是一个质数
           var flag = true;
           //外边的for循环拿到的值 进行依次判断
           for (var j = 2; j < i; j++) {
               if (i % j === 0) {
                   //只要当前的i有出现整除为0的，说明当前的i不是质数，把开关关闭
                   flag = false;
               }
           }
   </script>
   ```

   

4.  任意进制转换

   ```html
   <script>
   function to2b(num, p) {
               //定义一个空数组 用来保存每次计算的余数
               var arr = [];
               //声明一个变量，用来保存单次计算的余数
               var r = null;
               var str = ""; //用字符串表示最后的值
               var base = "0123456789abcdefghijklmnopqrstuvwxyz";
               while (num > 0) {
                   //把num对2取余
                   r = num % p;
                   //把r用arr进行保存
                   arr.push(r);
                   //对得到值取整数
                   num = parseInt(num / p);
               }
   
               console.log(arr);
               while (arr.length > 0) {
                   //得到arr.pop不要直接赋值，而是获取arr.pop的这个值对应的数字或字母
                   //所以可以认为arr.pop()得到的是base的下标
                   str += base[arr.pop()];
               }
               console.log(str);
   
               return str;
           }
   
           var re = to2b(10000, 36);
   </script>
   ```

5.猴子找大王游戏

​    

```html
<script>
//有一群猴子排成一圈,按1、2、3、…、n依次编号，然后从第1只开始数,数到第m只,则把它踢出圈,然后从它后面再开始数,当再次数到第m只,继/续把它踢出去,以此类推,直到只剩下一只猴子为止,那只猴子就叫作大王。要求编程模拟此过程,输入m和n，输出最后那个大王的编号

 //n表示猴子个数，m表示踢出位置
 
 
 
        function findMonkeyKing(n, m) {
            //因为猴子都是有编号的，所以先把所有的猴子放在一个数组中
            //遍历n次 得到一个新数组
            var arr = [];
            for (var i = 1; i <= n; i++) {
                arr.push(i);
            }

            //只要arr的长度大于1，则还要进行踢猴子
            while (arr.length > 1) {
                // 遍历数组， 如果通过的猴子 就把这个猴子放在数组的末端，如果刚好到第m次 则不再移动这个值，而是把这个值删除
                for (var i = 0; i < m - 1; i++) {
                    //把数组的第一个值放在数组的末端
                    arr.push(arr.shift());
                }
                //到底第m个猴子的时候，把这个猴子删除掉
                arr.shift();
            }

            return arr[0];
        }
        var re = findMonkeyKing(100, 8);
        console.log(re);
                                     </script>
```

6.数组去重

```html
<script>
/* 
            数组去重方法1：
                for for嵌套
        
        */
        /* var arr = [1, 3, 1, 2, 3, 4, 3, 6, 5, 4, 6];
        //遍历数组，得到每一个值 然后开始比较
        for (var i = 0; i < arr.length; i++) {
            //每次拿到一个值 都是从i+1开始比较的
            for (var j = i + 1; j < arr.length; j++) {
                //开始比较 看后边数组中哪一个值和当前拿到的值相等，如果相等则删除
                if (arr[i] === arr[j]) {
                    arr.splice(j, 1);
                    //只要删除有元素，则数组的下标会向前移动以为 所以遍历的j需要减1
                    j--;
                }
            }
        }

        console.log(arr); */


        /* 
            数组去重方法2：
                创建一个新数组，把值依次添加到新数组中，如果新数组已经存在，则忽略不再添加
                indexOf
        
        */
        /* var arr = [1, 3, 1, 2, 3, 4, 3, 6, 5, 4, 6];
        var newArr = [];
        arr.forEach(function (item, index) {
            //判断新数组中有没有item
            if (newArr.indexOf(item) === -1) {
                newArr.push(item);
            }
        });
        console.log(newArr); */



        /* 
            方法三：
                检测每一个值的第一次出现的位置 是不是当前值的下标，如果是则第一次出现，否则已经出现过了   
        
        */
        /* var arr = [1, 3, 1, 2, 3, 4, 3, 6, 5, 1, 4, 6];
        var newArr = [];
        arr.forEach(function (item, index) {
            //判断新数组中有没有item
            if (arr.indexOf(item) === index) {
                newArr.push(item);
            }
        });
        console.log(newArr);
 */


        /* var arr = [1, 3, 1, 2, 3, 4, 3, 6, 5, 1, 4, 6];
        var newArr = arr.filter(function (item, index) {
            return arr.indexOf(item) === index;
        })
        console.log(newArr); */
</script>
```

7.冒泡排序

```html
<script>
var arr = [3, 5, 1, 4, 2, 6, 8, 5, 9, 4];

        //因为冒泡排序每次只能找到一个最大值，所以要找很多次，所以要for循环遍历得到次数
        for (var i = 0; i < arr.length; i++) {
            //每次开始找最大值
            for (var j = 0; j < arr.length - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    //交换两个位置
                    var temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
</script>
```

8.快排

```html
<script>
var arr = [3, 1, 5, 4, 7, 6, 9, 8, 9, 6, 5];

        function quickSort(arr) {
            //当数组的长度为1的时候，则直接返回该数组，不需要排序
            if (arr.length <= 1) {
                return arr;
            }
            //选出一个基准值
            var center = arr.pop();
            //设置一个左边的空数组和右边的空数组
            var left = [];
            var right = [];

            //遍历数组 把数组的值一个个对基准值进行判断，
            //如果是升序：把小于基准值的放在left中 大于放在右边right中
            arr.forEach(function (item, index) {
                if (item >= center) {
                    right.push(item);
                } else {
                    left.push(item);
                }
            });
            console.log(left, center, right);
            //合并
            var newArr = quickSort(left).concat(center, quickSort(right));
            return newArr;
        }

        var re = quickSort(arr);
        console.log(re)
                </script>
```

9.手撸call

```html
<script>
/* 
            1.判断context
            2.给context扩展一个方法ff
            3.调用context.ff
            4.删除ff方法
            5.获取实参 在调用ff的时候 传入
            6.把ff这个名字换了
        
        
        */
        /* 
            手写call:
                - call是每一个函数都有的
                - call可以改变函数的this指向
                - call可以调用函数
                - 函数执行的时候 call可以给函数传参
        
        */

        Function.prototype.myCall = function (context) {
            //根据call的特征判断context的类型
            //如果context是null或者undefined 则context应该为window
            if (context === null || context === undefined) {
                context = window;
            }
            //如果context是基本包装类型，则context应该是当前类型的基本包装对象
            if (typeof context != "object" && typeof context != "function") {
                context = Object(context);
            }
            //如果context是对象类型，则不对context进行修改

            //拿到用户调用myCall时 为fn传入的参数  arguments代表实参
            console.log(arguments);
            //截取arguments的第二位以后的值 用数组保存
            // console.log(Array.prototype.slice.call(arguments, 1))
            var arg = Array.from(arguments).slice(1);
            console.log(arg);


            //此时this指向调用myCall的函数fn（姑且认为fn就是调用myCall的函数）
            //目标：调用fn 并且把fn的this指向context
            //给context扩展一个方法 赋值为fn  如果context调用了fn，则fn的this就会指向context
            // context.ff = this;
            //优化，希望给context扩展一个唯一的不重名的方法名
            //可以把时间戳转为36进制的值，作为属性key，可以不重名
            var key = Date.now().toString(36);
            context[key] = this;

            //如果context调用了ff方法，则说明：fn调用了，fn的this指向了context
            // context.ff();
            // eval("context.ff(" + arg.toString() + ")");
            eval("context[key](" + arg.toString() + ")");
            //因为为了实现逻辑，给context扩展了一个方法，因为这个方法在后来不需要了，所以可以把这个方法删除
            // delete context.ff;
            delete context[key];

        }

        function fn(a, b) {
            console.log(a, b);
            console.log(this, a + b);
        }
        
        fn.myCall(1, 1, 2);
        fn.myCall("abc", 1, 2);
        fn.myCall(true, 1, 2);
        fn.myCall([1, 2], 1, 2);
        fn.myCall({
            name: "laowang"
        }, 1, 2);



        /* 
            理解：  让ff的this指向o
        
        */
        function ff() {
            console.log(this);
        }
        var o = {};
        //给o扩展一个方法 赋值为ff 则ff的this就指向o了
        o.f = ff;
        o.f();



        /* 
            参数用数组保存 怎么传参
        */
        /* var arr = [1, 2, 3]; //'1,2,3'

        function fn(a, b, c) {
            console.log(a + b + c)
        }
        // eval("fn(" + "1,2,3" + ")")
        eval("fn(" + arr.toString() + ")") */
</script>
```



10.手写apply

```html
<script>
Function.prototype.myApply = function (context) {
            //判断context的类型 并改变context类型
            if (context === null || context === undefined) {
                context = window;
            }
            if (typeof context !== 'object' && typeof context !== 'function') {
                context = Object(context);
            }

            //获取用户给函数fn的传参
            var arg = arguments[1];

            //把调用myApply方法的fn函数 的this指向context  并且调用 fn

            //把fn当做是context对象的一个方法
            var key = Date.now().toString(36);
            context[key] = this;

            eval("context[key](" + arg.toString() + ")");

            delete context[key];


        }

        function fn(a, b) {
            console.log(this, a + b);
        }

        fn.myApply(1, [1, 2]);
        fn.myApply('1', [1, 2]);
        fn.myApply(true, [1, 2]);
        fn.myApply(null, [1, 2]);
        fn.myApply(undefined, [1, 2]);
        fn.myApply({
            name: "laowang"
        }, [1, 2]);
        fn.myApply(["a", "b"], [1, 2]);
</script>
```

11.手写bind

```html
<script>
/* 
            bind作用：
                1.改变了函数的上下文对象
                2.返回一个改变上下文对象指向的一个函数

                //换一种思考方法
                bind返回了一个函数，当我调用这个函数的时候，把函数的this指向改变为bind的第一个参数


        */

        Function.prototype.myBind = function (context) {
            //这个位置的this 代表的是调用bind的函数fn
            var _this = this;
            //获取用户给fn的参数
            var arg = Array.from(arguments).slice(1);
            return function () {
                //bind直接返回一个函数
                //当这个函数执行的时候，再获取调用bind的函数fn，然后调用fn 并改变fn的this指向、
                _this.apply(context, arg);
            }
        }

        function fn(a, b) {
            console.log(this, a + b);
        }

        var re = fn.myBind(1, 1, 2)
        re();
        var re = fn.myBind("1", 1, 2)
        re();
        var re = fn.myBind([1, 2], 1, 2)
        re();
        var re = fn.myBind({}, 1, 2)
        re();
        var re = fn.myBind(null, 1, 2)
        re();
</script>
```

12.手写instanceof

```html
<script>
/* 
            手写instanceof：
                myInstanceof(A, B):
                    判断B的原型对象是否在A的原型链上
        
        */

        function myInstanceof(A, B) {
            //先获取B的原型对象
            var _B = B.prototype;
            var _A = A.__proto__;
            while (_A) {
                if (_A === _B) {
                    return true;
                }
                _A = _A.__proto__;
            }

            //当while执行完成还没有返回true，则说明返回false
            return false;

        }


        function Foo() {}
        var f1 = new Foo();
        console.log(myInstanceof(f1, Foo))
        console.log(myInstanceof(f1, Object))
        console.log(myInstanceof(Object, Function))
        console.log(myInstanceof(Object, Object))
        console.log(myInstanceof(Function, Object))
        console.log(myInstanceof(Function, Function))
        console.log(myInstanceof(Object, Foo))
    </script>
```

13.手写new

```html
<script>
/* 
            手写new
                - new做了什么？
                    - 创建了一个对象，并把这个对象返回
                    - 把构造函数的this指向这个创建的对象
                    - 将这个对象的原型链修改，将隐式原型指向构造函数的显式原型
        
        */

        function Person(name, age) {
            this.name = name;
            this.age = age;
            return [];
        }
        Person.prototype.do = function () {
            console.log("do")
        }

        var p1 = new Person("laowang", 18);
        console.log(p1);


        function myNew(constur) {
            //1.创建一个对象
            var obj = {};
            //2.调用构造函数，并把构造函数的this指向当前的对象
            var arg = Array.from(arguments).slice(1);
            //re就是函数调用后的返回值
            var re = constur.apply(obj, arg);
            //3.修改原型链，让obj的隐式原型指向构造函数的显式原型
            obj.__proto__ = constur.prototype;

            //4.返回对象之前，判断构造函数的返回值是基本类型还是对象类型
            //如果是对象类型，则直接返回构造函数的返回值，否则返回obj
            if (typeof re === "object" && re !== null || typeof re === 'function') {
                //如果是object类型 则直接返回re
                return re;
            }

            //如果不符合上边的条件，则返回obj对象
            return obj;
        }

        var p2 = myNew(Person, "xiaowang", 20);
        console.log(p2);

        console.log(p2.do === p1.do); //true
</script>
```

14.深拷贝

```html
<script>
var obj = {
            name: "laowang",
            do: function () {

            },
            score: [10, 20, 30]
        }

        function checkType(o) {
            return Object.prototype.toString.call(o).slice(8, -1).toLowerCase();
        }

        function deepClone(o) {
            //先判断o的类型是什么
            if (checkType(o) === "object") {
                //如果拷贝的是对象，则创建一个新对象
                var newObj = {};
            } else if (checkType(o) === "array") {
                //如果拷贝的是数组，则创建一个新数组
                var newObj = [];
            } else {
                // 如果是其他类型，则可以直接赋值，不需要拷贝
                return o;
            }

            //开始拷贝
            for (var key in o) {
                newObj[key] = deepClone(o[key])
            }

            return newObj;

        }

        var re = deepClone(obj);
        console.log(re);
        console.log(re.score === obj.score);
    </script>
```

15.节流函数

```html
<script>
        var oBox = document.getElementById('box');为
        // 节流函数：在规定的一段时间内只执行第一次
        
        //把包含核心代码的函数提炼出来
        function center(e) {
            console.log(1);
            //因为这个函数是我们的逻辑函数，正常的话 this应该指向绑定事件的对象
            console.log(this);
            //使用event事件对象
            console.log(e);
        }
        oBox.onmousemove = throttle(center, 300);
        oBox.onmousemove({});
        //高阶函数
        function throttle(fn, time) {
            //初始化一个上一次的时间
            var lastTime = 0;
            //return的这个函数才是真正的事件函数
            return function () {
                //每次执行事件的时候，获取当前的时间
                var nowTime = Date.now();
                //看门狗
                if (nowTime - lastTime < time) {
                    return;
                }
                //如果放行，先把当次时间变成上一次的时间
                lastTime = nowTime;

                //放行后就可以执行核心代码
                //因为当前所在函数的this才是指向绑定事件对象oBox的，所以需要让fn的this指向当前的this
                // fn();
                //arguments[0]是当前的事件函数的event对象
                fn.call(this, arguments[0])
            }
        }
    </script>
```

16.防抖函数

```
<script>
        // 防抖函数：在规定时间内只执行最后一次

        var oIpt = document.getElementById('ipt');

        //核心代码
        function center(e) {
            console.log(1);
            console.log(this);
            console.log(e);
        }
        oIpt.oninput = debounce(center, 500);

        //防抖函数
        function debounce(fn, time) {
            //初始化一个定时器
            var timer = null;
            //真正的事件函数
            return function () {
                //每次重新触发事件的时候，把上一次的定时器清除掉，重新设置开始计时
                clearTimeout(timer);

                //保存事件函数的this
                var _this = this;

                //保存事件对象
                var e = arguments[0];
                //设置一个定时器 延迟time事件执行fn
                timer = setTimeout(function () {
                    // fn();
                    fn.call(_this, e);
                }, time);
            }
        }
    </script>
```

