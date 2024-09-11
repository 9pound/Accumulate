# Module



一个模块就是一个独立的文件





## import() 

运行时加载

异步加载，返回promise 对象



## import

编译时加载，或者称为静态加载，用于输入其他模块提供的功能。

import命令输入的变量都是只读的，因为它的本质是输入接口，但如果是一个对象，改写对象的属性是允许的。





```
import {stat,exists,readFile} from 'fs';


```



`import`后面的`from`指定模块文件的位置，可以是相对路径，也可以是绝对路径，`.js`后缀可以省略。如果只是模块名，不带有路径，那么必须有配置文件，告诉 JavaScript 引擎该模块的位置。

模块的整体加载

```
import * as circle from './circle'
```



## export

export命令用于规定模块的对外接口

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。

变量，function，class

export命令可以出现在模块的任何位置，只要处于模块顶层就可以。

```javascript
// 输出变量
// 写法1
export var firstName = '';
export var lastName = '';

// 写法2
var firstName = "";
var lastName = "";

export{firstName,lastName}

// 输出函数
export function multiply(x,y){
    return x*y;
}

function func1(){}
function func2(){}

export{
	func1 as v1,
    func2 as v2
}

// 输出
```

import和export命令只能在模块的顶层