UI 界面描述：

```text
UI 界面从上到下依次分为以下几个模块：
1. 顶部 bar ， 水平排列，左侧是返回按钮， 中间是页面 logo 图片和标题， 右侧是分享按钮
2. 用户信息模块， 垂直排列依次是：
    a. 用户基础信息： 水平排列，左侧是头像， 右侧是昵称和简介， 昵称在上， 简介在下
    b. 用户贡献数据： 水平排列，包括答题数量，金币数，帮助人数三项， 两端对齐， 每一项里面包含名称和对应的数字， 垂直排列， 数字使用较大字号， 在上面， 名称使用常规字号， 在下面
3. 常用功能：水平排列，包含多个可跳转的链接，最多 5 个， 每个功能会显示一个圆形的大图标和文字， 图标和文字垂直排列，图标在上，文字在下
```

根据 UI 界面描述，生成的 mock 数据如下:

```json
{
    "topBar": {
        "backButton": "返回",
        "logo": "https://example.com/logo.png",
        "title": "页面标题",
        "shareButton": "分享"
    },
    "userInfo": {
        "avatar": "https://example.com/avatar.png",
        "nickname": "用户昵称",
        "description": "这是用户的简介",
        "contribution": {
            "questionCount": "答题数量：100",
            "coinCount": "金币数：200",
            "helpedPeople": "帮助人数：50"
        }
    },
    "commonFunctions": [
        {
            "icon": "https://example.com/function1.png",
            "text": "功能1",
            "link": "https://example.com/function1"
        },
        {
            "icon": "https://example.com/function2.png",
            "text": "功能2",
            "link": "https://example.com/function2"
        },
        {
            "icon": "https://example.com/function3.png",
            "text": "功能3",
            "link": "https://example.com/function3"
        },
        {
            "icon": "https://example.com/function4.png",
            "text": "功能4",
            "link": "https://example.com/function4"
        },
        {
            "icon": "https://example.com/function5.png",
            "text": "功能5",
            "link": "https://example.com/function5"
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
        "width": "100%"
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
                    "type": "span",
                    "style": {
                        "fontSize": "16",
                        "color": "#000000"
                    },
                    "text": "${data.topBar.backButton}"
                },
                {
                    "type": "img",
                    "style": {
                        "src": "${data.topBar.logo}",
                        "width": "50",
                        "height": "50"
                    }
                },
                {
                    "type": "span",
                    "style": {
                        "fontSize": "16",
                        "color": "#000000"
                    },
                    "text": "${data.topBar.shareButton}"
                }
            ]
        },
        {
            "type": "flex",
            "style": {
                "flexDirection": "row",
                "justifyContent": "flex-start",
                "width": "100%"
            },
            "children": [
                {
                    "type": "img",
                    "style": {
                        "src": "${data.userInfo.avatar}",
                        "width": "50",
                        "height": "50"
                    }
                },
                {
                    "type": "flex",
                    "style": {
                        "flexDirection": "column",
                    },
                    "children": [
                        {
                            "type": "span",
                            "style": {
                                "fontSize": "16",
                                "color": "#000000"
                            },
                            "text": "${data.userInfo.nickname}"
                        },
                        {
                            "type": "span",
                            "style": {
                                "fontSize": "12",
                                "color": "#888888"
                            },
                            "text": "${data.userInfo.description}"
                        }
                    ]
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
                    "type": "span",
                    "style": {
                        "fontSize": "16",
                        "color": "#000000"
                    },
                    "text": "${data.userInfo.contribution.questionCount}"
                },
                {
                    "type": "span",
                    "style": {
                        "fontSize": "16",
                        "color": "#000000"
                    },
                    "text": "${data.userInfo.contribution.coinCount}"
                },
                {
                    "type": "span",
                    "style": {
                        "fontSize": "16",
                        "color": "#000000"
                    },
                    "text": "${data.userInfo.contribution.helpedPeople}"
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
                    "type": "flex",
                    "style": {
                        "flexDirection": "column",
                        "alignItems": "center",
                        "justifyContent": "center"
                    },
                    "condition": {
                        "mfor": {
                            "list": "${data.commonFunctions}",
                            "item": "function",
                            "index": "i"
                        }
                    },
                    "children": [
                        {
                            "type": "img",
                            "style": {
                                "src": "${function.icon}",
                                "width": "50",
                                "height": "50"
                            }
                        },
                        {
                            "type": "span",
                            "style": {
                                "fontSize": "12",
                                "color": "#888888"
                            },
                            "text": "${function.text}"
                        }
                    ]
                }
            ]
        }
    ]
}
```