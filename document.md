**可组合函数 `@Composable`**

**预览函数 `@Preview`**：预览函数是一个无参函数

```kotlin

@Composable

fun MessageCard(name: String) {

    Text(text = "Hello $name!")

}

@Preview

@Preview(name = "Light Mode")

@Preview(

    uiMode = Configuration.UI_MODE_NIGHT_YES,                        // 深色模式

    showBackground = true,

    name = "Dark Mode"

)

@Composable

fun PreviewMessageCard() {                        // 无参函数

    MessageCard("Android")

}

```

**`LocalContext.current` 上下文**

<br/>

# Compose 组合函数库

Compose 提供了一些预定义的组合函数库（界面库）

- Text

- Image

- Column

- Row

- Box 堆叠元素

- LazyColumn、LazyRow 列表

- Spacer 空元素

- Divider 下划线

<br/>

## 修饰符

```kotlin

Modifier

// 尺寸

.fillMaxSize()

.size(40.dp)

.width(4.dp).height(4.dp)

// 间距

.padding(all = 8.dp)

.clip(CircleShape)                                 // 图片剪裁

.background(color = Color.LightGray)                // 背景

.border(1.5.dp, MaterialTheme.colorScheme.primary, CircleShape)                // 边框

// 平滑改变大小

.animateContentSize().padding(1.dp)

// 布局

.align(Alignment.End)

```

<br/>

---

<br/>

# 状态变量

**`remember` 记忆状态值**：创建一个可记忆的状态

- 当 UI 发生变化时（Compose 重新组合），它会记住当前的状态值（将状态值绑定到 UI）

- UI -> State：当 UI 发生变化时，记住 State 状态值

**`mutableStateOf()` 可变状态值**：创建一个可变化的状态，返回一个 `MutableState<>` 对象

- 当状态值发生变化时，Compose 会自动更新对应（绑定）的 UI

- State -> UI：当 State 状态值发生变化时，同步更新 UI

所以当 remeber 和 mutableState() 结合使用时，可创建一个 "数据/UI 互相绑定" 的联动效果

```kotlin 

var checked by remeber { mutableStateOf(false) }

```

<br/>

**`animateColorAsState`**：创建一个可动画的颜色状态 `State<Color>`

- 当颜色值发生变化时，它不会一下子改变，而是平滑的从颜色1变化到颜色2

```kotlin

var color by animateColorAsState {

  if (isExpanded) MaterialTheme.colorScheme.primary else MaterialTheme.colorScheme.surface

}

```

