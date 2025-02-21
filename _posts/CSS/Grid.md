CSS Grid 布局是一种强大的布局工具，可以让你轻松创建复杂的响应式布局。以下是一些常见的 CSS Grid 设置和示例，帮助你理解和使用 Grid 布局。

### 基本概念

1. **容器（Container）**：使用 `display: grid` 将一个元素定义为 Grid 容器。
2. **项目（Items）**：Grid 容器中的子元素称为 Grid 项目。
3. **行（Rows）**：垂直方向上的网格线。
4. **列（Columns）**：水平方向上的网格线。
5. **单元格（Cells）**：行和列交叉形成的区域。
6. **轨道（Tracks）**：行或列之间的空间。
7. **区域（Areas）**：多个单元格组成的矩形区域。

### 基本语法

#### 定义 Grid 容器

```css
.container {
  display: grid;
}
```

#### 定义行和列

```css
.container {
  display: grid;
  grid-template-columns: 100px 200px 150px; /* 定义三列 */
  grid-template-rows: 50px 100px; /* 定义两行 */
}
```

#### 使用 `repeat` 函数

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 100px); /* 重复三列，每列 100px */
  grid-template-rows: repeat(2, 50px); /* 重复两行，每行 50px */
}
```

#### 使用 `fr` 单位

`fr` 单位表示分数单位，用于分配可用空间。

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr; /* 第二列占两倍空间 */
  grid-template-rows: 1fr 1fr; /* 两行等分空间 */
}
```

#### 自动填充行和列

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr)); /* 自动填充列，最小宽度 100px */
  grid-auto-rows: 50px; /* 自动创建行，每行 50px */
}
```

### 常见属性

1. **`grid-template-columns`** 和 **`grid-template-rows`**：定义列和行的宽度和高度。
2. **`grid-template-areas`**：定义命名区域。
3. **`grid-column-gap`** 和 **`grid-row-gap`**：定义列和行之间的间距。
4. **`justify-items`** 和 **`align-items`**：对齐项目。
5. **`justify-content`** 和 **`align-content`**：对齐轨道。
6. **`grid-column`** 和 **`grid-row`**：定位项目。
7. **`grid-area`**：定义项目的区域。

### 示例

#### 基本网格布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Basic Grid Layout</title>
  <style>
    .container {
      display: grid;
      grid-template-columns: 1fr 2fr 1fr;
      grid-template-rows: 100px 100px;
      gap: 10px;
      padding: 10px;
    }

    .item {
      background-color: lightblue;
      padding: 20px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
  </div>
</body>
</html>
```

#### 命名区域

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Named Areas Grid Layout</title>
  <style>
    .container {
      display: grid;
      grid-template-columns: 1fr 2fr 1fr;
      grid-template-rows: 100px 100px 100px;
      grid-template-areas:
        "header header header"
        "nav main main"
        "footer footer footer";
      gap: 10px;
      padding: 10px;
    }

    .header {
      grid-area: header;
      background-color: lightcoral;
    }

    .nav {
      grid-area: nav;
      background-color: lightgreen;
    }

    .main {
      grid-area: main;
      background-color: lightblue;
    }

    .footer {
      grid-area: footer;
      background-color: lightyellow;
    }

    .item {
      padding: 20px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header item">Header</div>
    <div class="nav item">Nav</div>
    <div class="main item">Main</div>
    <div class="footer item">Footer</div>
  </div>
</body>
</html>
```

#### 响应式网格布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Grid Layout</title>
  <style>
    .container {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
      gap: 10px;
      padding: 10px;
    }

    .item {
      background-color: lightblue;
      padding: 20px;
      text-align: center;
    }

    @media (max-width: 600px) {
      .container {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
  </div>
</body>
</html>
```

### 总结

通过以上示例和解释，你应该能够理解如何使用 CSS Grid 布局来创建各种复杂的响应式布局。CSS Grid 提供了丰富的功能和灵活的布局选项，可以帮助你轻松实现多样的设计需求。希望这些信息对你有帮助！如果你有任何其他问题或需要进一步的帮助，请告诉我。