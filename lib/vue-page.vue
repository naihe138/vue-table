/**
* @file 分页组件
* @author 何文林
* @date 2017/9/8
*/
<template>
	<nav aria-label="Page navigation" class="navigation">
		<ul class="pagination" :class="pageSize">
			<!--<li :class="{'disabled':value<=1}" v-if="boundaryLinks" @click="onPageChange(1)" data-action="first">-->
			<!--<a role="button">-->
			<!--<span aria-hidden="true">&laquo;</span>-->
			<!--</a>-->
			<!--</li>-->
			<li :class="{'disabled':value<=1}" v-if="directionLinks" @click="onPageChange(value-1)" data-action="prev-page">
				<a role="button">
					<span aria-hidden="true">上一页</span>
				</a>
			</li>
			<li v-if="sliceStart>0" @click="toPage(1)" data-action="prev-group">
				<a role="button">...</a>
			</li>
			<li v-for="item in sliceArray" :key="item" @click="onPageChange(item+1)" class="pagination-page"
					:class="{'active': value==item+1}">
				<a role="button">{{item + 1}}</a>
			</li>
			<li v-if="sliceStart<totalPage-maxSize" @click="toPage(0)" data-action="next-group">
				<a role="button">...</a>
			</li>
			<li :class="{'disabled':value>=totalPage}" v-if="directionLinks" @click="onPageChange(value+1)"
					data-action="next-page">
				<a role="button">
					<span aria-hidden="true">下一页</span>
				</a>
			</li>
			<!--<li :class="{'disabled':value>=totalPage}" v-if="boundaryLinks" @click="onPageChange(totalPage)"-->
			<!--data-action="last">-->
			<!--<a role="button">-->
			<!--<span aria-hidden="true">&raquo;</span>-->
			<!--</a>-->
			<!--</li>-->
		</ul>
		<div class="passPage">
			第 <input type="text" class="form-control" :class="'input-' + size" v-model="passPage">页
			<input class="btn btn-default" :class="'input-' + size" type="button" value="跳转" @click="toPassPage">
		</div>
	</nav>
</template>

<script>
  export default {
    props: {
      value: {
        type: Number
      },
      boundaryLinks: {
        type: Boolean,
        'default': false
      },
      directionLinks: {
        type: Boolean,
        'default': true
      },
      size: {
        type: String,
        'default': ''
      },
      totalPage: {
        type: Number
      },
      maxSize: {
        type: Number,
        'default': 5
      }
    },
    data () {
      return {
        sliceStart: 0,
        passPage: null
      }
    },
    watch: {
      value (value) {
        if (value > this.sliceStart + this.maxSize) {
          if (value > this.totalPage - this.maxSize) {
            this.sliceStart = this.totalPage - this.maxSize
          } else {
            this.sliceStart = value - 1
          }
        } else if (value < this.sliceStart + 1) {
          if (value - this.maxSize > 0) {
            this.sliceStart = value - this.maxSize
          } else {
            this.sliceStart = 0
          }
        }
      }
    },
    computed: {
      pageSize () {
        return this.size ? `pagination-${this.size}` : ``
      },
      pageArray () {
        let newArray = []
        for (let i = 0; i < this.totalPage; i++) {
          newArray.push(i)
        }
        return newArray
      },
      sliceArray () {
        let afterSlice = this.pageArray.slice()
        return afterSlice.slice(this.sliceStart, this.sliceStart + this.maxSize)
      }
    },
    methods: {
      onPageChange (page) {
        if (page > 0 && page <= this.totalPage) {
          this.$emit('input', page)
          this.$emit('change', page)
        }
      },
      toPage (pre) {
        let start = pre ? this.sliceStart - this.maxSize : this.sliceStart + this.maxSize
        if (start < 0) {
          this.sliceStart = 0
        } else if (start > this.totalPage - this.maxSize) {
          this.sliceStart = this.totalPage - this.maxSize
        } else {
          this.sliceStart = start
        }
      },
      toPassPage() {
        if (Number(this.passPage)) {
          this.onPageChange(Number(this.passPage))
          this.$emit('input', Number(this.passPage))
          this.$emit('change', Number(this.passPage))
        } else {
          console.log('输入正确的页码')
        }
      }
    }
  }
</script>

