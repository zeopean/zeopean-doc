
#### location的匹配流程

当一个nginx配置文件中有多个location时，刚接触Nginx都会错误的认为location是按照配置文件的顺序，由上至下与URI匹配下来，匹配到之后就应用location指令块里面的规则。
实际上，要比这复杂一些。

#### location指令种类

    location指令的匹配方式大致上分为前缀字符串匹配（prefix strings）和正则表达式匹配（regular expression）两种：
    
    1.正则表达式匹配location：location带符号 ~ 或者 ~* 的，表示正则表达式匹配， ~ 区分大小写，~* 不区分大小写；如，location ~ \.(jpe?g|png|gif) {....} 匹配图片格式为jpg、jpeg、png、gif的格式的uri；
    
    2.前缀字符串匹配location：不带符号的location都是，另外带 = 或 ~^ 符号也是，这两个符号比较特殊（下面会说到）。

#### 匹配过程和规则
##### 正常匹配流程
    
    1、nginx会优先匹配前缀location，所有前缀location匹配完之后，会选定一个最长匹配度的location作为候选，与顺序无关（注意：并不确定该location为最终结果），比如：
    location  /statics/  {...A..}
    location  /statics/js/ {...B..}
    
    对于上面的例子，uri  /static/js/jQuery.js会匹配B这个location，如果下面没有正则表达式location在的话，就会选定这个为最终结果；
    
    2、当所有的前缀location匹配完之后，开始按顺序匹配正则表达式location，此时有两种情况：
    
    
    如果匹配到正则表达式location，则马上停止匹配剩下的location，并将这个正则表达式location，覆盖掉原来候选的前缀location，作为最终结果；
    如果没有匹配到任何正则表达式location，则选用之前候选的前缀Location，作为最终结果。

##### 阻止nginx匹配正则表达式location

    我们可以通过在前缀location匹配里添加^~或者=来阻止nginx继续匹配正则表达式location，两者区别在于：
    
    =     必须精确匹配
    ^~   受最长匹配规则影响
    
    另外一种情况就是当前缀location满足精确匹配的情况
