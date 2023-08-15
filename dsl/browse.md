# D2C 平台专用 DSL 标准定义

标准里本质是定义了一些标签节点， 将这些标签进行组合、嵌套即可描述任意 UI 界面。

> 注意： 这个标准和 HTML 、CSS 完全无关，是一份完全独立的、唯一的标准定义。

## 类型定义

下面是使用 typescript 描述的 DSL 标准定义：

```typescript
{[./dsl.ts]}
```

最后导出的 `DSLNode` 类型包含了所有支持的标签类型，每个标签的类型定义里的 style 字段， 也声明了这个标签所有能使用的所有样式属性。

## 绑定数据

DSL 里大部分字段的值，可以绑定数据里特定的字段， 格式为 '${字段名}' ， 其中字段名支持多级，数据整体本身命名固定为 `data`。

比如， `style` 下的 `color` 属性值需要绑定数据里的 `x` 字段， 则 DSL 里的对应 `color` 属性的描述为 `color: '${data.x}'`。

## 条件语法

DSL 里所有标签都可以使用条件语法，在标签节点的 `condition` 字段里声明即可， 支持 `mfor` `mif` `show` 三种语法。

### `mfor`

表示将一个节点循环输出，类似 vue.js 里的  `v-for` 指令，一般在遍历数组或对象时用来，具体定义参考上面的 `ConditionFor` 类型。
以下是使用 `mfor` 的示例：

遍历数组：

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

遍历对象：

```js
{
    type: 'span',
    condition: {
        mfor: {
            list: '${data.x}', // 变量 x 是个对象
            item: 'val', // 值可以指定任意合法的变量名， 对应对象里单个键值对的值
            index: 'key' // 值可以指定任意合法的变量名， 对应对象里单个键值对的健
        },
    },
    text: '${ key } - ${ val }' // 可以使用 mfor 条件里定义的变量名
}
```

### `mif` 和 `show`

这两个条件比较类似，一个表示是否渲染， 一个表示渲染后是否展示， 值的格式都一样，是一个表达式， 返回值会被强制转为 布尔值。

以下是几个示例：

- `mif: '${x} > 1'`
- `show: '${isShow}'`

## 示例

下面是一个比较完整的示例， 包括了 mock 数据， 以及绑定了 mock 数据的 DSL 描述。

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
// 需要严格符合 DSLNode 类型
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
                    text: '${ data.title }' // 使用 title 字段
                }，
                {
                    type: 'span',
                    text: '${ data.person.name }' // 使用 person.name 字段
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
                    text: '${ i } - ${ item }' // 可以使用 mfor 条件里定义的变量名
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
                                src: '${ val.imgUrl }' // 使用 for 条件里定义的变量名
                            }
                        },
                        {
                            type: 'span',
                            text: '${ key } - ${ val.text }' // 使用 for 条件里定义的变量名
                        }
                    ]
                }
            ]
        }
    ]
}
```
