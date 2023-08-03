1、示例1：

UI 界面描述：

```text
水平两列布局
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "left": "左边文案",
  "right": "右边文案"
}
```

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "height": "auto",
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "width": "auto",
        "height": "auto",
        "flexGrow": "1",
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.left}"
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "width": "auto",
        "height": "auto",
        "flexGrow": "1",
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.right}"
        }
      ]
    }
  ]
}
```

2、示例2

UI 界面描述：

```text
水平三列布局
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "left": "左边文案",
  "center": "中间文案",
  "right": "右边文案"
}
```

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "flexGrow": "1",
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.left}"
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexGrow": "1",
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.center}"
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexGrow": "1",
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.right}"
        }
      ]
    }
  ]
}
```

3、示例3

UI 界面描述：

```text
水平循环五列
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "list": [
    {"text": "列1"},
    {"text": "列2"},
    {"text": "列3"},
    {"text": "列4"},
    {"text": "列5"}
  ]
}
```

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "flexGrow": "1",
      },
      "condition": {
          "mfor": {
              "list": "${data.list}",
              "item": "item",
              "index": "i"
          }
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${item.text}"
        }
      ]
    }
  ]
}
```

4、示例4

UI 界面描述：

```text
垂直循环五行
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "list": [
    {"text": "行1"},
    {"text": "行2"},
    {"text": "行3"},
    {"text": "行4"},
    {"text": "行5"}
  ]
}
```

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "flexDirection": "column",
  },
  "children": [
    {
      "type": "flex",
      "style": {
          "width": "100%",
      },
      "condition": {
          "mfor": {
              "list": "${data.list}",
              "item": "item",
              "index": "i"
          }
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${item.text}"
        }
      ]
    }
  ]
}
```

5、示例5

UI 界面描述：

```text
整个界面水平排列，左边是垂直水平居中文字，中间是垂直排列并且水平居中的5行文本，右边是垂直水平居中的文字
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "left": "左边文字",
  "centerList": [
    {
      "text": "行1"
    },
    {
      "text": "行2"
    },
    {
      "text": "行3"
    },
    {
      "text": "行4"
    },
    {
      "text": "行5"
    }
  ],
  "right": "右边文字"
}
```

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "height": "auto",
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "width": "100",
        "height": "100%",
        "flexDirection": "column",
        "alignItems": "center",
        "justifyContent": "center"
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.left}",
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "column",
        "flexGrow": "1",
      },
      "children": [
        {
          "type": "flex",
          "style": {
            "width": "100%",
            "height": "auto",
            "flexDirection": "row",
            "justifyContent": "center",
          },
          "condition": {
            "mfor": {
              "list": "${data.centerList}",
              "item": "item",
              "index": "i"
            }
          },
          "children": [
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A",
              },
              "text": "${item.text}"
            }
          ]
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "width": "100",
        "height": "100%",
        "flexDirection": "column",
        "alignItems": "center",
        "justifyContent": "center",
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.right}"
        }
      ]
    }
  ]
}
```

6、示例6

UI 界面描述：

```text
整个界面垂直排列，上面是垂直水平居中文字，中间是水平排列并且垂直居中的5行文本，下面是垂直水平居中的文字
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "top": "上面文字",
  "centerList": [
    {
      "text": "列1"
    },
    {
      "text": "列2"
    },
    {
      "text": "列3"
    },
    {
      "text": "列4"
    },
    {
      "text": "列5"
    }
  ],
  "bottom": "下面文字"
}
```

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "height": "auto",
    "flexDirection": "column",
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "height": "100",
        "flexDirection": "column",
        "alignItems": "center",
        "justifyContent": "center"
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.top}",
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "flexDirection": "row",
      },
      "children": [
        {
          "type": "flex",
          "style": {
            "height": "30",
            "flexDirection": "row",
            "alignItems": "center",
            "flexGrow": "1",
          },
          "condition": {
            "mfor": {
              "list": "${data.centerList}",
              "item": "item",
              "index": "i"
            }
          },
          "children": [
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A",
              },
              "text": "${item.text}"
            }
          ]
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "height": "100",
        "flexDirection": "column",
        "alignItems": "center",
        "justifyContent": "center",
      },
      "children": [
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#11141A",
          },
          "text": "${data.bottom}"
        }
      ]
    }
  ]
}
```
