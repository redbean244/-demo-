# 感想
很简单的一个项目。我原来是用按钮一个一个实现改变的。看了源代码后发现可以用数组，减少代码行数。
# 新知识

## cssText的用法以及特点

#### cssText 本质是什么？
cssText 的本质就是设置 HTML 元素的 style 属性值。
#### cssText 怎么用？
`document.getElementById("d1").style.cssText = "color:red; font-size:13px;";`
#### cssText 返回值是什么？

在某些浏览器中（比如 Chrome），你给他赋什么值，它就返回什么值。
```
    var oBox = document.getElementsByClassName("box")[0];
    console.log(oBox.style.cssText);//""
    oBox.style.height = "200px";
    console.log(oBox.style.cssText);//"height: 200px;"
```
在 IE 中则比较痛苦，它会格式化输出、会把属性大写、会改变属性顺序、会去掉最后一个分号，比如：
```
document.getElementById("d1").style.cssText = "color:red; font-size:13px;";
alert(document.getElementById("d1").style.cssText);
```
在 IE 中值为：FONT-SIZE: 13px; COLOR: red
#### cssText的使用优势

一般情况下我们用js设置元素对象的样式会使用这样的形式：

var element= document.getElementById(“id”);
element.style.width=”20px”;
element.style.height=”20px”;
element.style.border=”solid 1px red”;

样式一多，代码就很多；而且通过JS来覆写对象的样式是比较典型的一种销毁原样式并重建的过程，这种销毁和重建，都会增加浏览器的开销。

js中有一个cssText的方法：

语法为：

obj.style.cssText=”样式”;

element.style.cssText=”width:20px;height:20px;border:solid 1px red;”;

这样就可以尽量避免页面reflow，提高页面性能。

但是，这样会有一个问题，会把原有的cssText清掉，比如原来的style中有’display:none;’，那么执行完上面的JS后，display就被删掉了。
为了解决这个问题，可以采用cssText累加的方法：

Element.style.cssText += ‘width:100px;height:100px;top:100px;left:100px;’

因此，上面cssText累加的方法在IE中是无效的。

最后，可以在前面添加一个分号来解决这个问题：

Element.style.cssText += ‘;width:100px;height:100px;top:100px;left:100px;’

再进一步，如果前面有样式表文件写着 div { text-decoration:underline; }，这个会被覆盖吗？不会！因为它不是直接作用于 HTML 元素的 style 属性。


## this.index == oBtn.length - 1 && (oBox.style.cssText = "");
这句等同于 
```
if (this.index == oBtn.length - 1) {
    oBox.style.cssText = "";
}
```
 &&语句前半句若为假，后半句不会执行。