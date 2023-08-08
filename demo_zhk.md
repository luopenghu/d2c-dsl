UI 界面描述：

```text
UI 界面从上到下一次分为以下几个模板：
1. 顶部标题，水平排列，左侧是头像 中间是标题，右侧是负反馈按钮
2. 线路信息，左右分布依次是：
  a. 线路信息：垂直排列： 上面是下一站信息，下面是上一站信息
  b. 按钮信息：垂直排列： 上面是按钮图片，下面是按钮描述。
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "robot_title": "您正在乘坐415路，要下车吗",
  "photo": "https://map-mobile-opnimg.cdn.bcebos.com/2587445e224345b3a2746b98722f1956.gif",
  "title": "下一站·<font color='#3377FF'>来广营西桥</font>",
  "sub_title": "上一站·来广营西桥东",
  "icon": "https://map-mobile-resource.cdn.bcebos.com/icon/service/trip-helper/default/Frame%20143%403x-1.png",
  "icon_text": "到站提醒",
  "feedback_icon": "https://map-mobile-opnimg.cdn.bcebos.com/efba43686f5325057f2ee0d29d170bd2.png"
}
```

生成的 DSL 描述：

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "height": "auto",
    "padding": "0 0 10 0",
    "flexDirection": "column"
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "height": "52",
        "padding": "0 0 0 10",
        "flexDirection": "row",
        "alignItems": "center"
      },
      "children": [
        {
          "type": "flex",
          "style": {
            "width": "40",
            "height": "40",
            "flexDirection": "column"
          },
          "children": [
            {
              "type": "img",
              "style": {
                "width": "40",
                "height": "40",
                "src": "${data.photo}"
              }
            }
          ]
        },
        {
          "type": "flex",
          "style": {
            "width": "100%",
            "height": "auto",
            "flexDirection": "column",
            "flexGrow": "1",
            "flexShrink": "1"
          },
          "children": [
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A"
              },
              "text": "${data.robot_title}"
            }
          ]
        },
        {
          "type": "flex",
          "style": {
            "width": "30",
            "height": "52",
            "flexDirection": "column",
            "alignItems": "flex-end",
            "gravity": "top|right"
          },
          "children": [
            {
              "type": "img",
              "style": {
                "width": "12",
                "height": "12",
                "margin": "6 6 0 0",
                "src": "${data.feedback_icon}",
                "gravity": "top|right"
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
        "margin": "5 0 0 0",
        "flexDirection": "row"
      },
      "children": [
        {
          "type": "flex",
          "style": {
            "width": "100%",
            "height": "auto",
            "flexDirection": "column",
            "flexGrow": "1",
            "flexShrink": "1"
          },
          "children": [
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A"
              },
              "text": "${data.title}"
            },
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A"
              },
              "text": "${data.sub_title}"
            }
          ]
        },
        {
          "type": "flex",
          "style": {
            "width": "60",
            "height": "auto",
            "flexDirection": "column",
            "alignItems": "center"
          },
          "children": [
            {
              "type": "img",
              "style": {
                "width": "60",
                "height": "34",
                "src": "${data.icon}"
              }
            },
            {
              "type": "span",
              "style": {
                "fontSize": "12",
                "color": "#3377FF"
              },
              "text": "${data.icon_text}"
            }
          ]
        }
      ]
    }
  ]
}
```