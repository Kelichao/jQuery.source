# jQuery源码解读笔记

[jQuery在线文档](http://jquery.cuishifeng.cn/parent.html)

[jQuery源码解读1（架构与依赖模块）issue列表](https://github.com/Kelichao/jQuery/issues)

- [28. 【queue,dequeue】介绍](https://github.com/Kelichao/jQuery-source1/issues/28)
- [27. 【$.deferred】用法详解](https://github.com/Kelichao/jQuery-source1/issues/27)
- [26. 自己写的Deferred的连缀写法精简版](https://github.com/Kelichao/jQuery-source1/issues/26)
- [25. 认识$.Deferred的接口](https://github.com/Kelichao/jQuery-source1/issues/25)
- [24. 异步，以及线性回调 ,Deferred](https://github.com/Kelichao/jQuery-source1/issues/24)
- [23. jQuery的缓存系统（data）,以及其静态方法和实例方法的区别](https://github.com/Kelichao/jQuery-source1/issues/23)
- [22. unique & stopOnFalse](https://github.com/Kelichao/jQuery-source1/issues/22)
- [21. memory的设计](https://github.com/Kelichao/jQuery-source1/issues/21)
- [20. once的设计](https://github.com/Kelichao/jQuery-source1/issues/20)
- [19. 默认回调对象设计](https://github.com/Kelichao/jQuery-source1/issues/19)
- [18. jQuery回调模块结构](https://github.com/Kelichao/jQuery-source1/issues/18)
- [17. jquery回调对象](https://github.com/Kelichao/jQuery-source1/issues/17)
- [16. 模式的实际运用](https://github.com/Kelichao/jQuery-source1/issues/16)
- [15. 理解观察者模式](https://github.com/Kelichao/jQuery-source1/issues/15)
- [14. 1.理解回调函数2.回调的灵活运用](https://github.com/Kelichao/jQuery-source1/issues/14)
- [13. jQuery的each迭代器](https://github.com/Kelichao/jQuery-source1/issues/13)
- [12. 迭代器](https://github.com/Kelichao/jQuery-source1/issues/12)
- [11. 仿栈与队列的操作](https://github.com/Kelichao/jQuery-source1/issues/11)
- [10. 回溯处理的设计 end(), addBack()](https://github.com/Kelichao/jQuery-source1/issues/10)
- [9. 插件接口的设计extend方法](https://github.com/Kelichao/jQuery-source1/issues/9)
- [8. 静态与实例方法共享设计](https://github.com/Kelichao/jQuery-source1/issues/8)
- [7. 对象的构建，分离构造器](https://github.com/Kelichao/jQuery-source1/issues/7)
- [6. jQuery多库共存处理$.noConflict()方法](https://github.com/Kelichao/jQuery-source1/issues/6)
- [5. jQuery中ready与load事件](https://github.com/Kelichao/jQuery-source1/issues/5)
- [4. jQuery的类数组对象结构](https://github.com/Kelichao/jQuery-source1/issues/4)
- [3. 仿jQuery的mouseenter事件](https://github.com/Kelichao/jQuery-source1/issues/3)
- [2. jQuery中的立即表达式](https://github.com/Kelichao/jQuery-source1/issues/2)

-------------------------------------------------------------------------------------------------------------------

# jQuery选择器核心
- 1.层次选择器
<table>
<tr>
<td>匹配单个紧邻在prev元素后面的next元素，效果等同于$("prev").next();</td>
<td>$("prev + next");</td>
</tr>

<tr>
<td>匹配所有prev元素后面的同辈siblings元素，
<br>注意是之后的元素，且不包含该元素本身在内。
效果等同于 $("prev").nextAll("siblings");</td>
<td>$("prev ~ siblings");</td>
</tr>
</table>

- 2.过滤选择器（伪类选择器）

<table>

 <tr><td>选中第一个元素 </td><td>$("select:first") $("select:eq(0)");</td></tr>
 <tr><td>选中最后一个元素 </td><td>$("select:last");</td></tr>
 <tr><td>选中偶数元素 </td><td>$("select:even");</td></tr>
 <tr><td>选中奇数元素 </td><td>$("select:odd");</td></tr>
 <tr><td>选中之后所有 </td><td>$("select:gt(3)");</td></tr>
 <tr><td>选中之前所有 </td><td>$("select:lt(3)");</td></tr>
 <tr><td>选中可见元素 </td><td>$("select:visible");</td></tr>
 <tr><td>选中不可见元素 </td><td>$(select:hidden);</td></tr>
 <tr><td>选中第一个子元素(中间需要有空格) </td><td>$("select :first-child");</td></tr>
 <tr><td>选中最后一个子元素 </td><td>$("select :last-child");</td></tr>
 <tr><td>选中第一个子元素(计数从1开始) </td><td>$("select :nth-child(2)");</td></tr>
 <tr><td>选中不包含one类的元素 </td><td>$("select:not(.one)");</td></tr>
 <tr><td>选中包含one类的元素 </td><td>$("select.one");</td></tr>
 </table>

- 3.内容选择器

<table>
<tr><td>选中文本内容为空的</td><td> $("select:empty");</td></tr>
<tr><td>选中包含特定文本的</td><td> $("select:contains(klc)");</td></tr>
<tr><td>选中不包含特定文本的</td><td> $("select:not(:contains(klc))");</td></tr>
<tr><td>选中子代中含有某个类的节点</td><td> $("select:has(.class)");</td></tr>
<tr><td>选中拥有子元素（包括文本,回车符）的元素</td><td> $("select:parent");</td></tr>
 </table>


- 4.属性选择器

<table>
<tr><td>选中含有title属性的</td><td> $("select[title]");</td></tr>
<tr><td>选中title=text的元素(引号可省略)</td><td> $("select[title=text]");</td></tr>
<tr><td>title值以klc开始</td><td> $("select[title^=klc]");</td></tr>
<tr><td>title值以klc结束</td><td> $("select[title$=klc]");</td></tr>
<tr><td>title值包含klc</td><td> $("select[title*=klc]");</td></tr>
<tr><td>title值不包含klc</td><td> $("select[title!=klc]");</td></tr>
<tr><td>组合属性写法</td><td> $("select[title][bob]");</td></tr>
<tr><td>被选中的input</td><td> $("input:checked");</td></tr>
 </table>
