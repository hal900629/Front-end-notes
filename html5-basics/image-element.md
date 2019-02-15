img元素定义及使用说明:

- `<img>` 标签定义 HTML 页面中的图像。
- `<img>` 标签有两个必需的属性：src 和 alt。

> **值得注意的是:**
> 
> - 从技术上讲，图像并不会插入 HTML 页面中，而是链接到 HTML 页面上。`<img>` 标签的作用是为被引用的图像创建占位符。
> - 通过在 `<a>` 标签中嵌套 `<img>` 标签，给图像添加到另一个文档的链接。

img元素的属性列表:

| 属性名 | 值 | 描述 |
| --- | --- | --- |
| align | top\bottom\middle\left\right | HTML5 不支持。HTML 4.01 已废弃。 规定如何根据周围的文本来排列图像。|
| alt | text | 规定图像的替代文本。|
| height | pixels | 规定图像的高度。|
| src | URL | 规定显示图像的 URL。|
| width | pixels | 规定图像的宽度。|

```html
<!DOCTYPE html>