/**
* @file
* @author 何文林
* @date 2017/9/26
*/
<template>
	<div class="checkwramp" :class="isTrue ? 'active' : ''">
		<i class="checkbox iconfont">{{isTrue ? '&#xe7a1;' : ''}}</i>
		<slot></slot>
	</div>
</template>

<script>
  export default{
    props: {
      isTrue: {
        type: Boolean,
				default: false
			},
      isDisable: {
        type: Boolean,
        default: false
      }
		}
	}
</script>

<style lang="less" scoped>
	.checkwramp{
		display: flex;
		align-items: center
	}
	.checkwramp.active{
		color: #1caf4c;
		i{
			border-color: #1caf4c;
		}
	}
	.checkbox{
		width: 16px;
		height: 16px;
		border: 1px solid #7b7b7b;
		text-align: center;
		line-height: 16px;
		font-size: 12px;
		border-radius: 4px;
		cursor: pointer;
		display: inline-block;
		overflow: hidden;
		box-sizing: border-box;
		background: #ffffff;
		margin-right: 5px;
	}
	.checkbox.active{
		color: #1caf4c;
		border-color: #1caf4c;
	}
	.checkbox:hover{
		color: #1caf4c;
		border-color: #1caf4c;
	}
</style>