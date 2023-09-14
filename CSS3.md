#### 浮动

![image-20230810200055380](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810200055380.png)

浮动前

![image-20230810200213390](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810200213390.png)

浮动后

![image-20230810200237311](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810200237311.png)





##### 浮动产生的影响

![image-20230810202347011](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810202347011.png)

原图，123均未浮动

![image-20230810201717564](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810201717564.png)

123设置浮动后

![image-20230810201852324](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810201852324.png)

123**后**加上4方块——浮动对后面的元素有影响

![image-20230810202139406](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810202139406.png)

123**前**加上方块0——浮动对前面的元素没有影响

![image-20230810202210450](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230810202210450.png)

清除浮动产生影响的五种方法

![image-20230811122435379](C:\Users\asus\OneDrive\桌面\笔记\images\image-20230811122435379.png)







#### 布局思路-移动端商城多图标展示

<img src="C:\Users\asus\OneDrive\桌面\笔记\images\image-20230815151855562.png" alt="image-20230815151855562" style="zoom:50%;" />

```css
.cate-lv3-list {//最外层大框子
	display:flex;		//设置内容元素为弹性盒子
    flex-wrap：wrap;		//一行放不下自动换行
    .cate-lv3-item{		//框子内部的各个item项
        width:33.33%;			//每个图片+文字的item都设置为1/3宽，一行能放下3个item
        display:flex;			//同样是弹性布局
        flex-direction:column;	//图片和文字呈现纵向布局
        justify-content:center;	//水平居中
        align-items:center;		//垂直居中
        
        image{
            width:60px;
            height:60px;
        }
        text{
            font-size:12px;
        }
    }
}
```





#### 实现搜索框等组件吸顶效果

<img src="C:\Users\asus\OneDrive\桌面\笔记\images\image-20230816114217964.png" alt="image-20230816114217964" style="zoom:50%;" />

```css
.search-box {
	position: sticky;
	top: 0;	
    z-index: 999;//提高层级，防止被覆盖

}
```





#### 搜索词条的美化

<img src="C:\Users\asus\OneDrive\桌面\笔记\images\image-20230816153012878.png" alt="image-20230816153012878" style="zoom:67%;" />

```css
.goods-name{
    white-space: nowarp;		//文字不允许换行（单行文本）
    overflow: hidden;			//溢出部分隐藏
    text-overflow: ellipsis;	//文本溢出后，使用 ... 代替
    margin-right: 3px
}
```





