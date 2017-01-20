---
layout: post
category: tech
tags: tech
keywords: android 水平进度条
description: 安卓自定义水平进度条
title: android自定义水平进度条
---

android系统自带的ProgressBar很丰富，有转圈的菊花，也有水平进度条，大小，颜色，背景色，进度条颜色都能够设置。

但是仅仅是能够设置，并不是能够很方便的设置。

比如我要在java代码里动态的设置水平进度条的颜色，这时就比较困难了，因为进度条颜色与进度条背景色不同，进度条颜色可以通过xml文件配置出来，但是在java里动态设置颜色就有点麻烦。

适用场景，类似微信轻应用页面头部的进度条。

这时，我们不妨自己撸一个进度条。

先说一下构思：

1、这个进度条名称叫HorizontalProgressBar。

2、继承自android原始的View。

3、通过重写View的onDraw方法，绘制View的颜色。

4、在setProgress方法里设置进度，并更新视图，也就是调用onDraw方法，达到更新进度条的目的。

看代码：

```
public class HorizontalProgressBar extends View {

    private int progress;
    private int color;

    public HorizontalProgressBar(Context context) {
        super(context);
        init();
    }

    public HorizontalProgressBar(Context context, AttributeSet attrs) {
        super(context, attrs);
        init();
    }

    public HorizontalProgressBar(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        init();
    }
    //默认颜色
    private void init(){
        color = Color.parseColor("#A3BFDD");//灰蓝色
        progress = 0;
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        int screenWidth = Util.getWindowWidth(this.getContext());//屏幕宽度
        int progress = screenWidth*this.progress/100;//100为最大进度
        Paint paint = new Paint();//画笔
        paint.setColor(color);//画笔颜色
        paint.setStyle(Paint.Style.FILL);//实心画笔
        canvas.drawRect(0,0,progress,getHeight(),paint);//以视图高度为高，进度为宽，画矩形
    }
    //获取进度
    public int getProgress() {
        return progress;
    }
    //设置进度，更新画布
    public void setProgress(int progress) {
        this.progress = progress;
        invalidate();
    }

    public int getColor() {
        return color;
    }
    //设置颜色
    public void setColor(int color) {
        this.color = color;
    }
    //设置字符串颜色
    public void setColor(String color){
        this.color = Color.parseColor(color);
    }
}
```

自定义进度条完成。非常简单实用。

当然，模拟原生的进度条也可以用这个思路，原生的进度条有三重颜色：背景色，第二进度条色，进度条色。

我们可以定义三个画笔，分别管理这三种颜色就行。




