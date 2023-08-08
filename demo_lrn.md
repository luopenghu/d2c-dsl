UI 界面描述：

```text
UI 界面从上到下依次分为以下几个模块：
1. 顶部水平排列，左侧是logo按钮， 右侧是正在前往的目的地文字描述
2. 底部两个盒子水平排列，左侧盒子占比90%，右侧满剩余空间，
    左侧盒子包含两个小盒子，两盒子垂直排列，顶部小盒子展示“全程100公里，30分钟”，底部小盒子展示“平峰套餐-本单可减3元  购买 >”，
    右侧盒子展示“查看”文字
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "img": "https://map-mobile-resource.cdn.bcebos.com/icon/service/feedback-center/default/page-header-logo.png",
  "title": "正在前往",
  "destination": "中国美术馆",
  "content": {
    "text": "全程100公里，30分钟",
    "package": "平峰套餐-本单可减3元  购买 >",
    "btn": "查看"
  }
}
```

生成的 DSL 描述：

```json
{
  "type": "flex",
  "style": {
    "width": "100%",
    "height": "auto",
    "padding": "0 10 10 10",
    "flexDirection": "column"
  },
  "children": [
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "height": "auto",
        "flexDirection": "row",
        "alignItems": "center"
      },
      "children": [
        {
          "type": "img",
          "style": {
            "width": "50",
            "height": "40",
            "margin": "5 0 0 0",
            "src": "${data.img}"
          }
        },
        {
          "type": "span",
          "style": {
            "fontSize": "16",
            "color": "#11141A",
            "fontWeight": "bold"
          },
          "text": "${data.title}"
        },
        {
          "type": "span",
          "style": {
            "fontSize": "18",
            "color": "#3377FF",
            "fontWeight": "bold"
          },
          "text": "${data.destination}"
        }
      ]
    },
    {
      "type": "flex",
      "style": {
        "width": "100%",
        "height": "auto",
        "flexDirection": "row",
        "alignItems": "center"
      },
      "children": [
        {
          "type": "flex",
          "style": {
            "width": "90%",
            "height": "auto",
            "flexDirection": "column"
          },
          "children": [
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A"
              },
              "text": "${data.content.text}"
            },
            {
              "type": "span",
              "style": {
                "fontSize": "18",
                "color": "#11141A"
              },
              "text": "${data.content.package}"
            }
          ]
        },
        {
          "type": "span",
          "style": {
            "fontSize": "17",
            "color": "#3377FF",
            "fontWeight": "bold"
          },
          "text": "${data.content.btn}"
        }
      ]
    }
  ]
}
```