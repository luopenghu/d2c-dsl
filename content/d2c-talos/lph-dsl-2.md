# D2C 平台的 DSL 标准定义

DSL 标准里本质是定义了一些标签， 将这些标签进行组合、嵌套即可描述任意 UI 界面。

## 基础 DSL 格式

1. 基础 DSL
```ts
interface DSL {
    // 标签名，取值需要唯一， 取值只能是标准里定义过的标签， 不能自行创造
    type: string;
    // 样式属性，字符串键值对， 里面的字段必须严格按照各个标签定义的类型使用， 不能出现任何未定义过的字段
    style?: Record<string, any>;
    // 暗黑样式属性，字符串键值对， 类似  style ， 仅代表暗黑模式下的样式属性
    darkStyle?: Record<string, any>;
    // 其它属性
    props?: Record<string, any>;
    // 条件判断，目前支持 if、show、for
    condition?: Condition;

    // 只有一个子节点是文本。只在span标签和text标签存在
    text?: string;
    // 子节点集合，只有一个插槽时，可以简写为children
    children?: DSL[];
}
```
2. 容器 DSL
```ts
interface ParentDSL extends DSL {
    // 常规父容器一定有children
    children: DSL[];
}
```

## 样式(`style`)

1. 值类型定义
```ts
// 展示策略
const enum Display {
    // 隐藏，不占位
    None = 'none',
    // 隐藏，占位
    Invisible = 'invisible',
    // 正常展示
    Visible = 'visible'
}

// 超出展示
const enum Overflow {
    // 自动
    Auto = 'auto',
    // 显示
    Visible = 'visible',
    // 隐藏
    Hidden = 'hidden'
}

// linear排列方向
const enum Orientation {
    // 垂直
    V = 'v',
    // 水平
    H = 'h'
}

// 布局方位(linear/frame直接子节点应用)
const enum Gravity {
    Top = 'top',
    Bottom = 'bottom',
    Left = 'left',
    Right = 'right',
    CenterV = 'center_vertical',
    CenterH = 'center_horizontal',
    Center = 'center',
    TopLeft = 'top|left',
    LeftTop = 'left|top',
    TopRight = 'top|right',
    RightTop = 'right|top',
    TopCenterH = 'top|center_horizontal',
    CenterHTop = 'center_horizontal|top',
    LeftCenterV = 'left|center_vertical',
    CenterVLeft = 'center_vertical|left',
    RightCenterV = 'right|center_vertical',
    CenterVRight = 'center_vertical|right',
    BottomLeft = 'bottom|left',
    LeftBottom = 'left|bottom',
    BottomRight = 'bottom|right',
    RightBottom = 'right|bottom',
    BottomCenterH = 'bottom|center_horizontal',
    CenterHBottom = 'center_horizontal|bottom'
}

// 主轴的方向
const enum FlexDirection {
    // 水平
    Row = 'row',
    // 垂直
    Col = 'column'
}

// 是否换行
const enum FlexWrap {
    // flex 元素 被打断到多个行中
    Wrap = 'wrap',
    // flex 的元素被摆放到到一行
    NoWrap = 'nowrap'
}

// 定义项目的放大比例(flex直接子节点应用)
const enum FlexGrow {
    // 等分剩余空间
    Yes = '1',
    // 默认为0，即如果存在剩余空间，也不放大
    No = '0'
}

// 定义了项目的缩小比例(flex直接子节点应用)
const enum FlexShrink {
    // 默认为1，即如果空间不足，该项目将缩小
    Yes = '1',
    // 如果一个项目为0，其他项目都为1，则空间不足时，前者不缩小
    No = '0'
}

// 定义了项目在主轴上的对齐方式
const enum JustifyContent {
    // 左对齐（默认值）
    FlexStart = 'flex-start',
    // 右对齐
    FlexEnd = 'flex-end',
    // 居中
    Center = 'center',
    // 两端对齐，项目之间的间隔都相等
    SpaceBetween = 'space-between',
    // 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍
    SpaceAround = 'space-around'
}

// 定义项目在交叉轴上如何对齐
const enum AlignItems {
    // 交叉轴的起点对齐
    FlexStart = 'flex-start',
    // 交叉轴的终点对齐
    FlexEnd = 'flex-end',
    // 交叉轴的中点对齐
    Center = 'center',
    // 如果项目未设置高度或设为auto，将占满整个容器的高度（默认值）
    Stretch = 'stretch'
}

// 允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性
const enum AlignSelf {
    // 继承父元素
    Auto = 'auto',
    // 交叉轴的起点对齐
    FlexStart = 'flex-start',
    // end：交叉轴的终点对齐
    FlexEnd = 'flex-end',
    // 交叉轴的中点对齐
    Center = 'center',
    // 如果项目未设置高度或设为auto，将占满整个容器的高度（默认值）
    Stretch = 'stretch'
}

// 图片填充方式
const enum ImgScaleType {
    // 不保持宽高比，拉伸填满
    FitXY = 'fitXY',
    // 保持宽高比，居中铺满，多余裁剪
    CenterCrop = 'centerCrop',
    // 保持宽高比，短边填满，剩余空白
    FitCenter = 'fitCenter'
}

// Lottie填充方式
const enum LottieResizeMode {
    // 保持宽高比，全部容纳
    Contain = 'contain'
}

// 文本粗细程度
const enum FontWeight {
    // 正常不加粗
    Normal = 'normal',
    // 500
    Mid = '500',
    // 加粗
    Bold = 'bold'
}

// 文本截断位置
const enum Ellipsis {
    // 开头
    Start = 'start',
    // 中间
    Center = 'center',
    // 结尾
    End = 'end'
}

// 文本修饰线
const enum TextDecoration {
    // 无
    None = 'none',
    // 删除线
    Through = 'line-through',
    // 下划线
    Under = 'underline'
}

// 是否循环播放
const enum LottieRepeat {
    Yse = '1',
    No = '0'
}
```
2. 通用样式类型定义
```ts
interface Style {
    // 展示策略
    visibility?: Display;
    // 宽度。单位为px的数值
    width?: string;
    // 高度，单位为px的数值
    height?: string;
    // 控制元素所有四条边的内边距属性。四个值，依次（顺时针方向）作为上边，右边，下边，和左边的内边距
    // 注意， 这里没有定义  paddingLeft  paddingRight  paddingTop  paddingBottom ， 所以生成 DSL 时请一定不要使用这些子属性
    padding?: string;
    // 控制元素所有四条边的外边距属性。四个值，依次（顺时针方向）作为上边，右边，下边，和左边的外边距
    // 注意， 这里没有定义  marginLeft  marginRight  marginTop  marginBottom ， 所以生成 DSL 时请一定不要使用这些子属性
    margin?: string;
    // 矩形边框宽度。单位为px
    borderWidth?: string;
    // 矩形边框颜色。取值同css中border-color
    borderColor?: string;
    // 圆角边框，单位为px
    borderRadius?: string;
    // 背景颜色。取值同css中background-color
    bgColor?: string;
    // 用于为一个元素设置一个背景图像。值为图片地址
    bgImg?: string;
    // 设置背景图片大小
    scaleType?: ImgScaleType;
    // 设置了元素溢出时所需的行为
    overflow?: Overflow;
    // 属性指定了内部元素是如何在 flex 容器中布局的，定义了主轴的方向 (正方向或反方向)
    flexDirection?: FlexDirection;
    // 属性指定 flex 元素单行显示还是多行显示。如果允许换行，这个属性允许你控制行的堆叠方向
    flexWrap?: FlexWrap;
    // 定义 flex 直接子元素在交叉轴上如何对齐
    alignItems?: AlignItems;
    // 定义 flex 直接子元素在主轴上的对齐方式
    justifyContent?: JustifyContent;
    // 布局方位(linear/frame直接子节点应用)
    gravity?: Gravity;
    // 类似css的z-index
    weight?: string;
    // 定义项目的放大比例(flex直接子元素应用)
    flexGrow?: FlexGrow;
    // 定义了项目的缩小比例(flex直接子元素应用)
    flexShrink?: FlexShrink;
    // 允许 flex 的直接子元素有与其他直接子元素不一样的对齐方式，可覆盖alignItems属性
    alignSelf?: AlignSelf;
    // 图片或者lottie地址
    src: string;
    placeHolder?: string;
    loopTime?: string;
    scale?: string;
    // linear元素的排列方向
    orientation?: Orientation;
    weightSum?: string;
    gap?: string;
    showNum?: string;
    repeat?: string;
    resizeMode?: LottieResizeMode;
    // 文本字体大小。Span标签独有
    fontSize: string;
    // 文本颜色。取值同css中color。Span表情独有
    color: string;
    // 文本截断位置
    ellipsis: Ellipsis;
    // 文本粗细程度
    fontWeight: FontWeight;
    strokeWidth?: string;
    // 文本行高
    lineHeight?: string;
    // 文本修饰线
    decoration?: TextDecoration;
}
```

