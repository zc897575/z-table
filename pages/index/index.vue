<template>
	<view class="content">
		<image class="logo" src="/static/z-table/z-table.png"></image>
		<view class="version">v 1.0.1</view>
		<view class="title">
			注意:
			<view>本示例必须使用sass插件,请在HbuildX的工具-插件安装中安装scss/sass编译插件</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">基础使用示例</view>
			<view class="table">
				<z-table :tableData="baseTableData" :columns="baseColumns"></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{baseHtml}}
					
					js代码:
					baseTableData: [{
						    name: '张三',
						    age: 18,
						    gender: '男'
						},{
						    name: '赵四',
						    age: 16,
						    gender: '女'
						},{
						    name: '王五',
						    age: 20,
						    gender: '男'
						},{
						    name: '李六',
						    age: 18,
						    gender: '女'
						}],
						
					baseColumns: [{
						    title: '姓名',
						    key: 'name',
						    width: 100
						},{
						    title: '性别',
						    key: 'gender',
						    width: 100
						},{
						    title: '年龄',
						    key: 'age',
						    width: 100
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">tableData [Array] <text class="explain-text">需要展示的数据</text></view>
					<view class="explain">columns [Array] <text class="explain-text">表格列的配置描述</text></view>
				</view>
				<view class="explain-title">columns具体参数</view>
				<view class="explain-context">
					<view class="explain">title [String] <text class="explain-text">列名</text></view>
					<view class="explain">key [String] <text class="explain-text">对应tableData中的字段名</text></view>
					<view class="explain">width [Number] <text class="explain-text">列宽(如果不给列宽会出现列宽不一致的问题)</text></view>
				</view>
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">左侧固定的表格示例</view>
			<view class="table">
				<z-table :tableData="stickSideTableData" :columns="stickSideColumns" stickSide></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{stickSideHtml}}
					
					js代码:
					stickSideTableData: [{
						    name: '张三',
						    age: 18,
						    gender: '男'
						},{
						    name: '赵四',
						    age: 16,
						    gender: '女'
						},{
						    name: '王五',
						    age: 20,
						    gender: '男'
						},{
						    name: '李六',
						    age: 18,
						    gender: '女'
						}],
						
					stickSideColumns: [{
						    title: '姓名',
						    key: 'name',
						    width: 100
						},{
						    title: '性别',
						    key: 'gender',
						    width: 400
						},{
						    title: '年龄',
						    key: 'age',
						    width: 400
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">其他参数一样</view>
					<view class="explain">stickSide [Boolean] <text class="explain-text">是否固定左侧第一列</text></view>
				</view>
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">显示底部统计的表格示例</view>
			<view class="table">
				<z-table :tableData="showBottomSumTableData" :columns="showBottomSumColumns" showBottomSum></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{showBottomSumHtml}}
					
					js代码:
					showBottomSumTableData: [{
						    name: '张三',
						    age: 18,
						    gender: '男'
						},{
						    name: '赵四',
						    age: 16,
						    gender: '女'
						},{
						    name: '王五',
						    age: 20,
						    gender: '男'
						},{
						    name: '李六',
						    age: 18,
						    gender: '女'
						}],
						
					showBottomSumColumns: [{
						    title: '姓名',
						    key: 'name',
						    width: 100
						},{
						    title: '性别',
						    key: 'gender',
						    width: 400
						},{
						    title: '年龄',
						    key: 'age',
						    width: 400
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">其他参数一样</view>
					<view class="explain">showBottomSum [Boolean] <text class="explain-text">是否显示底部统计行</text></view>
				</view>
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">自定义内容的表格示例</view>
			<view class="table">
				<z-table :tableData="customTableData" :columns="customColumns"></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{customHtml}}
					
					js代码:
					customTableData: [{
						    name: '张三',
						    age: 18,
						    gender: '男'
						},{
						    name: '赵四',
						    age: 16,
						    gender: '女'
						},{
						    name: '王五',
						    age: 20,
						    gender: '男'
						},{
						    name: '李六',
						    age: 18,
						    gender: '女'
						}],
						
					customColumns: [{
						    title: '姓名',
						    format: {
						        template: "我叫 #name#",
						        names: ["name"]
						    },
						    width: 200
						},{
						    title: '性别',
						    key: 'gender',
						    width: 400
						},{
						    title: '年龄',
						    key: 'age',
						    width: 400
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">其他参数一样</view>
					<view class="explain">
						columns中的key替换为format
					</view>
					<view class="explain">format [Object] <text class="explain-text">自定义内容</text></view>
				</view>
				<view class="explain-title">format具体参数</view>
				<view class="explain-context">
					<view class="explain">template [String] <text class="explain-text">自定义内容模版需要用到tableData中的字段时用#key#(key是字段名)来替换</text></view>
					<view class="explain">name [Array] <text class="explain-text">对应tableData中的字段名数组</text></view>
				</view>
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">单元格内容为链接的示例</view>
			<view class="table">
				<z-table :tableData="isLinkTableData" :columns="isLinkColumns"></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{isLinkHtml}}
					
					js代码:
					isLinkTableData: [{
						    name: '张三',
						    age: 18,
						    gender: '男'
						},{
						    name: '赵四',
						    age: 16,
						    gender: '女'
						},{
						    name: '王五',
						    age: 20,
						    gender: '男'
						},{
						    name: '李六',
						    age: 18,
						    gender: '女'
						}],
						
					isLinkColumns: [{
						    title: '姓名',
						    key: 'name',
						    width: 100
						},{
						    title: '性别',
						    key: 'gender',
						    width: 100
						},{
						    title: '年龄',
						    key: 'age',
						    width: 100
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">其他参数一样</view>
					<view class="explain">
						columns中的添加参数isLink
					</view>
					<view class="explain">isLink [Object] <text class="explain-text">单元格为链接的数据</text></view>
				</view>
				<view class="explain-title">isLink具体参数</view>
				<view class="explain-context">
					<view class="explain">url [String] <text class="explain-text">链接地址, 在H5上地址带http被认为是外部链接</text></view>
					<view class="explain">params [Array] <text class="explain-text">地址带的参数[key|value, key|value, ...]每一项都是key和value以'|'链接,如果不带'|'默认键值同名 value就是tableData中的字段名</text></view>
				</view>
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">自定义判空显示的示例</view>
			<view class="table">
				<z-table :tableData="emptyTableData" :columns="emptyColumns" :showLoading="false" emptyText="设置了showLoading=false才会看到我"></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{emptyHtml}}
					
					js代码:
					emptyTableData:  [],						
					emptyColumns: [{
						    title: '姓名',
						    key: 'name',
						    width: 100
						},{
						    title: '性别',
						    key: 'gender',
						    width: 100
						},{
						    title: '年龄',
						    key: 'age',
						    width: 100
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">其他参数一样</view>
					<view class="explain">showLoading [Boolean] <text class="explain-text">对于第一次渲染表格时显示正在加载</text></view>
					<view class="explain">emptyText [String] <text class="explain-text">空数据显示的文字内容, 默认:暂无数据</text></view>
				</view>
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">自定义高度示例</view>
			<view class="table">
				<z-table :tableData="heightTableData" :columns="heightColumns" :tableHeight="192"></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{heightHtml}}
					
					js代码:
					heightTableData: [{
						    name: '张三',
						    age: 18,
						    gender: '男'
						},{
						    name: '赵四',
						    age: 16,
						    gender: '女'
						},{
						    name: '王五',
						    age: 20,
						    gender: '男'
						},{
						    name: '李六',
						    age: 18,
						    gender: '女'
						}],						
					heightColumns: [{
						    title: '姓名',
						    key: 'name',
						    width: 100
						},{
						    title: '性别',
						    key: 'gender',
						    width: 100
						},{
						    title: '年龄',
						    key: 'age',
						    width: 100
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">其他参数一样</view>
					<view class="explain">tableHeight [Number] <text class="explain-text">表格的高度超出会开启滚动,(实测谷歌亲儿子机型可能会出现下拉触发整个页面下拉刷新的问题)</text></view>
				</view>
			</view>
		</view>
		<view class="example-block">
			<view class="example-title block-title">开启排序示例</view>
			<view class="table">
				<z-table :tableData="sortTableData" :columns="sortColumns"  @onSort="doSort"></z-table>
			</view>
			<view class="example-title">code:</view>
			<scroll-view scroll-x class="codes">
				<text space="ensp">
					html代码:
					{{sortHtml}}
					
					js代码:
					sortTableData: [{
						    name: '张三',
						    age: 18,
						    gender: '男'
						},{
						    name: '赵四',
						    age: 16,
						    gender: '女'
						},{
						    name: '王五',
						    age: 20,
						    gender: '男'
						},{
						    name: '李六',
						    age: 18,
						    gender: '女'
						}],
						
					sortColumns: [{
						    title: '姓名',
						    key: 'name',
						    width: 100
						},{
						    title: '性别',
						    key: 'gender',
						    sort: true,
						    width: 100
						},{
						    title: '年龄',
						    key: 'age',
						    sort: true,
						    width: 100
						}]
				</text>
			</scroll-view>
			<view class="example-explain">
				<view class="explain-title">参数</view>
				<view class="explain-context">
					<view class="explain">sort [Boolean] <text class="explain-text">开启排序</text></view>
				</view>
				<view class="explain-title">回调事件</view>
				<view class="explain-context">
					<view class="explain">onSort [Function] <text class="explain-text">向上触发sort事件传递参数 [Object]: 
					{
				        key: 列的字段名, 
				        type: 正序'asc'/倒序'desc'
					}
					最终排序需要到外部自行实现
					</text></view>
				</view>
				<view class="explain-title">事件</view>
				<view class="explain-context">
					<view class="explain">resetSort [Function] <text class="explain-text">父级可以调用这个方法来重置排序</text></view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
import zTable from '../../components/z-table/z-table.vue';

export default {
	data() {
		return {
			title: 'zTable使用示例',
			baseTableData: [
				{
					name: '张三',
					age: 18,
					gender: '男'
				},
				{
					name: '赵四',
					age: 16,
					gender: '女'
				},
				{
					name: '王五',
					age: 20,
					gender: '男'
				},
				{
					name: '李六',
					age: 18,
					gender: '女'
				}
			],
			baseColumns: [
				{
					title: '姓名',
					key: 'name',
					width: 100
				},
				{
					title: '性别',
					key: 'gender',
					width: 400
				},
				{
					title: '年龄',
					key: 'age',
					width: 400
				}
			],
			baseHtml: '<z-table :tableData="baseTableData" :columns="baseColumns"></z-table>',
			// 固定左侧
			stickSideTableData: [{
				name: '张三',
				age: 18,
				gender: '男'
			},{
				name: '赵四',
				age: 16,
				gender: '女'
			},{
				name: '王五',
				age: 20,
				gender: '男'
			},{
				name: '李六',
				age: 18,
				gender: '女'
			}],
			stickSideColumns: [{
				title: '姓名',
				key: 'name',
				width: 100
			},{
				title: '性别',
				key: 'gender',
				width: 400
			},{
				title: '年龄',
				key: 'age',
				width: 400
			}],
			stickSideHtml: '<z-table :tableData="stickSideTableData" :columns="stickSideColumns" stickSide="true"></z-table>',
			// 底部统计表格
			showBottomSumTableData: [{
				name: '张三',
				age: 18,
				gender: '男'
			},{
				name: '赵四',
				age: 16,
				gender: '女'
			},{
				name: '王五',
				age: 20,
				gender: '男'
			},{
				name: '李六',
				age: 18,
				gender: '女'
			}],
			showBottomSumColumns: [{
				title: '姓名',
				key: 'name',
				width: 100
			},{
				title: '性别',
				key: 'gender',
				width: 400
			},{
				title: '年龄',
				key: 'age',
				width: 400
			}],
			showBottomSumHtml: '<z-table :tableData="showBottomSumTableData" :columns="showBottomSumColumns" showBottomSum="true"></z-table>',
			// 自定义内容的表格
			customTableData: [{
				name: '张三',
				age: 18,
				gender: '男'
			},{
				name: '赵四',
				age: 16,
				gender: '女'
			},{
				name: '王五',
				age: 20,
				gender: '男'
			},{
				name: '李六',
				age: 18,
				gender: '女'
			}],
			customColumns: [{
				title: '姓名',
				format: {
				    template: "我叫 #name#",
				    names: ["name"]
				},
				width: 200
			},{
				title: '性别',
				key: 'gender',
				width: 400
			},{
				title: '年龄',
				key: 'age',
				width: 400
			}],
			customHtml: '<z-table :tableData="customTableData" :columns="customColumns"></z-table>',
			// 单元格为链接
			isLinkTableData: [
				{
					name: '张三',
					age: 18,
					gender: '男'
				},
				{
					name: '赵四',
					age: 16,
					gender: '女'
				},
				{
					name: '王五',
					age: 20,
					gender: '男'
				},
				{
					name: '李六',
					age: 18,
					gender: '女'
				}
			],
			isLinkColumns: [
				{
					title: '姓名',
					key: 'name',
					isLink: {
						url: "https://www.baidu.com",
						params: ["from|name"]
					},
					width: 100
				},
				{
					title: '性别',
					key: 'gender',
					width: 400
				},
				{
					title: '年龄',
					key: 'age',
					width: 400
				}
			],
			isLinkHtml: '<z-table :tableData="isLinkTableData" :columns="isLinkColumns"></z-table>',
			// 空字符串
			emptyTableData: [],
			emptyColumns: [
				{
					title: '姓名',
					key: 'name',
					empty: {
						url: "https://www.baidu.com",
						params: ["from|name"]
					},
					width: 100
				},
				{
					title: '性别',
					key: 'gender',
					width: 400
				},
				{
					title: '年龄',
					key: 'age',
					width: 400
				}
			],
			emptyHtml: '<z-table :tableData="emptyTableData" :columns="emptyColumns" :showLoading="false" emptyText="设置了showLoading=false才会看到我"></z-table>',
			// 自定义高度
			heightTableData: [
				{
					name: '张三',
					age: 18,
					gender: '男'
				},
				{
					name: '赵四',
					age: 16,
					gender: '女'
				},
				{
					name: '王五',
					age: 20,
					gender: '男'
				},
				{
					name: '李六',
					age: 18,
					gender: '女'
				}
			],
			heightColumns: [
				{
					title: '姓名',
					key: 'name',
					height: {
						url: "https://www.baidu.com",
						params: ["from|name"]
					},
					width: 100
				},
				{
					title: '性别',
					key: 'gender',
					width: 400
				},
				{
					title: '年龄',
					key: 'age',
					width: 400
				}
			],
			heightHtml: '<z-table :tableData="heightTableData" :columns="heightColumns" :tableHeight="192"></z-table>',
			// 开启排序
			sortTableData: [
				{
					name: '张三',
					age: 18,
					gender: '男'
				},
				{
					name: '赵四',
					age: 16,
					gender: '女'
				},
				{
					name: '王五',
					age: 20,
					gender: '男'
				},
				{
					name: '李六',
					age: 18,
					gender: '女'
				}
			],
			sortColumns: [
				{
					title: '姓名',
					key: 'name',
					width: 100
				},
				{
					title: '性别',
					key: 'gender',
					sort: true,
					width: 400
				},
				{
					title: '年龄',
					key: 'age',
					sort: true,
					width: 400
				}
			],
			sortHtml: '<z-table :tableData="sortTableData" :columns="sortColumns" @sort="doSort"></z-table>',
		};
	},
	components: {
		zTable
	},
	methods: {
		doSort(res) {
			uni.showToast({
				title: `点击了${res.key}的排序, 排序方式为${res.type}`,
				icon: 'none'
			})
		}
	}
};
</script>

<style>
.content {
	padding: 20upx;
	font-size: 24upx;
	background: #066;
}

.logo {
	display: block;
	height: 144upx;
	width: 144upx;
	margin: 0 auto;
	margin-top: 50upx;
}

.version {
	text-align: center;
	color: #fff;
}

.table {
	text-align: center;
}

.title {
	font-size: 24upx;
	color: #fff;
}

.block-title {
	position: sticky;
	top: var(--window-top);
	padding: 40upx 0 !important;
	text-align: center;
	background: #f7f9ff;
	z-index: 99;
}

.example-block {
	padding: 20upx;
	margin: 20upx -20upx;
	background: #f7f9ff;
}

.example-title {
	font-size: 30upx;
	font-weight: bold;
	margin: 30upx 0 10upx;
}

.example-explain {
	font-size: 24upx;
}

.explain-title {
	margin-top: 30upx;
	padding-bottom: 10upx;
	font-size: 28upx;
	border-bottom: solid 2upx #ccc;
}

.explain-context {
	margin-top: 10upx;
	color: #8f8f94;
}

.explain {
	display: flex;
}

.explain-text {
	flex: 1;
	margin-left: 20upx;
}

.codes {
	padding: 20upx;
	background: #333;
	color: #fff;
	box-sizing: border-box;
}

.codes text {
	white-space: nowrap;
}
</style>
