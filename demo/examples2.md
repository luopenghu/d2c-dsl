1、示例1：

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

2、示例2：

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

3、示例3

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