## 标签

### `Flex` 标签

1. DSL 描述
```ts
// 弹性布局
interface FlexDSL extends ParentDSL {
    type: 'flex';
    style: FlexStyle;
    children: DSL[];
}
```
2. 支持的样式属性(`style`)
```ts
// 支持 flex 布局的样式属性
interface FlexStyle {
    visibility?: Display;
    width?: string;
    height?: string;
    padding?: string;
    borderWidth?: string;
    borderColor?: string;
    borderRadius?: string;
    margin?: string;
    bgColor?: string;
    bgImg?: string;
    scaleType?: ImgScaleType;
    overflow?: Overflow;
    flexDirection?: FlexDirection;
    flexWrap?: FlexWrap;
    alignItems?: AlignItems;
    justifyContent?: JustifyContent;
    gravity?: Gravity;
    weight?: string;
    flexGrow?: FlexGrow;
    flexShrink?: FlexShrink;
    alignSelf?: AlignSelf;
}
```
3. 支持的其它属性(`props`)
暂无

### `Frame` 标签

1. DSL 描述
```ts
// 层叠布局，类似 CSS 里的绝对定位的效果，只用在合适的场景里，一般较少用
interface FrameDSL extends ParentDSL {
    type: 'frameLayout';
    style: FrameStyle;
    children: DSL[];
}
```
2. 支持的样式属性(`style`)
```ts
// 支持 flex 布局的样式属性
interface FrameStyle {
    visibility?: Display;
    width?: string;
    height?: string;
    padding?: string;
    borderWidth?: string;
    borderColor?: string;
    borderRadius?: string;
    margin?: string;
    bgColor?: string;
    bgImg?: string;
    scaleType?: ImgScaleType;
    overflow?: Overflow;
    gravity?: Gravity;
    weight?: string;
    flexGrow?: FlexGrow;
    flexShrink?: FlexShrink;
    alignSelf?: AlignSelf;
}
```
3. 支持的其它属性(`props`)
暂无

