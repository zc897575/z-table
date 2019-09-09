<template>
	<view class="content">
		<image class="logo" src="/static/z-table/z-table.png"></image>
		<view class="version">v 1.1.2</view>
		<view class="title">
			注意:
			<view>本示例必须使用sass插件,请在HbuildX的工具-插件安装中安装scss/sass编译插件</view>
			<view class="toggle-btn" @click="showUpData = !showUpData">{{ showUpData ? '隐藏' : '显示' }}更新内容</view>
			<view v-if="showUpData">
				<text space="ensp">
					1.1.2更新内容：
					添加自定义表头columns.title内容可以是html字符串模版，添加表头内容的对齐方式
					1.1.0更新内容：
					添加选择模块，默认多选可选择单选；添加单元格点击事件；尝试使用render函数但只有H5可以使用所以舍去，想尝试的可以把组件内的renderComponents组件注释去掉
					1.0.7更新内容：
					优化dosum事件，如果当前列中有个字段为非数字则计算出来的总和为'-'
					1.0.6更新内容：
					添加title或者表格内容异步获取时的loading，注意如果需要异步加载，需要把tableData初始值设为false，当没有数据的时候值为空数组
					1.0.4更新内容：
					数据高度小于视窗高度的时候，底部统计不再显示跟随最后一条数据显示，而是沉在视窗底部
				</text>
			</view>
		</view>
		<view class="type-select-box">
			<view class="type-select-box-title">
				功能列表
			</view>
			<view :class="['type-select-item', {selected: nowType ===  index}]" v-for="(item, index) in selectContent" :key="item.id" @click="changeType(index)">
				{{ `${index + 1}. ${item.name}` }}
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">{{ selectContent[nowType].name }}</view>
			<view class="table">
				<z-table :textAlign="selectContent[nowType].textAlign" :titleTextAlign="selectContent[nowType].titleTextAlign" :tableData="nowData" :columns="nowColumn" @onSort="doSort" :stickSide="selectContent[nowType].stickSide" :showBottomSum="selectContent[nowType].showBottomSum" :showLoading="false" :emptyText='selectContent[nowType].emptyText'
				 :tableHeight='selectContent[nowType].tableHeight' @onClick="rowClick" :singleSelect="singleSelect" :showSelect="selectContent[nowType].showSelect" @onSelect="tableSelect"></z-table>
			</view>
			<button v-if="selectContent[nowType].showSelect" class="select-btn" type="primary" @click="singleSelect = !singleSelect">{{ !singleSelect ? '开启单选' : '开启多选' }}</button>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{nowHtml}}
		
					js代码:
					tableData: {{ JSON.stringify(nowData).replace(/(\,)/g, `$1\n    			`).replace(/(\})/g, '\n$1').replace(/(\{)/g, '\n$1\n    			') }},
		
					columns: {{ JSON.stringify(nowColumn).replace(/(\,)/g, `$1\n    			`).replace(/(\})/g, '\n$1').replace(/(\{)/g, '\n$1\n    			') }}
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">tableData [Array] <text class="explain-text">需要展示的数据</text></view>
					<view class="explain">columns [Array] <text class="explain-text">表格列的配置描述</text></view>
					<view class="explain">stickSide [Boolean] <text class="explain-text">是否固定左侧第一列</text></view>
					<view class="explain">showBottomSum [Boolean] <text class="explain-text">是否显示底部统计行</text></view>
					<view class="explain">showLoading [Boolean] <text class="explain-text">对于第一次渲染表格时显示正在加载</text></view>
					<view class="explain">emptyText [String] <text class="explain-text">空数据显示的文字内容, 默认:暂无数据</text></view>
					<view class="explain">tableHeight [Number] <text class="explain-text">表格的高度超出会开启滚动,(实测谷歌亲儿子机型可能会出现下拉触发整个页面下拉刷新的问题)</text></view>
					<view class="explain">showSelect [Boolean] <text class="explain-text">开启选择</text></view>
					<view class="explain">singleSelect [Boolean] <text class="explain-text">是否单选，默认false</text></view>
				</view>
				<view class="explain-title">columns具体参数</view>
				<view class="explain-context">
					<view class="explain">title [String] <text class="explain-text">列名</text></view>
					<view class="explain">key [String] <text class="explain-text">对应tableData中的字段名</text></view>
					<view class="explain">width [Number] <text class="explain-text">列宽(如果不给列宽会出现列宽不一致的问题)</text></view>
					<view class="explain">
						columns中的key替换为format
					</view>
					<view class="explain">format [Object] <text class="explain-text">自定义内容</text></view>
				</view>
				<view class="explain">
					columns中的添加参数isLink
				</view>
				<view class="explain">isLink [Object] <text class="explain-text">单元格为链接的数据</text></view>
				<view class="explain">sort [Boolean] <text class="explain-text">开启排序</text></view>
				<view class="explain-title">format具体参数</view>
				<view class="explain-context">
					<view class="explain">template [String] <text class="explain-text">自定义内容模版需要用到tableData中的字段时用#key#(key是字段名)来替换</text></view>
					<view class="explain">name [Array] <text class="explain-text">对应tableData中的字段名数组</text></view>
				</view>
				<view class="explain-title">isLink具体参数</view>
				<view class="explain-context">
					<view class="explain">url [String] <text class="explain-text">链接地址, 在H5上地址带http被认为是外部链接</text></view>
					<view class="explain">params [Array] <text class="explain-text">地址带的参数[key|value, key|value,
							...]每一项都是key和value以"|"链接,如果不带"|"默认键值同名 value就是tableData中的字段名</text></view>
				</view>
				<view class="explain-title">回调事件</view>
				<view class="explain-context">
					<view class="explain">onSort [Function] <text class="explain-text">向上触发sort事件传递参数 [Object]:
							{
							key: 列的字段名,
							type: 正序"asc"/倒序"desc"
							}
							最终排序需要到外部自行实现
						</text></view>
					<view class="explain">onSelect [Function] <text class="explain-text">当选择时触发选中的数据下标的数组 [Array]:
							数组存放对应tableData中的数据的下标
						</text></view>
				</view>
				<view class="explain-title">事件</view>
				<view class="explain-context">
					<view class="explain">resetSort [Function] <text class="explain-text">父级可以调用这个方法来重置排序</text></view>
				</view>
			</view>
		</view>
		
		<view class="example-block">
			<view class="example-title block-title">开启点击事件</view>
			<view class="table">
				<z-table :tableData="clickData" :columns="clickColumns" @onClick="rowClick"></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{clickHtml}}

					js代码:
					clickData: [{
					name: "张三",
					age: 18,
					gender: "男"
					},{
					name: "赵四",
					age: 16,
					gender: "女"
					},{
					name: "王五",
					age: 20,
					gender: "男"
					},{
					name: "李六",
					age: 18,
					gender: "女"
					},
					...
					],

					clickColumns: [{
					title: "姓名",
					key: "name",
					width: 300
					},{
					title: "性别",
					key: "gender",
					width: 300,
					listenerClick: true
					},{
					title: "年龄",
					key: "age",
					width: 300
					}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">columns列表配置</view>
				<view class="explain-context">
					<view class="explain">listenerClick [Boolean] <text class="explain-text">开启当前列的点击事件</text></view>
				</view>
				<view class="explain-title">回调事件</view>
				<view class="explain-context">
					<view class="explain">onClick [Function] <text class="explain-text">点击事件触发 [object]:
							点击事件触发的行对象数据
						</text></view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import zTable from "../../components/z-table/z-table.vue";

	export default {
		data() {
			return {
				title: "zTable使用示例",
				showUpData: false,
				nowType: 0,
				nowData: false,
				nowColumn: false,
				nowHtml: '',
				selectContent: [
					{
						id: 'f0',
						name: '开启所有的功能', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'finaleTableData', // 表格数据
						columns: 'finaleColumns', // 表格列内容
						stickSide: true, // 左侧固定
						showBottomSum: true, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: true ,// 开启选择功能
						html: 'finaleHtml'
					},
					{
						id: 'f1',
						name: '基础使用示例', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'baseTableData', // 表格数据
						columns: 'baseColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'baseHtml'
					},
					{
						id: 'f2',
						name: '左侧固定', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'stickSideTableData', // 表格数据
						columns: 'stickSideColumns', // 表格列内容
						stickSide: true, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'stickSideHtml'
					},
					{
						id: 'f3',
						name: '显示底部统计', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'showBottomSumTableData', // 表格数据
						columns: 'showBottomSumColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: true, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'showBottomSumHtml'
					},
					{
						id: 'f4',
						name: '自定义内容', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'customTableData', // 表格数据
						columns: 'customColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'customHtml'
					},
					{
						id: 'f5',
						name: '单元格内容为链接', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'isLinkTableData', // 表格数据
						columns: 'isLinkColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'isLinkHtml'
					},
					{
						id: 'f6',
						name: '自定义判空显示内容', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'emptyTableData', // 表格数据
						columns: 'emptyColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'emptyHtml'
					},
					{
						id: 'f7',
						name: '自定义高度', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'heightTableData', // 表格数据
						columns: 'heightColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: 200, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'alignHtml'
					},
					{
						id: 'f8',
						name: '开启排序', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'sortTableData', // 表格数据
						columns: 'sortColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'sortHtml'
					},
					{
						id: 'f9'
,						name: '开启选择', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'selectData', // 表格数据
						columns: 'selectColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: true ,// 开启选择功能
						html: 'selectHtml'
					},
					{
						id: 'f10',
						name: '开启点击事件', // 功能名
						textAlign: false, // 内容对齐方式
						titleTextAlign: false, // 表头对齐方式
						tableData: 'clickData', // 表格数据
						columns: 'clickColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'clickHtml'
					},
					{
						id: 'f11',
						name: '设置对齐方式', // 功能名
						textAlign: 'center', // 内容对齐方式
						titleTextAlign: 'center', // 表头对齐方式
						tableData: 'alignTableData', // 表格数据
						columns: 'alignColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'alignHtml'
					},
					{
						id: 'f12',
						name: '自定义表头内容（只能定义样式）', // 功能名
						textAlign: 'center', // 内容对齐方式
						titleTextAlign: 'center', // 表头对齐方式
						tableData: 'customTitleTableData', // 表格数据
						columns: 'customTitleColumns', // 表格列内容
						stickSide: false, // 左侧固定
						showBottomSum: false, // 底部显示统计
						emptyText: '设置了showLoading=false才会看到我', // 表格内容为空时显示的内容
						tableHeight: false, // 表格高度
						showSelect: false ,// 开启选择功能
						html: 'customTitleHtml'
					}
				],
				baseTableData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				baseColumns: [{
						title: "姓名",
						key: "name",
						width: 100
					},
					{
						title: "性别",
						key: "gender",
						width: 400
					},
					{
						title: "年龄",
						key: "age",
						width: 400
					}
				],
				baseHtml: "<z-table :tableData='baseTableData' :columns='baseColumns'></z-table>",
				// 固定左侧
				stickSideTableData: [{
					name: "张三",
					age: 18,
					gender: "男"
				}, {
					name: "赵四",
					age: 16,
					gender: "女"
				}, {
					name: "王五",
					age: 20,
					gender: "男"
				}, {
					name: "李六",
					age: 18,
					gender: "女"
				}],
				stickSideColumns: [{
					title: "姓名",
					key: "name",
					width: 100
				}, {
					title: "性别",
					key: "gender",
					width: 400
				}, {
					title: "年龄",
					key: "age",
					width: 400
				}],
				stickSideHtml: "<z-table :tableData='stickSideTableData' :columns='stickSideColumns' stickSide='true'></z-table>",
				// 底部统计表格
				showBottomSumTableData: [{
					name: "张三",
					age: 18,
					gender: "男"
				}, {
					name: "赵四",
					age: 16,
					gender: "女"
				}, {
					name: "王五",
					age: 20,
					gender: "男"
				}, {
					name: "李六",
					age: 18,
					gender: "女"
				}],
				showBottomSumColumns: [{
					title: "姓名",
					key: "name",
					width: 100
				}, {
					title: "性别",
					key: "gender",
					width: 400
				}, {
					title: "年龄",
					key: "age",
					width: 400
				}],
				showBottomSumHtml: "<z-table :tableData='showBottomSumTableData' :columns='showBottomSumColumns' showBottomSum='true'></z-table>",
				// 自定义内容的表格
				customTableData: [{
					name: "张三",
					age: 18,
					gender: "男"
				}, {
					name: "赵四",
					age: 16,
					gender: "女"
				}, {
					name: "王五",
					age: 20,
					gender: "男"
				}, {
					name: "李六",
					age: 18,
					gender: "女"
				}],
				customColumns: [{
					title: "姓名",
					format: {
						template: "我叫 #name#",
						names: ["name"]
					},
					width: 200
				}, {
					title: "性别",
					key: "gender",
					width: 400
				}, {
					title: "年龄",
					key: "age",
					width: 400
				}],
				customHtml: "<z-table :tableData='customTableData' :columns='customColumns'></z-table>",
				// 单元格为链接
				isLinkTableData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				isLinkColumns: [{
						title: "姓名",
						key: "name",
						isLink: {
							url: "https://www.baidu.com",
							params: ["from|name"]
						},
						width: 100
					},
					{
						title: "性别",
						key: "gender",
						width: 400
					},
					{
						title: "年龄",
						key: "age",
						width: 400
					}
				],
				isLinkHtml: "<z-table :tableData='isLinkTableData' :columns='isLinkColumns'></z-table>",
				// 空字符串
				emptyTableData: [],
				emptyColumns: [{
						title: "姓名",
						key: "name",
						width: 100
					},
					{
						title: "性别",
						key: "gender",
						width: 400
					},
					{
						title: "年龄",
						key: "age",
						width: 400
					}
				],
				emptyHtml: "<z-table :tableData='emptyTableData' :columns='emptyColumns' :showLoading='false' emptyText='设置了showLoading=false才会看到我'></z-table>",
				// 自定义高度
				heightTableData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				heightColumns: [{
						title: "姓名",
						key: "name",
						width: 100
					},
					{
						title: "性别",
						key: "gender",
						width: 400
					},
					{
						title: "年龄",
						key: "age",
						width: 400
					}
				],
				heightHtml: "<z-table :tableData='heightTableData' :columns='heightColumns' :tableHeight='192'></z-table>",
				// 开启排序
				sortTableData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				sortColumns: [{
						title: "姓名",
						key: "name",
						width: 100
					},
					{
						title: "性别",
						key: "gender",
						sort: true,
						width: 400
					},
					{
						title: "年龄",
						key: "age",
						sort: true,
						width: 400
					}
				],
				sortHtml: "<z-table :tableData='sortTableData' :columns='sortColumns' @sort='doSort'></z-table>",
				finaleTableData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					},
					{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					},
					{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				finaleColumns: [{
						title: "姓名",
						format: {
							template: "我叫 #name#",
							names: ["name"]
						},
						isLink: {
							url: "https://www.baidu.com",
							params: ["from|name"]
						},
						width: 200
					},
					{
						title: "性别",
						key: "gender",
						sort: true,
						width: 400,
						listenerClick: true
					},
					{
						title: "年龄",
						key: "age",
						sort: true,
						width: 400
					}
				],
				finaleHtml: "<z-table :tableData='finaleTableData' :columns='finaleColumns' stickSide showBottomSum emptyText='设置了showLoading=false才会看到我' :tableHeight='600' showSelect @onClick='rowClick' @onSelect='tableSelect' @onSort='doSort' ></z-table>",
				singleSelect: false,
				selectData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				selectColumns: [{
						title: "姓名",
						key: 'name',
						width: 300
					},
					{
						title: "性别",
						key: "gender",
						width: 300
					},
					{
						title: "年龄",
						key: "age",
						width: 300
					}
				],
				selectHtml: "<z-table showSelect :singleSelect='singleSelect' :tableData='selectData' :columns='selectColumns' @onSelect='tableSelect'></z-table>",
				clickData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				clickColumns: [{
						title: "姓名",
						key: 'name',
						width: 300
					},
					{
						title: "性别",
						key: "gender",
						width: 300,
						listenerClick: true
					},
					{
						title: "年龄",
						key: "age",
						width: 300
					}
				],
				clickHtml: "<z-table :tableData='selectData' :columns='selectColumns' @onClick='rowClick'></z-table>",
				alignTableData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				alignColumns: [{
						title: "姓名",
						key: 'name',
						width: 200
					},
					{
						title: '性别',
						key: "gender",
						width: 400,
					},
					{
						title: "年龄",
						key: "age",
						width: 400
					}
				],
				alignHtml: "<z-table :tableData='alignTableData' :columns='alignColumns'></z-table>",
				customTitleTableData: [{
						name: "张三",
						age: 18,
						gender: "男"
					},
					{
						name: "赵四",
						age: 16,
						gender: "女"
					},
					{
						name: "王五",
						age: 20,
						gender: "男"
					},
					{
						name: "李六",
						age: 18,
						gender: "女"
					}
				],
				customTitleColumns: [{
						title: '<span style="color: #333"><span style="display: inline-block; width: 10px; height: 10px; line-height: 10px; margin-right: 5px; border: solid 1px #000; border-radius: 50%; font-size: 11px; text-align: center; vertical-align: middle;">!</span><span st yle="vertical-align: middle;">姓名</span></span>',
						key: 'name',
						width: 200
					},
					{
						title: '<span style="color: red">性别</span>',
						key: "gender",
						width: 400,
					},
					{
						title: '<span style="color: blue">年龄</span>',
						key: "age",
						width: 400
					}
				],
				customTitleHtml: "<z-table :tableData='customTitleTableData' :columns='customTitleColumns'></z-table>",
			};
		},
		components: {
			zTable
		},
		watch: {
			nowType: {
				handler() {
					this.nowData = false
					this.nowColumn = false
					this.debounce(this.setTable)()
				},
				immediate: true
			}
		},
		methods: {
			changeType(index) {
				if (this.nowType === index) return
				this.nowType = index
			},
			setTable() {
				this.nowData = this.$data[this.selectContent[this.nowType].tableData]
				this.nowColumn = this.$data[this.selectContent[this.nowType].columns]
				this.nowHtml = this.$data[this.selectContent[this.nowType].html]
				console.log(this.nowHtml)
			},
			debounce(fn, time = 1000) {
				let timer = null
				return function() {
					if (timer) clearTimeout(timer)
					timer = setTimeout(fn, time)
				}
			},
			doSort(res) {
				uni.showToast({
					title: `点击了${res.key}的排序, 排序方式为${res.type}`,
					icon: "none"
				})
			},
			rowClick(item) {
				uni.showToast({
					title: `${JSON.stringify(item)}数据被点击`,
					icon: 'none'
				})
			},
			tableSelect(selectList) {
				uni.showToast({
					title: `选中了TableData中下标为${selectList.join(',')}的元素`,
					icon: 'none'
				})
			}
		}
	};
</script>

<style lang="scss">
	.content {
		padding: 20rpx;
		font-size: 24rpx;
		background: #066;
	}

	.logo {
		display: block;
		height: 144rpx;
		width: 144rpx;
		margin: 0 auto;
		margin-top: 50rpx;
	}

	.version {
		text-align: center;
		color: #fff;
	}

	.table {
		text-align: center;
	}

	.title {
		margin-bottom: 20rpx;
		font-size: 24rpx;
		color: #fff;
	}

	.block-title {
		position: sticky;
		top: var(--window-top);
		padding: 40rpx 0 !important;
		text-align: center;
		background: #f7f9ff;
		z-index: 99;
	}

	.example-block {
		padding: 20rpx;
		margin: 20rpx -20rpx;
		background: #f7f9ff;
	}

	.example-title {
		font-size: 30rpx;
		font-weight: bold;
		margin: 30rpx 0 10rpx;
	}

	.example-explain {
		font-size: 24rpx;
	}

	.explain-title {
		margin-top: 30rpx;
		padding-bottom: 10rpx;
		font-size: 28rpx;
		border-bottom: solid 2rpx #ccc;
	}

	.explain-context {
		margin-top: 10rpx;
		color: #8f8f94;
	}

	.explain {
		display: flex;
	}

	.explain-text {
		flex: 1;
		margin-left: 20rpx;
	}

	.codes {
		padding: 20rpx;
		background: #333;
		color: #fff;
		box-sizing: border-box;
	}

	.codes text {
		white-space: nowrap;
	}

	.toggle-btn {
		margin: 10rpx 0;
		padding: 10rex;
		color: #1c1;
	}

	.select-btn {
		display: inline-block;
		width: 200rpx;
		margin-top: 20rpx;
		font-size: 24rpx;
	}
	
	.type-select-box {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		padding: 20rpx;
		margin: 0 -20rpx;
		background: #f7f9ff;
	}
	
	.type-select-box-title {
		width: 100%;
		margin-bottom: 20rpx;
		font-size: 36rpx;
	}
	
	.type-select-item {
		flex: 1;
		padding: 20rpx;
		margin-right: 10rpx;
		margin-bottom: 10rpx;
		white-space: nowrap;
		border: solid 2rpx #066;
		border-radius: 4rpx;
		font-size: 28rpx;
		background: #fff;
		color: #006666;
		text-align: center;
		
		&.selected {
			background: #066;
			color: #fff;
		}
	}
</style>
