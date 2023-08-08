UI 界面描述：

```text
UI 界面从上到下依次分为以下几个模块：
1. 头部标题，水平排列，左侧是小度头像，中间是标题，右侧是负反馈按钮
2. 行程信息模块， 水平排列依次是：
    a.上车站信息：垂直排列，车辆出发时间在上，上车地点在下
    b.行程信息：垂直排列，车辆类型图片在上，行程花费的时间在下
    c.下车站信息，垂直排列，车辆到达时间在上，下车地点在下
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "title": "你最近的行程安排",
  "info_arr": [
    {
      "text": "11:21",
      "sub_text": "北京南站"
    },
    {
      "text": "30分钟",
      "icon": "https://map-mobile-opnimg.cdn.bcebos.com/b3b456509233ab208feadd2deeffcbaf.png"
    },
    {
      "text": "11:51",
      "sub_text": "天津站"
    }
  ]
}
```

生成的 DSL 描述：

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "height": "144",
    "flexDirection": "column"
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "height": "64",
        "padding": "4 0 0 4",
        "flexDirection": "row"
      },
      "children": [
        {
          "type": "flex",
          "style": {
            "width": "100%",
            "height": "60",
            "flexDirection": "row",
            "alignItems": "center",
            "flexGrow": "1",
            "flexShrink": "1"
          },
          "children": [
            {
              "type": "img",
              "style": {
                "width": "20",
                "height": "20",
                "src": "https://map-mobile-resource.cdn.bcebos.com/icon/service/feedback-center/default/page-bounty-person.png"
              }
            },
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A"
              },
              "text": "${data.title}"
            }
          ]
        },
        {
          "type": "flex",
          "style": {
            "width": "30",
            "height": "60",
            "flexDirection": "column"
          },
          "children": [
            {
              "type": "img",
              "style": {
                "width": "12",
                "height": "12",
                "src": "https://map-mobile-opnimg.cdn.bcebos.com/80d1e3ba1fdaaddfc95a44acdfc8f24a.png",
                "alignSelf": "center"
              }
            }
          ]
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "height": "auto",
        "padding": "0 10 0 10",
        "margin": "10 0 0 0",
        "flexDirection": "row"
      },
      "children": [
        {
          "type": "flex",
          "style": {
            "width": "auto",
            "height": "auto",
            "flexDirection": "column",
            "flexGrow": "1"
          },
          "children": [
            {
              "type": "flex",
              "style": {
                "width": "100%",
                "height": "auto",
                "flexDirection": "column",
                "alignItems": "center"
              },
              "children": [
                {
                  "type": "span",
                  "style": {
                    "fontSize": "18",
                    "color": "#11141A"
                  },
                  "text": "${item.text}"
                },
                {
                  "type": "span",
                  "style": {
                    "fontSize": "18",
                    "color": "#11141A"
                  },
                  "text": "${item.sub_text}"
                }
              ],
              "condition": {
                "mif": "${item.sub_text}&&!${item.icon}"
              }
            },
            {
              "type": "flex",
              "style": {
                "width": "100%",
                "height": "auto",
                "flexDirection": "column",
                "alignItems": "center"
              },
              "children": [
                {
                  "type": "img",
                  "style": {
                    "width": "109",
                    "height": "24",
                    "src": "${item.icon}"
                  },
                  "condition": {}
                },
                {
                  "type": "span",
                  "style": {
                    "fontSize": "18",
                    "color": "#11141A"
                  },
                  "text": "${item.text}"
                }
              ],
              "condition": {
                "mif": "!${item.sub_text}&&${item.icon}"
              }
            }
          ],
          "condition": {
            "mfor": {
              "list": "${data.info_arr}",
              "item": "item",
              "index": "index"
            }
          }
        }
      ]
    }
  ]
}
```