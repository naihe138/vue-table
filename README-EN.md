# vue-table
a table component for vue2.0

<h2><a href="http://gitblog.naice.me/vue-table/demo/vueTable/index.html#/">demo</a></h2>

<h2><a href="https://github.com/naihe138/vue-table">中文</a></h2>

### vue-table

vue-table: The component encapsulates the daily commonly used functions, paging, selection, operation and fixed scroll around, and other functions, please see the specific effect demo。

### The basic use

````
    import vueTable from 'vue-table'
   
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
	Please see the instructions below
````

#### columns config（columns）

| name  | default  | require  | describe |
| ------------ | ------------ | ------------ | ------------ |
| title   |   |  yes | The table header |
| key |   | yes  | The key of data |
| width   |   | yes  | The width and the minimum width of the column |
| textLine  |   | no  | Specify that a list of the cell text overflow display ellipses |
| textAlign   | left  |  no  | cell text alignment： left（左对齐） center（ 居中） right(右对齐) |


### 表格组件的属性配置说明（table config）

| name  |  type |  default | require  | describe |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| tdata  |  Array |   | yes  | Render the form data |
| tcolumns  | Array  |   | yes  | columns config |
| showSelect | Boolean  |  false  | no  | show left select box |
| showHandle  | Boolean  |  false |  no | show right action box |
| titleHeight  | Number  | 32  | no  | table header hight |
| tdHeight  | Number  | 50  | no  | cell hight |
| titleFixed  | String  | 'auto'  |  no | table head is fixed，default 'auto'（no fixed），'fixed'(fixed), ps：table header fixed should specify the scrollHight（scrollHight） |
|  scrollHight | Numer  | 400  |  no | The height of the scrolling content |
|  selectFixed | Boolean  | false  |   no | the left side of the fixed |
| handleFixed  | Boolean  | false  |   no | the right side of the fixed |
| page  | Object  |   | no  | page config，{totalPage: 50,maxSize: 5} （totalPage)Total number of pages ,（maxSize）show max page |

### events

| name  | require  | describe  |
| ------------ | ------------ | ------------ |
| clickItem  | no  | Click on each row trigger events  |
|  changePage | no | he page number change when the trigger event  |
|  selectCheck | no | select chebox trigger events |

### slot describe

action template slot
````
    <template slot="operations" scope="scope">
    	<span @click="edit(scope.item)">编辑</span>
    	<span @click="edit(scope.item)">删除</span>
    	<span @click="edit(scope.item)">禁用</span>
    </template>
	
````

ps：If feel useful to you Please click a start, you support me is the greatest power


