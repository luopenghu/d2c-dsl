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