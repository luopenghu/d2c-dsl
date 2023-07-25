UI 界面描述：

```text
UI 界面从上到下依次分为以下几个模块：
1. 顶部从左到右依次是：定位图标，标题，地址信息，关闭图标
2. 答题模块，从做到右依次是：
    a、图片，图片下面是距离
    b、从上到下依次是：
      ba、标题
      bb、金币图标，领取金币内容，帮助图标，帮助人数内容
      bc、最多三个按钮
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
  "topModule": {
    "locationIcon": "https://example.com/locationIcon.png",
    "title": "UI界面标题",
    "addressInfo": "北京市朝阳区",
    "closeIcon": "https://example.com/closeIcon.png"
  },
  "questionModule": {
    "image": "https://example.com/questionImage.png",
    "title": "问题标题",
    "coinIcon": "https://example.com/coinIcon.png",
    "coinInfo": "领取100金币",
    "helpIcon": "https://example.com/helpIcon.png",
    "helpNumber": "帮助人数：1000",
    "buttons": [
      "答案选项1",
      "答案选项2",
      "答案选项3"
    ]
  }
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
            "type": "flex",
            "style": {
                "flexDirection": "row",
                "justifyContent": "space-between",
                "width": "100%"
            },
            "children": [
                {
                    "type": "img",
                    "style": {
                        "src": "${data.topModule.locationIcon}",
                        "width": "20",
                        "height": "20"
                    }
                },
                {
                    "type": "span",
                    "style": {
                        "fontSize": "16",
                        "color": "#000000"
                    },
                    "text": "${data.topModule.title}"
                },
                {
                    "type": "span",
                    "style": {
                        "fontSize": "14",
                        "color": "#666666"
                    },
                    "text": "${data.topModule.addressInfo}"
                },
                {
                    "type": "img",
                    "style": {
                        "src": "${data.topModule.closeIcon}",
                        "width": "20",
                        "height": "20"
                    }
                }
            ]
        },
        {
            "type": "flex",
            "style": {
                "flexDirection": "row",
                "justifyContent": "space-between",
                "width": "100%"
            },
            "children": [
                {
                    "type": "img",
                    "style": {
                        "src": "${data.questionModule.image}",
                        "width": "100",
                        "height": "100"
                    }
                },
                {
                    "type": "flex",
                    "style": {
                        "flexDirection": "column",
                        "justifyContent": "space-between",
                        "width": "100%"
                    },
                    "children": [
                        {
                            "type": "span",
                            "style": {
                                "fontSize": "16",
                                "color": "#000000"
                            },
                            "text": "${data.questionModule.title}"
                        },
                        {
                            "type": "flex",
                            "style": {
                                "flexDirection": "row",
                                "justifyContent": "space-between"
                            },
                            "children": [
                                {
                                    "type": "img",
                                    "style": {
                                        "src": "${data.questionModule.coinIcon}",
                                        "width": "20",
                                        "height": "20"
                                    }
                                },
                                {
                                    "type": "span",
                                    "style": {
                                        "fontSize": "14",
                                        "color": "#666666"
                                    },
                                    "text": "${data.questionModule.coinInfo}"
                                },
                                {
                                    "type": "img",
                                    "style": {
                                        "src": "${data.questionModule.helpIcon}",
                                        "width": "20",
                                        "height": "20"
                                    }
                                },
                                {
                                    "type": "span",
                                    "style": {
                                        "fontSize": "14",
                                        "color": "#666666"
                                    },
                                    "text": "${data.questionModule.helpNumber}"
                                }
                            ]
                        },
                        {
                            "type": "flex",
                            "style": {
                                "flexDirection": "row"
                            },
                            "children": [
                                {
                                    "type": "flex",
                                    "condition": {
                                        "mfor": {
                                            "list": "${data.questionModule.buttons}",
                                            "item": "button",
                                            "index": "i"
                                        }
                                    },
                                    "children": [
                                        {
                                            "type": "span",
                                            "style": {
                                                "fontSize": "14",
                                                "color": "#666666"
                                            },
                                            "text": "${button}"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```