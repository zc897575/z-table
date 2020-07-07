# z-table
uni-app的表格插件
目前兼容H5和微信小程序

### 表格使用
#### props: 
##### tableData [Array | Boolean] | 表格数据 如果为false则显示loading
##### columns [Array | Boolean] | 数据映射表 如果为false则显示loading 
params|类型|说明|默认值
---|---|---|---
title|String|表头文字|-
width|Number|每列宽度|内容宽度
key|String|对应tableData的字段名|-
format|Object|自定义内容|-
sort|Boolean|是否要排序|false
isLink|Object|是否显示为超链接|undefind
listenerClick|Boolean|是否监听点击事件|false
formatNum|Boolean|是否自动格式化数字|true
noSum|Boolean|设置showBottomSum时是否不计算总和|false
##### format格式:
params|类型|说明
---|---|---
template|String|字符串模版用 #key# 表示需要被替换的数据
names|Array[String]|对应template的要被替换内容的key
##### isLink格式: 
params|类型|说明
---|---|---
url|String|链接地址
params|Array[String]|地址带的参数Array[key`|`value, key`|`value, ...]，每一项都是key和value以'`|`'链接,如果不带'`|`'默认键值同名

##### stickSide Boolean | 是否固定右侧首栏 默认不显示
##### showBottomSum Boolean | 是否显示底部统计 默认不显示
##### showLoading Boolean | 是否首次加载首次加载不显示暂无数据内容
##### emptyText String | 空数据显示的文字内容
##### tableHeight Number | 设置表格高度会滚动
##### sort Boolean | 开启排序
##### showSelect Boolean | 开启选择
##### singleSelect Boolean | 在开启选择的状态下是否开起单选
##### textAlign String | 内容对齐方式 left center right
##### titleTextAlign String | 表头对齐方式 left center right

---
#### event: 
##### onSort | 排序事件 返回{key: 被排序列的字段名, type: 正序'asc'/倒序'desc'}
##### onSelect | 选中时触发 返回选择的行的下标
##### onClick | 单元格点击事件 返回点击单元格所属行的数据
---
#### function: 
##### resetSort | 调用后重置排序 *注意:不会触发sort事件

### 效果预览
![小程序二维码](https://wx2.sinaimg.cn/mw690/72f899dcgy1ggd09xhjvzj20760760tu.jpg)