### `Img` 标签

1. DSL 描述
```ts
// 图片
interface ImgDSL extends DSL {
    type: 'img';
    style: ImgStyle;
}
```
2. 支持的样式属性(`style`)
```ts
// 支持 flex 布局的样式属性
interface ImgStyle {
    visibility?: Display;
    width?: string;
    height?: string;
    padding?: string;
    borderWidth?: string;
    borderColor?: string;
    borderRadius?: string;
    margin?: string;
    bgColor?: string;
    src: string;
    scaleType: ImgScaleType;
    placeHolder?: string;
    loopTime?: string;
    scale?: string;
    gravity?: Gravity;
    weight?: string;
    flexGrow?: FlexGrow;
    flexShrink?: FlexShrink;
    alignSelf?: AlignSelf;
}
```
3. 支持的其它属性(`props`)
暂无

### `Linear` 标签

1. DSL 描述
```ts
// 线性布局
interface LinearDSL extends ParentDSL {
    type: 'linearLayout';
    style: LinearStyle;
    children: DSL[];
}
```
2. 支持的样式属性(`style`)
```ts
// 支持 flex 布局的样式属性
interface LinearStyle {
    visibility?: Display;
    width?: string;
    height?: string;
    padding?: string;
    borderWidth?: string;
    borderColor?: string;
    borderRadius?: string;
    margin?: string;
    bgColor?: string;
    bgImg?: string;
    scaleType?: ImgScaleType;
    orientation?: Orientation;
    weightSum?: string;
    gap?: string;
    showNum?: string;
    gravity?: Gravity;
    weight?: string;
    flexGrow?: FlexGrow;
    flexShrink?: FlexShrink;
    alignSelf?: AlignSelf;
}
```
3. 支持的其它属性(`props`)
暂无

### `Lottie` 标签

