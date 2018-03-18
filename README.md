# rem-
主要运用在移动端的应用中，目的是为了自适应屏幕大小

rem是计算匹配
为了方便计算，缩放比例一般为1rem等于100px
说明
1.在html内最外层元素给max-width:640px,min-width:340px;
2.元素都会以rem进行缩放;
3.字体大小一般为0.2rem-0.34rem;
4.引入img标签的时候，img标签必须给float或者给一个属性(vertical-aligin:middle，display:block);否则与父元素有20px的margin-bottom
5.如果img想自适应需要给个宽度，宽度可以是百分比，也可以是rem为单位给固定宽度，比如img实际宽度为100px，因此js想自动缩放可以在该元素css给该img
{width：1rem}，其他元素雷同
6.如果用到input的时候，该元素浮动或者以rem为单位，给固定的宽高，不然占据的行高会很大，出现元素占据的行高大的时候，float一下即可。

(function(doc,win){
  var docE1=doc.documentElement,
      //orientationchange事件是在用户水平或者垂直翻转设备（即方向变化）时触发该事件。
      //resize事件是屏幕缩放时触发事件
      resizeEvt='orientationchange' in window ?  'orientationchange':'resize',
      recalc=function(){
        var clientWidth=docE1.clientWidth;
        if(! clientWidth) return;
        if(clientWidth>=640){
          docE1.style.fontSize='100px';
        }else{
          docE1.style.fontSize=100*(clientWidth/640)+"px";
        }
      };
      if(!doc.addEventlistener) return;
      win.addEventlistener(resizeEvt,recalc,false);
      doc.addEventlistener('DOMcontentloaded',recalc,false);
})

//DOMcontentloaded是在firefox下特有的Event，当所有DOM解析完之后，会触发这个事件
//DOMcontentloaded事件不会等待css文件，图片，iframe加载完成。
它的触发时机是加载页面，解析所有标签（不会等待css和js）并如规范中所说的设置interactive和执行每个静态中的js，然后触发。
而js的执行，需要等待它前面的css加载执行完成，因为js可能会依赖他前面的css计算出来样式。


对rem的看法
1.相对于根节点，让我们整个网站可以统一。
2.让字体更好的适应网站的大小。

问题解决
1.出现字体过大的元素，通常是没有设置font-size。
2.元素的font-size是继承根目录的。
最佳的解决方案
1.在展现文字父级或者本身设置font-size
2.在body设置像素


