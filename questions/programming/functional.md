

### 范畴论(category)

+ 范畴：输入，输出及映射关系(物件和态射)

+ 函数的合成：如果一个值要经过多个函数，才能变成另外一个值，就可以把所有中间步骤合并成一个函数，这叫做"函数的合成"（compose）。

  ![compose](../resource/compose.png)

  + compose是可结合的：
    $$
    h∘(g∘f) = (h∘g)∘f = h∘g∘f
    $$

  

+ 函子（functor）：

  + 输入输出是范畴的范畴，高阶范畴
  + mappable，具有map方法的对象，都可以认为是函子，比如 "给定map参数的数组对象”。

### higher-order function

+ 至少符合一个以下条件：
  + 接受一个或多个函数作为输入
  + 输出一个函数



### 纯函数

+ 相同输入一定有相同的输出

+ 整个过程没有副作用（指对外部产生了可观察到的变化）

  

### partial function & total function

- partial function 是给定一个输入不一定有输出的函数
- total function 是给定输入一定有输出的函数
- currying后的函数就是partial function

### 	currying:

- 是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术

- 具有：延迟计算、参数复用、动态生成函数的作用

  ```js
  function currying (fn){
      const params = [];
      const fnTmp = function (param){
          params.push(param);
          return fnTmp;
      }
      fnTmp.valueOf = function(){
          return fn(...params);
      }
      return fnTmp;
  }
  ```

  

### point-free:

+ 不使用所要处理的值，只合成运算过程
+ 无参函数，用于生成新的函数



### Monoid

?



#### 函子

1. 函子

   ```js
   class Functor {
     constructor(val) { 
       this.val = val; 
     }
   
     map(f) {
       return new Functor(f(this.val));
     }
   }
   ```

   

2. Either 函子 ( 优先使用右值 )

```js
class Either extends Functor {
  constructor(left, right) {
    this.left = left;
    this.right = right;
  }

  map(f) {
    return this.right ? 
      Either.of(this.left, f(this.right)) :
      Either.of(f(this.left), this.right);
  }
}	
```



3. 





### immutable

1. - 优点：
     - 节省内存空间（结构共享，immutable库只会修改变化的节点和其父节点，可以理解为只重新创建出现变化的部分）
     - Undo/Redo，Copy/Paste 
     - 拥抱函数式编程
     - 线程安全
     - 数据比较的效率
   - 缺点：
     - 学习成本，额外引入资源
     - 容易和原生对象混淆
     - 扩散性（用就得全用）