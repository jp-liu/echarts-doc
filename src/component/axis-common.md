{{target: axis-common}}

#${prefix} name(string)

坐标轴名称。

#${prefix} nameLocation(string) = 'start'

坐标轴名称显示位置。

**可选：**
+ 'start'
+ 'middle'
+ 'end'

#${prefix} nameTextStyle(Object)

坐标轴名称的文字样式。

{{use: partial-text-style(prefix='#' + ${prefix}, name="坐标轴名称")}}

#${prefix} nameGap(number) = 15

坐标轴名称与轴线之间的距离。

#${prefix} inverse(boolean) = false

是否是反向坐标轴。

#${prefix} type(string) = ${axisTypeDefault|default('value')}

坐标轴类型。

可选：
+ `'value'`
    数值轴，适用于连续数据。

+ `'category'`
    类目轴，适用于离散的类目数据，为该类型时必须通过 [data](~${componentType}.data) 设置类目数据。

+ `'time'`
    时间轴，适用于连续的时序数据，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。

+ `'log'`
    对数轴。适用于对数数据。

#${prefix} min(number|string) = 'auto'

坐标轴刻度最小值，在非类目轴中有效。

可以设置成特殊值 `'dataMin'`，此时取数据在该轴上的最小值作为最小刻度。在使用 [dataZoom](~dataZoom) 的数值轴上比较有用。

不设置时会自动计算最小值保证坐标轴刻度的均匀分布。

#${prefix} max(number|string) = 'auto'

坐标轴刻度最大值，在非类目轴中有效。

可以设置成特殊值 `'dataMax'`，此时取数据在该轴上的最大值作为最大刻度。在使用 [dataZoom](~dataZoom) 的数值轴上比较有用。

不设置时会自动计算最大值保证坐标轴刻度的均匀分布。

#${prefix} scale(boolean) = false

只在数值轴中（[type](~${componentType}.type): 'value'）有效。

是否是脱离 0 值比例。设置成 `true` 后坐标刻度不会强制包含零刻度。在双数值轴的散点图中比较有用。

在设置 [min](~${componentType}.min) 和 [max](~${componentType}.max) 之后该配置项无效。

#${prefix} splitNumber(number) = 6

坐标轴的分割段数，需要注意的是这个分割段数只是个预估值，最后实际显示的段数会在这个基础上根据分割后坐标轴刻度显示的易读程度作调整。

只在数值轴中（[type](~${componentType}.type): 'value'）有效。




#${prefix} axisLine(Object)

坐标轴轴线相关设置。

##${prefix} show(boolean) = true

是否显示坐标轴轴线。

{{ if: ${componentType} == 'xAxis' || ${componentType} == 'yAxis' }}

##${prefix} onZero(boolean) = true
X 轴或者 Y 轴的轴线是否在另一个轴的 0 刻度上，只有在另一个轴为数值轴且包含 0 刻度时有效。

{{ /if }}

##${prefix} lineStyle(Object)

{{ use: partial-line-style(prefix='##' + ${prefix}, defaultColor="'#333'", defaultWidth=1, defaultType="'solid'", name="坐标轴线") }}




#${prefix} axisTick(Object)

坐标轴刻度相关设置。

##${prefix} show(boolean) = true

是否显示坐标轴刻度。

##${prefix} interval(number|Function) = 'auto'

坐标轴刻度的显示间隔，默认同 [axisLabel.interval](~${componentType}.axisLabel.interval) 一样。


##${prefix} inside(boolean) = false

坐标轴刻度是否朝内，默认朝外。

##${prefix} length(number) = 5

坐标轴刻度的长度。

##${prefix} lineStyle(Object)

{{ use: partial-line-style(prefix='##' + ${prefix}, defaultColor="'#333'", defaultWidth=1, defaultType="'solid'", name="坐标轴刻度") }}


#${prefix} axisLabel(Object)

坐标轴刻度标签的相关设置。

##${prefix} show(boolean) = true

是否显示刻度标签。

##${prefix} inside(boolean) = false

刻度标签是否朝内，默认朝外。

##${prefix} rotate(number) = 0

刻度标签旋转的角度，在类目轴的类目标签显示不下的时候可以通过旋转防止标签之间重叠。

旋转的角度从 -90 度到 90 度。

##${prefix} margin(number) = 8

刻度标签与轴线之间的距离。

##${prefix} formatter(string|Function)

刻度标签的内容格式器，支持字符串模板和回调函数两种形式。

示例:
```js
// 使用字符串模板，模板变量为刻度默认标签 {value}
formatter: '{value} kg'

// 使用函数模板，函数参数分别为刻度数值（类目），刻度的索引
formatter: function (value, index) {
    // 格式化成月/日，只在第一个刻度显示年份
    var date = new Date(value);
    var texts = [(date.getMonth() + 1), date.getDate()];
    if (idx === 0) {
        texts.unshift(date.getYear());
    }
    return texts.join('/');
}
```
##${prefix} textStyle(Object)

{{ use: partial-text-style(prefix='##' + ${prefix},
defaultColor="'#333'"
)}}




#${prefix} splitLine(Object)

坐标轴在 [grid](~grid) 区域中的分隔线，默认不显示。

##${prefix} show(boolean) = false

是否显示分隔线。

##${prefix} lineTyle(Object)

{{ use: partial-line-style(prefix='##' + ${prefix}, defaultColor="'#333'", defaultWidth=1, defaultType="'solid'", name="分隔线") }}

<!-- overwrite color -->
###${prefix} color(Array|string) = ['#ccc']

分隔线颜色，可以设置成单个颜色。

也可以设置成颜色数组，分隔线会按数组中颜色的顺序依次循环设置颜色。

示例
```
splitLine: {
    lineStyle: {
        // 使用深浅的间隔色
        color: ['#aaa', '#ddd']
    }
}
```



#${prefix} splitArea(Object)

坐标轴在 [grid](~grid) 区域中的分隔区域，默认不显示。

##${prefix} show(boolean) = false

是否显示分隔区域。

##${prefix} areaStyle(Object)

分隔区域的样式设置。

###${prefix} color(Array) = ['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)']

分隔区域颜色。分隔区域会按数组中颜色的顺序依次循环设置颜色。默认是一个深浅的间隔色。

{{ use:partial-style-shadow-opacity(prefix='##' + ${prefix}) }}




#${prefix} data(Array)

类目数据，在类目轴（[type](~${componentType}.type): 'category'）中有效。

示例：

```js
// 所有类目名称列表
data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
// 每一项也可以是具体的配置项，此时取配置项中的 `value` 为类目名
data: [{
    value: '周一',
    // 突出周一
    textStyle: {
        fontSize: 20,
        color: 'red'
    }
}, '周二', '周三', '周四', '周五', '周六', '周日']
```

##${prefix} value(string)

单个类目名称。

##${prefix} textStyle(Object)

类目标签的文字样式。

{{ use:partial-text-style(prefix='##' + ${prefix}) }}