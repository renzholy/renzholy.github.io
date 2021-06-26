# 使用 React 后端渲染 SVG 图片

这篇文章教你使用 Figma 作为设计工具，使用 React 作为模版渲染工具，使用 Next.js 作为 SSR，渲染出一个 SVG 图片。

---

最近参与制作了即刻里的一个小功能“我的持仓”。其前端主要分为两部分：一部分是即刻个人主页下的“小卡片”，另一部分是点击小卡片后跳转到的网页。我们主要来讲讲这个小卡片是如何实现的。

![image](https://user-images.githubusercontent.com/8287771/123503395-529dcd80-d685-11eb-8b7d-7ffef0a763ed.jpg)

- 小卡片实际上是一张 SVG 图片，放在整个卡片列表中的一个 `<img />` 标签里
- 为什么不以 SVG DOM 的方式渲染？这样做的话，卡片列表（上图黄框部分）和卡片内容（上图红框部分）代码要放在同一个项目中，“我的持仓”业务逻辑和即刻的业务逻辑就耦合了。
- 为什么不用 PNG 图片？因为图片中含有文字，PNG 图片无法适配不同手机的不同字体。

## Figma 导出 SVG

导出时注意不要勾选 `Outline Text`，该选项会把 text 变成 path，也就是把字体当作矢量图来画。但是在我们的渲染中需要 text 作为变量，因此不要勾选。

![image](https://user-images.githubusercontent.com/8287771/123503165-cfc84300-d683-11eb-9317-baecf48d8515.png)

## React 渲染 SVG

React 本身就支持 SVG 渲染，把刚才导出的 svg 代码复制粘贴成为一个 React Component

```tsx
export const SvgBox = () => (
  <svg
    width="100"
    height="100"
    viewBox="0 0 100 100"
    xmlns="http://www.w3.org/2000/svg"
  >
    ...
  </svg>
);
```

## Next.js SSR

使用 Next.js 的约定式路由，新建一个页面文件，使用 [renderToStaticMarkup](https://reactjs.org/docs/react-dom-server.html#rendertostaticmarkup) 和 [getServerSideProps](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering) 进行服务端渲染。请求这个页面时，返回的是 SVG，而不是 HTML。

```tsx
import type { GetServerSideProps } from "next";
import { renderToStaticMarkup } from "react-dom/server";

export default function SvgPage() {
  return null;
}

export const getServerSideProps: GetServerSideProps = async ({ res }) => {
  res.setHeader("Content-Type", "image/svg+xml");
  res.write(renderToStaticMarkup(<SvgBox />));
  res.end();
  return {
    props: {},
  };
};
```

之后所需要做的事情就是根据业务逻辑给 `<SvgBox />` 组件传入变量，就像写普通 React 组件一样。

## 嵌入图片

值得注意的是，为了在 Android 系统上显示 Apple Emoji，小卡片第二行行首的 emoji 不是字符，而是 PNG 图片。

### base64 encode

在 `<img />` 标签里显示的 svg 不能再请求外部资源，所以我们需要把 PNG base64 encode 后作为 [Data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) 传入 SVG 的 `<image />` 标签中，而不能只传一个 url。

### AVIF 和 WebP

PNG 图片 base64 后体积太大了，因此我为每张 emoji PNG 都准备了对应的 AVIF 和 WebP 版本，根据 `req.headers.accept` 来给 SVG 嵌入不同格式的图片
