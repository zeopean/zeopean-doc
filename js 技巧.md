
####  1.比较数组
一般情况下，js 数组是无法进行比较的，但是 可以进行 String 后进行比较

```
#解决方法一：

先排序，再利用toString方法，比较。例如：

    var a = [1,2,3];
    var b = [1,2,3];
    console.log(a.sort().toString() == b.sort().toString());


#解决方法二：


直接toString() 比较也是可以的。

    console.log(_checkedArr.toString() == checkedArr.toString());

```

#### 2.数组删除元素

```
    //删除数组元素
    Array.prototype.remove = function(val) {
        var index = this.indexOf(val);
        if (index > -1) {
            this.splice(index, 1);
        }
    };
    //var arr = new Array(); ...  arr.remove('..');

```