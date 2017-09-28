# vue-table
a table component for vue2.0

<h2><a href="http://gitblog.naice.me/vue-table/demo/vueTable/index.html#/">demo</a></h2>

<h2><a href="https://github.com/naihe138/vue-table/blob/master/README-EN.md">English</a></h2>


### vue-table 组件使用

vue-table组件封装了日常常用的功能，分页、选择、操作以及左右固定滚动等功能，具体效果请看 demo。

### 基本使用

````
    import vueTable from 'vue-table2'
   
    <vue-table :tdata="tableData"
    		   :tcolumns="tableColumns"
    		   :showHandle="true"
    		   :tdHeight="40"
    		   v-on:clickItem="tableSelectItem">
    	<template slot="operations" scope="scope">
    		<span @click="edit(scope.item)">编辑</span>
    		<span @click="edit(scope.item)">删除</span>
    		<span @click="edit(scope.item)">禁用</span>
    	</template>
    </vue-table>
	
	/*
	const columns1 = [
    {
      title: '机构编号',
      key: 'number',
      width: 85,
      textAlign: 'left'
    },
    {
      title: '机构名称',
      key: 'name',
      width: 292,
      textAlign: 'left',
      textLine: 2,
      selectText: true
    },
    {
      title: '类型',
      key: 'type',
      width: 180,
      textAlign: 'center'
    },
    {
      title: '状态',
      key: 'brand',
      width: 82,
      textAlign: 'center'
    }
  ]
	*/
	请看下面的说明
````

#### 列的配置（columns）

| 名称  | 默认  | 是否必须  | 说明 |
| ------------ | ------------ | ------------ | ------------ |
| title   |   |  是 | 表头标题 |
| key |   | 是  | 数据的 key 值 |
| width   |   | 是  | 列的宽度以及最小宽度 |
| textLine  |   | 否  | 指定那一列的单元格文子溢出显示省略号 |
| textAlign   | left  | 否  | 指定那一列的单元格文字的对齐方式left（左对齐） center（ 居中） right(右对齐) |


### 表格组件的属性配置说明（table config）

| 名称  |  类型 |  默认 | 是否必须  | 说明 |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| tdata  |  Array |   | 是  | 渲染表格的数据 |
| tcolumns  | Array  |   | 是  | 表格列的配置 |
| showSelect | Boolean  |  false  | 否  | 是否显示左侧选择框 |
| showHandle  | Boolean  |  false |  否 | 是否显示右侧操作内容 |
| titleHeight  | Number  | 32  | 否  | 表头高度 |
| tdHeight  | Number  | 50  | 否  | 单元格高度 |
| titleFixed  | String  | 'auto'  |  否 | 表头是否固定，默认'auto'（不固定），'fixed'(固定),注意：表头固定需指定滚动内容（scrollHight）的高度 |
|  scrollHight | Numer  | 400  |  否 | 滚动内容的高度 |
|  selectFixed | Boolean  | false  |   否 | 左侧是否固定 |
| handleFixed  | Boolean  | false  |   否 | 右侧是否固定 |
| page  | Object  |   | 否  | 不配置这个 page 就不显示 底部页码，配置的话{totalPage: 50,maxSize: 5} （totalPage)总页数 ,（maxSize）显示页数 |

### 事件相关

| 名称  | 是否必须  | 说明  |
| ------------ | ------------ | ------------ |
| clickItem  | 否   | 点击每一行时候触发的事件  |
|  changePage |  否 | 页码改变时触发的事件  |
|  selectCheck |  否 | 选择左边 chebox 时候触发的事件  |

### slot 说明

操作的模板 slot
````
    <template slot="operations" scope="scope">
    	<span @click="edit(scope.item)">编辑</span>
    	<span @click="edit(scope.item)">删除</span>
    	<span @click="edit(scope.item)">禁用</span>
    </template>
	
````

ps：如果觉得对你有用的话 请点一个 start，你的支持我才是最大的动力


