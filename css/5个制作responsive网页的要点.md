> 笔记[来源]
[TOC]
## 0. 什么是响应式
网页会因应不同设备的屏幕大小，自动调整版面布局、图片及字体大小等，让网页适合在对应的屏幕大小中呈现，提供更好的网页浏览体验。


## 1. Media Query（媒体查询）
通过 Media Query 可设定一个 breakpoint，在设定当符合这个 breakpoint 的时候，CSS 样式的改变。
如：
```css
@media screen and (max-width: 360px) {  /* 一般适用于手机 */
  /* 设备有屏幕且分辨率 <= 360px */
  ul {
    flex-direction: column;
  }
}

@media screen and (min-width: 960px) { /* 一般适用于电脑 */
  /* 设备有屏幕且分辨率 >= 960px */
  ul {
    padding: 0 3rem;
  }

  ui li {
    font-size: 1.2rem;
  }
}
```

至于 breakpoint 的设定，不同的 CSS 框架也有自己的定论。

如：
*1. tailwindcss*
640px | 768px | 1024px | 1280px

*2. Bootstrap*
576px | 768px | 992px | 1200px


## 2. Meta Viewport
```css
<meta name="viewport" content="width=device-width,initial-scale=1">
```
这是一个写在 HTML `<head>` 标签里的 `<meta>` 标签。这个设定告诉手机浏览器，将网页的宽度设定为手机屏幕的宽度，让手机浏览器知道我们网站是支持 Responsive 的。

**这样 Media Query 对于小屏幕宽度的设定才会生效**。


## 3. Resolution
对于现在的手机来说，屏幕的尺寸和解析度时不对等的，例如屏幕尺寸为 320 x 480 实际显示的分辨率为 640 x 960，甚至更高。

我们需要理解的是，在硬件屏幕尺寸不怎么变的情况下，解析度的提升即是显示的密度提升。对应图片的尺寸就需要放大两倍甚至三倍了。


## 4. Image Size
那么在网页中，用多大的图片才足够在高清屏幕中显示呢？最懒的做法就是使用两倍大小的图片。例如将 600px x 600px 的图片，以 300px x 300px 的大小显示。

例如在 iOS APP 中，会被要求提供三个尺寸版本，分别是 `@1x`、`@2x`、`@3x`。iOS 到时候就会因应不同的机型，选择合适的版本去显示，确保显示出来的效果足够清晰。

在网页中也有类似的做法，因为如果不顾屏幕解析度，直接载入一张大图，虽然可以确保出来足够清晰，但可能会浪费一些数据流量。

如下：
```css
/* 套上一层 <picture> 标签 */
<picture>
  /* 加入 <source> 标签，定义 srcset 属性 */
  <source srcset="https://placehold.it/600x600 2x, https://placehold.it/900x900 3x">
  <img src="https://placehold.it/300x300>
</picture>
```

之后就会因应不同的设备显示不同尺寸的图片。

**而无论是哪一个版本，图片都会以 300px x 300px 的大小去显示**。


## 5. Font Size
由于网页要适配不同的屏幕大小，所以字体大小也应该因应屏幕大小而调整，所以建议使用相对的尺寸单位。

最基本的是在 `html` 中设定基础文字大小，这样就可以配合 Media Query，通过调整 `html` 的文字大小，一次性进行更改。

另外，`vw` 和 `vh` 也是挺有趣的用法，文字会因应 viewport 的宽度|高度而按比例缩放。


[ 来源 ]: https://www.bilibili.com/video/BV1i54y1D7cd