1. DSL 描述
```ts
// lottie
interface LottieDSL extends DSL {
    type: 'lottie';
    style: LottieStyle;
}
```
2. 支持的样式属性(`style`)
```ts
// 支持 flex 布局的样式属性
interface LottieStyle {
    visibility?: Display;
    width?: string;
    height?: string;
    padding?: string;
    borderWidth?: string;
    borderColor?: string;
    borderRadius?: string;
    margin?: string;
    bgColor?: string;
    src: string;
    scaleType: ImgScaleType;
    placeHolder?: string;
    loopTime?: string;
    scale?: string;
    repeat?: string;
    resizeMode?: LottieResizeMode;
    gravity?: Gravity;
    weight?: string;
    flexGrow?: FlexGrow;
    flexShrink?: FlexShrink;
    alignSelf?: AlignSelf;
}
```
3. 支持的其它属性(`props`)
暂无

### `Scroll` 标签

1. DSL 描述
```ts
// 滚动布局
interface ScrollDSL extends ParentDSL {
    type: 'scroll';
    style: ScrollStyle;
    children: DSL[];
}
```
2. 支持的样式属性(`style`)
```ts
// 支持 flex 布局的样式属性
interface ScrollStyle {
    visibility?: Display;
    width?: string;
    height?: string;
    padding?: string;
    borderWidth?: string;
    borderColor?: string;
    borderRadius?: string;
    margin?: string;
    bgColor?: string;
    orientation: Orientation;
    gravity?: Gravity;
    weight?: string;
    flexGrow?: FlexGrow;
    flexShrink?: FlexShrink;
    alignSelf?: AlignSelf;
}
```
3. 支持的其它属性(`props`)
暂无

### `Span` 标签

1. DSL 描述
```ts
// 纯文本
interface SpanDSL extends DSL {
    type: 'span';
    style: SpanStyle;
}
```
2. 支持的样式属性(`style`)
```ts
// 支持 flex 布局的样式属性
interface SpanStyle {
    visibility?: Display;
    fontSize: string;
    color: string;
    ellipsis: Ellipsis;
    fontWeight: FontWeight;
    strokeWidth?: string;
    lineHeight?: string;
    decoration?: TextDecoration;
}
```
3. 支持的其它属性(`props`)
暂无

## 条件语法
条件类型
```ts
interface Condition {
    // 是否渲染
    mif?: string;
    // 循环渲染
    mfor?: ConditionFor;
}

```

### `mfor`
```ts
// 条件 For 类型， 类似 vue 里的  v-for
interface ConditionFor {
    list: string; // 列表变量
    item: string; // 遍历列表项的变量名
    index: string; // 遍历列表项的索引
}
```

### `mif`
条件判断字符串。
示例：`mif: '${x} > 1'`

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
{
    type: 'flex';
    children: [
        {
            type: 'flex';
            children: [
                {
                    type: 'span',
                    text: '${ title }' // 使用 title 字段
                }，
                {
                    type: 'span',
                    text: '${ person.name }' // 使用 person.name 字段
                }
            ]
        },
        {
            type: 'flex',
            children: [
                {
                    type: 'span',
                    condition: {
                        // 这里使用 mfor 对列表形式的 DSL 节点进行了精简
                        mfor: {
                            list: '${x}', // 使用 x 变量，是个数组
                            item: 'dataItem', // 值就是对应单个列表项的变量名， 可以指定任意合法的变量名
                            index: 'i' // 对应单个列表项在数组中的索引， 可以指定任意合法的变量名
                        },
                    },
                    text: '${ i } - ${ dataItem }' // 使用 for 条件里定义的变量名
                }
            ]
        },
        {
            type: 'flex',
            children: [
                {
                    type: 'span',
                    condition: {
                        mfor: {
                            list: '${y}', // 也支持对 对象使用 mfor 条件语法
                            item: 'dataItem', // 值可以指定任意合法的变量名， 对应对象里单个键值对的值
                            index: 'key' // 值可以指定任意合法的变量名， 对应对象里单个键值对的健
                        },
                    },
                    text: '${ key } - ${ dataItem }' // 使用 for 条件里定义的变量名
                }
            ]
        }
    ]
}
```

## 最后

以上即是所有的 DSL 标准定义， 所有的 DSL 描述都只能基于以上定义来生成：

- 只能使用定义的这些标签，即 type 字段的值绝对不能出现其他未定义的标签名
- 各个标签下只能使用定义里对应的样式属性， 即 style 字段下绝对不能出现该标签定义里未出现的属性名
