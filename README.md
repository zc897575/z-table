# z-table
uni-app的表格插件
目前兼容H5和微信小程序

### 表格使用
#### props: 
##### tableData Array | 表格数据
##### columns Array | 数据映射表 每列params => title(表头文字), width(每列宽度) [, key(对应tableData的字段名) || format(自定义内容), sort(是否要排序), isLink(是否显示为超链接Object)]
##### format格式: {template: 字符串模版用#key#表示需要被替换的数据,names: 对应template属性内要被替换的内容的key}
##### isLink格式: {url: 链接地址, params: 地址带的参数Array[key|value, key|value, ...]每一项都是key和value以'|'链接,如果不带'|'默认键值同名}
##### stickSide Boolean | 是否固定右侧首栏 默认不显示
##### showBottomSum Boolean | 是否显示底部统计 默认不显示
##### showLoading Boolean | 是否首次加载首次加载不显示暂无数据内容
##### emptyText String | 空数据显示的文字内容
##### tableHeight Number | 设置表格高度会滚动
##### sort Boolean | 开启排序
---
#### event: 
##### onSort | 排序事件 返回{key: 被排序列的字段名, type: 正序'asc'/倒序'desc'}
---
#### function: 
##### resetSort | 调用后重置排序 *注意:不会触发sort事件

### 效果预览
![微信小程序二维码](https://mp.weixin.qq.com/wxopen/qrcode?action=show&type=2&fakeid=3839115583&token=1672400506)
