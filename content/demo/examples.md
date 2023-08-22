1、示例1：

UI 界面描述：

```text
水平两列布局，从左到右依次是第一列，第二列
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "first": "这是第一列",
  "second": "这是第二列"
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.first}"
        }
      ]
    },
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.second}"
        }
      ]
    }
  ]
}
```

2、示例2

UI 界面描述：

```text
水平三列布局，从左到右依次是第一列，第二列，第三列
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "first": "这是第一列",
  "second": "这是第二列",
  "third": "这是第三列"
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.first}"
        }
      ]
    },
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.second}"
        }
      ]
    },
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.third}"
        }
      ]
    }
  ]
}
```

3、示例3

UI 界面描述：

```text
水平循环五列，从左到右依次是第一列，第二列，第三列，第四列，第五列
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "list": [
    "这是第一列",
    "这是第二列",
    "这是第三列",
    "这是第四列",
    "这是第五列"
  ]
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
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
          "text": "${item}"
        }
      ]
    }
  ]
}
```
4、示例4：

UI 界面描述：

```text
垂直两行排列，从上到下依次是第一行，第二行
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "first": "这是第一行",
  "second": "这是第二行"
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "column",
  },
  "children": [
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.first}"
        }
      ]
    },
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.second}"
        }
      ]
    }
  ]
}
```

5、示例5

UI 界面描述：

```text
垂直三行排列，从上到下依次是第一行，第二行，第三行
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "first": "这是第一行",
  "second": "这是第二行",
  "third": "这是第三行"
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "column",
  },
  "children": [
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.first}"
        }
      ]
    },
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.second}"
        }
      ]
    },
    {
      "type": "flex",
      "children": [
        {
          "type": "span",
          "text": "${data.third}"
        }
      ]
    }
  ]
}
```

6、示例6

UI 界面描述：

```text
垂直循环五行排列，从左到右依次是第一行，第二行，第三行，第四行，第五行
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "list": [
    "这是第一行",
    "这是第二行",
    "这是第三行",
    "这是第四行",
    "这是第五行"
  ]
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "column",
  },
  "children": [
    {
      "type": "flex",
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
          "text": "${item}"
        }
      ]
    }
  ]
}
```

7、示例7：

UI 界面描述：

```text
整页内容水平排列， 从左到右依次分 3 个模块：
 模块1：垂直排列，共 2 行，从上到下依次是文案1，文案2
 模块2：垂直排列，共 3 行，从上到下依次是文案3，文案4，文案5
 模块3：垂直排列，共 5 行，从上到下依次是文案6，文案7，文案8，文案9，文案10
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "text1": "这是文案1",
  "text2": "这是文案2",
  "text3": "这是文案3",
  "text4": "这是文案4",
  "text5": "这是文案5",
  "rightTexts": [
    "这是文案6",
    "这是文案7",
    "这是文案8",
    "这是文案9",
    "这是文案10",
  ]
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "flexDirection": "column"
      },
      "children": [
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text1}"
            }
          ]
        },
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text2}"
            }
          ]
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "column",
      },
      "children": [
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text3}"
            }
          ]
        },
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text4}"
            }
          ]
        },
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text5}"
            }
          ]
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "column",
      },
      "children": [
        {
          "type": "flex",
          "condition": {
              "mfor": {
                  "list": "${data.rightTexts}",
                  "item": "item",
                  "index": "i"
              }
          },
          "children": [
            {
              "type": "span",
              "text": "${item}"
            }
          ]
        }
      ]
    }
  ]
}
```

8、示例8：

UI 界面描述：

```text
整页内容垂直排列，从上到下依次分 3 个模块：
 模块1：水平排列，共 2 列，从左到右依次是文案1，文案2
 模块2：水平排列，共 3 列，从左到右依次是文案3，文案4，文案5
 模块3：水平排列，共 2 列，从左到右依次是文案6，文案7，文案8，文案9，文案10
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "text1": "这是文案1",
  "text2": "这是文案2",
  "text3": "这是文案3",
  "text4": "这是文案4",
  "text5": "这是文案5",
  "bottomTexts": [
    "这是文案6",
    "这是文案7",
    "这是文案8",
    "这是文案9",
    "这是文案10",
  ]
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "column",
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "flexDirection": "row"
      },
      "children": [
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text1}"
            }
          ]
        },
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text2}"
            }
          ]
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "row",
      },
      "children": [
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text3}"
            }
          ]
        },
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text4}"
            }
          ]
        },
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.text5}"
            }
          ]
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "row",
      },
      "children": [
        {
          "type": "flex",
          "condition": {
              "mfor": {
                  "list": "${data.bottomTexts}",
                  "item": "item",
                  "index": "i"
              }
          },
          "children": [
            {
              "type": "span",
              "text": "${item}"
            }
          ]
        }
      ]
    }
  ]
}
```

9、示例9

UI 界面描述：

```text
左图右文布局： 整体水平排列，左边是一张图片， 右边文字分两行， 上面是标题， 下面是简介
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "img": "https://map-mobile-resource.cdn.bcebos.com/icon/service/feedback-center/default/red-packet-a1.png",
  "title": "这是标题",
  "intro": "这是简介"
}
```

```json
{
  "type": "flex",
  "style": {
    "flexDirection": "row",
  },
  "children": [
    {
      "type": "img",
      "style": {
        "src": "${data.img}",
      }
    },
    {
      "type": "flex",
      "style": {
        "flexDirection": "column",
      },
      "children": [
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.title}"
            }
          ]
        },
        {
          "type": "flex",
          "children": [
            {
              "type": "span",
              "text": "${data.intro}"
            }
          ]
        }
      ]
    }
  ]
}
```