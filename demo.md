1、下面是一个根据数据循环生成 span 标签的示例

遍历数组`{x: ['a', 'b', 'c']}`：
```js
{
    type: 'span',
    condition: {
        mfor: {
            list: '${data.x}', // 变量 x 是个数组
            item: 'item', // 值就是对应单个列表项的变量名， 可以指定任意合法的变量名
            index: 'i' // 对应单个列表项在数组中的索引， 可以指定任意合法的变量名
        },
    },
    text: '${ i } - ${ item }' // 可以使用 mfor 条件里定义的变量名
}
```

遍历对象`{y: {a: 1, b: 2, c: 3}}`：
```js
{
    type: 'span',
    condition: {
        mfor: {
            list: '${data.y}', // 变量 x 是个对象
            item: 'val', // 值可以指定任意合法的变量名， 对应对象里单个键值对的值
            index: 'key' // 值可以指定任意合法的变量名， 对应对象里单个键值对的健
        },
    },
    text: '${ key } - ${ val }' // 可以使用 mfor 条件里定义的变量名
}
```


2、下面是一个比较完整的示例， 包括了 mock 数据， 以及绑定了 mock 数据的 DSL 描述。

json 格式的 mock 数据如下:

```json
{
    "title": "xxx",
    "person": {
        "name": "Jack"
    },
    "x": ["a", "b"],
    "y": {
        "a": 1,
        "b": 2
    }
}
```

DSL 描述：

> 注意：为了方便描述，DSL 里省略了大部分的样式属性， 同时没有使用 JSON 格式， 而是 JS 里的对象格式

```javascript
// 需要严格符合 Node 类型
{
    type: 'flex';
    style: {
        flexDirection: 'column',
    },
    children: [
        {
            type: 'flex',
            style: {
                flexDirection: 'row',
            },
            children: [
                {
                    type: 'span',
                    text: '${data.title}' // 使用 title 字段
                }，
                {
                    type: 'span',
                    text: '${data.person.name}' // 使用 person.name 字段
                }
            ]
        },
        {
            type: 'flex',
            style: {
                flexDirection: 'row',
            },
            children: [
                {
                    type: 'span',
                    condition: {
                        // 使用 mfor 语法来遍历数组， 以便精简 DSL 体积
                        mfor: {
                            list: '${data.x}', // 变量 x 是个数组
                            item: 'item', // 值就是对应单个列表项的变量名， 可以指定任意合法的变量名
                            index: 'i' // 对应单个列表项在数组中的索引， 可以指定任意合法的变量名
                        },
                    },
                    text: '${i } - ${ item}' // 可以使用 mfor 条件里定义的变量名
                }
            ]
        },
        {

            type: 'flex',
            style: {
                flexDirection: 'row',
            },
            children: [
                {
                    type: 'flex',
                    style: {
                        flexDirection: 'row',
                    },
                    condition: {
                        // 使用 mfor 语法来遍历对象， 以便精简 DSL 体积
                        mfor: {
                            list: '${data.y}', // 也支持对 对象使用 mfor 条件语法
                            item: 'val', // 值可以指定任意合法的变量名， 对应对象里单个键值对的值
                            index: 'key' // 值可以指定任意合法的变量名， 对应对象里单个键值对的健
                        },
                    },
                    children: [
                        {
                            type: 'img',
                            style: {
                                src: '${val.imgUrl}' // 使用 for 条件里定义的变量名
                            }
                        },
                        {
                            type: 'span',
                            text: '${key } - ${ val.text}' // 使用 for 条件里定义的变量名
                        }
                    ]
                }
            ]
        }
    ]
}
```