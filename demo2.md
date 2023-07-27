UI 界面描述：

```text
UI 界面从上到下依次分为以下几个模块：
1. 顶部是一个居左的标题
2. 两个左右对齐的可以跳转页面的图片链接
3. 应用列表：垂直排列，包括4给可以跳转页面的链接，每个链接中的内容从左到右依次是：
    a、图片
    b、上面是标题，下面是描述内容
    c、申请按钮
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "title": "欢迎来到主页",
  "imageLinks": [
    {
      "imageUrl": "https://example.com/image1.jpg",
      "link": "https://example.com/page1"
    },
    {
      "imageUrl": "https://example.com/image2.jpg",
      "link": "https://example.com/page2"
    }
  ],
  "appList": [
    {
      "imageUrl": "https://example.com/app1.jpg",
      "title": "应用1",
      "description": "这是应用1的描述",
      "applyButtonLink": "https://example.com/apply1"
    },
    {
      "imageUrl": "https://example.com/app2.jpg",
      "title": "应用2",
      "description": "这是应用2的描述",
      "applyButtonLink": "https://example.com/apply2"
    },
    {
      "imageUrl": "https://example.com/app3.jpg",
      "title": "应用3",
      "description": "这是应用3的描述",
      "applyButtonLink": "https://example.com/apply3"
    },
    {
      "imageUrl": "https://example.com/app4.jpg",
      "title": "应用4",
      "description": "这是应用4的描述",
      "applyButtonLink": "https://example.com/apply4"
    }
  ]
}
```

DSL 描述：

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "column",
    "width": "100%",
    "height": "100%"
  },
  "children": [
    {
      "type": "span",
      "style": {
        "fontSize": "24",
        "color": "#000000"
      },
      "text": "${data.title}"
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "row",
        "justifyContent": "space-between",
        "width": "100%"
      },
      "condition": {
        "mfor": {
          "list": "${data.imageLinks}",
          "item": "imageLink",
          "index": "i"
        }
      },
      "children": [
        {
          "type": "img",
          "style": {
            "src": "${imageLink.imageUrl}",
            "width": "100",
            "height": "100"
          }
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "column",
        "width": "100%"
      },
      "condition": {
        "mfor": {
          "list": "${data.appList}",
          "item": "app",
          "index": "i"
        }
      },
      "children": [
        {
          "type": "img",
          "style": {
            "src": "${app.imageUrl}",
            "width": "100",
            "height": "100"
          }
        },
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#000000"
          },
          "text": "${app.title}"
        },
        {
          "type": "span",
          "style": {
            "fontSize": "14",
            "color": "#666666"
          },
          "text": "${app.description}"
        },
        {
          "type": "span",
          "style": {
            "fontSize": "16",
            "color": "#1E90FF"
          },
          "text": "申请"
        }
      ]
    }
  ]
}
```