<style lang="less" scoped>
	.btn {
		display: inline-block;
		padding: 6px 12px;
		margin-bottom: 0;
		font-size: 14px;
		font-weight: normal;
		line-height: 1.42857143;
		text-align: center;
		white-space: nowrap;
		vertical-align: middle;
		-ms-touch-action: manipulation;
		touch-action: manipulation;
		cursor: pointer;
		-webkit-user-select: none;
		-moz-user-select: none;
		-ms-user-select: none;
		user-select: none;
		background-image: none;
		border: 1px solid transparent;
		border-radius: 4px;
	}

	.btn:focus,
	.btn:active:focus,
	.btn.active:focus,
	.btn.focus,
	.btn:active.focus,
	.btn.active.focus {
		outline: 5px auto -webkit-focus-ring-color;
		outline-offset: -2px;
	}

	.btn:hover,
	.btn:focus,
	.btn.focus {
		color: #333;
		text-decoration: none;
	}

	.btn:active,
	.btn.active {
		background-image: none;
		outline: 0;
		-webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
		box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
	}

	.btn.disabled,
	.btn[disabled],
	fieldset[disabled] .btn {
		cursor: not-allowed;
		filter: alpha(opacity=65);
		-webkit-box-shadow: none;
		box-shadow: none;
		opacity: .65;
	}

	a.btn.disabled,
	fieldset[disabled] a.btn {
		pointer-events: none;
	}
	.btn-default {
		color: #333;
		background-color: #fff;
		border-color: #ccc;
	}

	.btn-default:focus,
	.btn-default.focus {
		color: #333;
		background-color: #e6e6e6;
		border-color: #8c8c8c;
	}

	.btn-default:hover {
		color: #333;
		background-color: #e6e6e6;
		border-color: #adadad;
	}

	.btn-default:active,
	.btn-default.active,
	.open>.dropdown-toggle.btn-default {
		color: #333;
		background-color: #e6e6e6;
		border-color: #adadad;
	}

	.btn-default:active:hover,
	.btn-default.active:hover,
	.open>.dropdown-toggle.btn-default:hover,
	.btn-default:active:focus,
	.btn-default.active:focus,
	.open>.dropdown-toggle.btn-default:focus,
	.btn-default:active.focus,
	.btn-default.active.focus,
	.open>.dropdown-toggle.btn-default.focus {
		color: #333;
		background-color: #d4d4d4;
		border-color: #8c8c8c;
	}

	.btn-default:active,
	.btn-default.active,
	.open>.dropdown-toggle.btn-default {
		background-image: none;
	}

	.btn-default.disabled:hover,
	.btn-default[disabled]:hover,
	fieldset[disabled] .btn-default:hover,
	.btn-default.disabled:focus,
	.btn-default[disabled]:focus,
	fieldset[disabled] .btn-default:focus,
	.btn-default.disabled.focus,
	.btn-default[disabled].focus,
	fieldset[disabled] .btn-default.focus {
		background-color: #fff;
		border-color: #ccc;
	}

	.btn-default .badge {
		color: #fff;
		background-color: #333;
	}
	.input-lg {
		height: 46px;
		padding: 10px 16px;
		font-size: 18px;
		line-height: 1.3333333;
		border-radius: 6px;
	}

	select.input-lg {
		height: 46px;
		line-height: 46px;
	}

	textarea.input-lg,
	select[multiple].input-lg {
		height: auto;
	}
	form-control-static.input-lg,
	.form-control-static.input-sm {
		padding-right: 0;
		padding-left: 0;
	}

	.input-sm {
		height: 30px;
		padding: 5px 10px;
		font-size: 12px;
		line-height: 1.5;
		border-radius: 3px;
	}

	select.input-sm {
		height: 30px;
		line-height: 30px;
	}

	textarea.input-sm,
	select[multiple].input-sm {
		height: auto;
	}
	.navigation {
		display: flex;
		.passPage {
			display: flex;
			align-items: center;
			padding-left: 20px;
			input[type="text"] {
				margin: 0 5px;
				text-align: center;
			}
			input[type="text"].input-lg{
				width: 64px;
				height: 24px;
			}
			input[type="text"].input-sm{
				width: 44px;
				height: 16px;
			}
			input[type="text"].input-md{
				width: 34px;
				height: 20px;
			}
			input[type="button"] {
				margin-left: 20px;
			}
		}
	}
	.form-control {
		display: block;
		width: 100%;
		height: 34px;
		padding: 6px 12px;
		font-size: 14px;
		line-height: 1.42857143;
		color: #555;
		background-color: #fff;
		background-image: none;
		border: 1px solid #ccc;
		border-radius: 4px;
		-webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
		box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
		-webkit-transition: border-color ease-in-out .15s, -webkit-box-shadow ease-in-out .15s;
		-o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
		transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
	}

	.form-control:focus {
		border-color: #66afe9;
		outline: 0;
		-webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px rgba(102, 175, 233, .6);
		box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px rgba(102, 175, 233, .6);
	}

	.form-control::-moz-placeholder {
		color: #999;
		opacity: 1;
	}

	.form-control:-ms-input-placeholder {
		color: #999;
	}

	.form-control::-webkit-input-placeholder {
		color: #999;
	}

	.form-control::-ms-expand {
		background-color: transparent;
		border: 0;
	}

	.form-control[disabled],
	.form-control[readonly],
	fieldset[disabled] .form-control {
		background-color: #eee;
		opacity: 1;
	}

	.form-control[disabled],
	fieldset[disabled] .form-control {
		cursor: not-allowed;
	}

	textarea.form-control {
		height: auto;
	}

	input[type="search"] {
		-webkit-appearance: none;
	}

	@media screen and (-webkit-min-device-pixel-ratio: 0) {
		input[type="date"].form-control,
		input[type="time"].form-control,
		input[type="datetime-local"].form-control,
		input[type="month"].form-control {
			line-height: 34px;
		}
		input[type="date"].input-sm,
		input[type="time"].input-sm,
		input[type="datetime-local"].input-sm,
		input[type="month"].input-sm,
		.input-group-sm input[type="date"],
		.input-group-sm input[type="time"],
		.input-group-sm input[type="datetime-local"],
		.input-group-sm input[type="month"] {
			line-height: 30px;
		}
		input[type="date"].input-lg,
		input[type="time"].input-lg,
		input[type="datetime-local"].input-lg,
		input[type="month"].input-lg,
		.input-group-lg input[type="date"],
		.input-group-lg input[type="time"],
		.input-group-lg input[type="datetime-local"],
		.input-group-lg input[type="month"] {
			line-height: 46px;
		}
	}
	.pagination {
		display: inline-block;
		padding-left: 0;
		margin: 20px 0;
		border-radius: 4px;
	}

	.pagination>li {
		display: inline;
	}

	.pagination>li>a,
	.pagination>li>span {
		position: relative;
		float: left;
		padding: 6px 12px;
		margin-left: -1px;
		line-height: 1.42857143;
		color: #337ab7;
		text-decoration: none;
		background-color: #fff;
		border: 1px solid #ddd;
	}

	.pagination>li:first-child>a,
	.pagination>li:first-child>span {
		margin-left: 0;
		border-top-left-radius: 4px;
		border-bottom-left-radius: 4px;
	}

	.pagination>li:last-child>a,
	.pagination>li:last-child>span {
		border-top-right-radius: 4px;
		border-bottom-right-radius: 4px;
	}

	.pagination>li>a:hover,
	.pagination>li>span:hover,
	.pagination>li>a:focus,
	.pagination>li>span:focus {
		z-index: 2;
		color: #23527c;
		background-color: #eee;
		border-color: #ddd;
	}

	.pagination>.active>a,
	.pagination>.active>span,
	.pagination>.active>a:hover,
	.pagination>.active>span:hover,
	.pagination>.active>a:focus,
	.pagination>.active>span:focus {
		z-index: 3;
		color: #fff;
		cursor: default;
		background-color: #337ab7;
		border-color: #337ab7;
	}

	.pagination>.disabled>span,
	.pagination>.disabled>span:hover,
	.pagination>.disabled>span:focus,
	.pagination>.disabled>a,
	.pagination>.disabled>a:hover,
	.pagination>.disabled>a:focus {
		color: #777;
		cursor: not-allowed;
		background-color: #fff;
		border-color: #ddd;
	}

	.pagination-lg>li>a,
	.pagination-lg>li>span {
		padding: 10px 16px;
		font-size: 18px;
		line-height: 1.3333333;
	}

	.pagination-lg>li:first-child>a,
	.pagination-lg>li:first-child>span {
		border-top-left-radius: 6px;
		border-bottom-left-radius: 6px;
	}

	.pagination-lg>li:last-child>a,
	.pagination-lg>li:last-child>span {
		border-top-right-radius: 6px;
		border-bottom-right-radius: 6px;
	}

	.pagination-sm>li>a,
	.pagination-sm>li>span {
		padding: 5px 10px;
		font-size: 12px;
		line-height: 1.5;
	}

	.pagination-sm>li:first-child>a,
	.pagination-sm>li:first-child>span {
		border-top-left-radius: 3px;
		border-bottom-left-radius: 3px;
	}

	.pagination-sm>li:last-child>a,
	.pagination-sm>li:last-child>span {
		border-top-right-radius: 3px;
		border-bottom-right-radius: 3px;
	}
	.pagination>li>a{
		color: #333;
	}
	.pagination>.active>a, .pagination>.active>span, .pagination>.active>a:hover, .pagination>.active>span:hover, .pagination>.active>a:focus, .pagination>.active>span:focus {
		z-index: 3;
		color: #fff;
		cursor: default;
		background-color: #00a53c;
		border-color: #00a53c;
	}
</style>
