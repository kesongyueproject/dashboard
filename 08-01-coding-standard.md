# <center>代码规范</center>

### 1. UI规范

##### 1.1 背景

###### 	1.1.1 颜色

​		整体背景色采用微信的背景色 #EDEDED。

##### 1.2 字体

###### 	1.2.1 颜色

​		主内容Black黑色，次要内容Grey灰色。

###### 	1.2.2 大小

​		微信内字体的使用与所运行的系统字体保持一致，常用字号为20，18，17，16，14，13，11。

##### 1.3 控件

###### 	1.3.1 ListView

​		ListView的各项item的背景色一般为White白色，各Item直接用灰色细线或设置margin使其显露出背景色隔	开。

​		![](/images/listView.png)

###### 	1.3.2 Button

​		Button的样式一般采用微信的内置样式：type="primary"。

​		![](/images/button.png)

---

### 2. wxml规范

##### 2.1 缩进与嵌套

​	保证块元素左对齐；嵌套块之间缩进两个字符；尽量将页面分为上、下两部分或上、中、下三部分这样方便阅览。

<view class='top'>

​    <text class='title'>{{title}}</text>

​    <view class='author' bindtap='getAuthorInfo'>

​      <image class='img' src='{{img_url}}'></image>

​      <view class='author_info'>

​        <text class='publisher'>{{nickname}}</text>

​        <text class='introduction'>{{introduction}}</text>

​      </view>

​    </view>

  </view>

---

### 3. wxss规范

##### 3.1 属性顺序

​	属性顺序基本是按照大小（width、height）、位置（margin、padding）、背景（background）、字体相关（font-size、font-color）、布局方式（display）、其他（border等）排列。

```css
.author_info{
  width: 550rpx;
  height: 100%;
  margin-left: 30rpx;
  display:flex; 
  flex-direction:column;
}
```

---

### 4. js规范

##### 4.1 语言规范

###### 	4.1.1 变量

​		声明变量必须加上var关键字，避免引起冲突，并明确该变量的作用域。

###### 	4.1.2 var that = this;

​		在函数里添加该行代码，方便获取data里的数据。

###### 	4.1.3 var app = getApp();

​		在js文件开头添加该行代码，方便获取全局变量。

##### 4.2 编码风格

###### 	4.2.1 注释

​		在每个函数开头添加注释，注明该函数的功能。如:

```
      //添加新建选择题的选项
      addOption: function () {
        var num = this.data.numOfNewOptions + 1;
        var options = this.data.newOptions;
        options.push({ name: "" });
        this.setData({
          numOfNewOptions: num,
          newOptions: options
        })
      },
```

###### 	4.2.2 数组和对象的初始化

​		短的数组和对象初始化时，如果数据不长，就写在单行上：

```javascript
		data: {
        	singleSelectQuestions: [],
        	multipleSelectQuestions: [],
        	hiddenSelectQuestion: true,
        	questionType: 2,
        	newSelectSubject: "",
        	numOfNewOptions: 2,
        	newOptions: [{ name: "" }, { name: "" }],
        	detailOfQuestion: {}
        },
```

​		对象数据过多过长就每行写一个数据：

```javascript
		data: {
        	title: that.data.detailOfQuestion.title,
        	uid: app.globalData.username,
        	reward: that.data.detailOfQuestion.reward,
        	mtype: "questionnaire",
        	description: that.data.detailOfQuestion.description,
        	imgs_url: that.data.detailOfQuestion.icon,
        	ing: true,
        	people: 0,
        	people_limit: that.data.detailOfQuestion.people_limit,
        	singleSelectQuestions: that.data.singleSelectQuestions,
        	multipleSelectQuestions: that.data.multipleSelectQuestions
      	}
```