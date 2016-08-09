# testPub  测试文件；

测试rsync

test 2.39----000


## dialog.js的总结
必须要进入的文件（jquery，seajs默认需要引入的）

- < link rel="stylesheet" href="../../wui/reset.css"/>
- < link rel="stylesheet" href="../../wui/dialog/css/dialog.css"/>
- < link rel="stylesheet" href="../../wui/button/css/button.css"/>

创建到时候，有两种消息框；一种是

- var xbox = Dialog.xbox({})  //普通的消息盒子
- var xbox = Dialog.msgBox({}) //meg消息；msgBox: 继承自Xbox;提供了subTitle、cls、msg套数来配置信息提示框要显示的内容;
- var xbox=Dialog.confirmBox({})    //确认框信息

### dialog 属性记录;

- title
- content  内容，如果需要样式修改，在这里直接用div修改，比如<div style="padding:10px;">标题栏可拖动</div>
- buttons: [], //删除确定、取消按钮；如果删除按钮，怎么显示右上角的关闭按钮？
    - buttons: [] //这个时候是不显示按钮；
    - buttons:[{},{},{}] 这种是自定义按钮的；属性有name,cls,url,target,callback,不写cls，默认的是绿色的按钮白色的字；name是必须的；
- modal: true, //设置了遮罩，xbox会自动居中显示;
- opacity number, 遮罩层不透明度设置。默认0.2，值范围是0-1
- drag: true //设置可以拖动;如果标题为false，不显示标题的情况下，是不可移动的;
- second:2,   //2秒后关闭；
- border  //boolean，是否显示默认边框。默认true。仅对xbox和msgBox有效。
- beforeShow
- afterShow
- afterHide
- 自定义显示动画
    - closeEffect:'elastic',
    - openEffect:'elastic',
    - direction:'down',
    - distance:30
- msgBox的设置，提示消息的；
    - title:'默认标题',
    - subTitle:'操作成功',
    - msg:'删除成功，请关闭',
    - afterHide:function(){console.log('默认的msgBox消息')},
- confirmBox里面的设置；var xbox = Dialog.confirmBox({})里面的
    - title:"你确定要删除吗？",// 提示消息；
    - content: '',//默认是空字符串的
    - ok:function(){console.log('ok')};//function, 点击确定按钮回调函数;当回调成功的时候，执行的操作；
    - cancel; function, //点击取消按钮回调函数

### dialog 方法记录，通过xbox调用的；
- xbox.show() 弹窗显示
- hide() 隐藏
- centralize() 居中显示
- destroy() 隐藏组件，并销毁dom
- showCloseButton(true)  显示/隐藏 标题的关闭按钮；
- setPosition(offset) 设置组件的位置。offset参数为对象，包含left和top属性。一般是参照点击的按钮来定位的；
   - var positon=$div1.offset(); //$div1是控制显示的元素
   - xbox.setPosition({left:positon.left,top:positon.top+100});

- setTitle(html) 设置标题，html参数可以是html字符串
- setContent(html) 设置内容，html参数可以是html字符串
    - xbox.setTitle($('#ipt1').val());
    - xbox.setContent($('#ipt2').val()); //#ipt1,#ipt2是用户可以见的input
- setButtons([{},{},{}]) 设置自定义按钮。
    - 属性是和buttons一样的；name,cls,url,target,callback；不写cls，默认的是绿色的按钮白色的字；
- autoClose(5);与second是对应的；
    - xbox.autoClose(5); 里面参数的数字是秒；
    - xbox.autoClose(-1); -1是为禁止自动关闭
- setIndex的方法
    - xbox的初始z-index值是1000, 可以使用setZIndex(index)来全局修改初始值。
    - 当然也可以使用xbox.$_wrapper.style.zIndex来修改单个xbox的z-index值。
    - dialog的z-index会自增；
- follow 显示位置 top|right|bottom|left|horizontal|vertical；其中horizontal和vertical会根据屏幕空间，决定显示位置。和centralize,setPosition有冲突；
    - xbox.follow({
    -       el: $(this),
    -       direction: 'top',//top|right|bottom|left|horizontal|vertical
    -       offsetX: 0,
    -       offsetY: 5,
    -       callback: function (direction) {
    -           console.log(direction);
    -       }
    -   });

- msgBox中的方法【showMsg】；建立的时候var xbox = Dialog.msgBox({})；不要用xbox，用msgBox；必须要引入/wui/reset.css 否则icon图标不出现；
    - xbox.showMsg({})  属性是写在xbox.showMsg({})里面的；
    - cls:'stop', //string, 提示框类型 调用不同的图片;massage | success | error | stop | wait | ask 。默认 massage
    - title:'提示-修改的', //修改的时候，是无效的；
    - subTitle:'是否继续删除-修改的', 提示客户的标题
    - msg:'删除后数据将不能恢复，请确认是否删除',提示客户的消息
    - afterHide:fn;//隐藏后的回调方法
- confirmBox中的方法；
    - var $this=$(this);
    - xbox.follow({
    -     el:$this,//元素是谁；通过$this来把操作的this封装好；
    -     direction:'bottom'//定在的位置；
    - });
    - e.preventDefault();
    - xbox.show();
    - setOk(fn)  //设置确定按钮回调函数;对应的是属性中ok那个函数
    - setCancel(fn) //设置取消按钮回调函数；对象的是属性中caneel的函数；

## paging的总结


