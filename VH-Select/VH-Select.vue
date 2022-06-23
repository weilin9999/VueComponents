<template>
	<div :style="[isShow ? 'border: 1px solid #409eff;':'','width: '+width+'px;']" class="vh-dropdown">
		<div class="cur-name" @click="timeOutClose"><p>{{current}}</p> <span :class="isShow ? 'onSelect iconfont icon-xiangshang2':'driSelect iconfont icon-31xiala'"></span> </div>
		<div :class="[isShow?'on':'',isopen ? 'list-and-search openSelect':'list-and-search disSelect']">
			<div class="squerSpen"></div>
			<div class="search-module clearfix" v-show="isNeedSearch">
				<input class="search-text" @input='search' :placeholder="placeholder" />
			</div>
			<ul class="list-module">
				<li :title="labelFunc(item)" v-for ="(item,index) in datalist" @click="clickItem(item)" :key="index">
					<span class="list-item-text">{{labelFunc(item)}}</span>
				</li>
			</ul>
			<div class="tip-nodata" v-show="searchValue.length && !datalist.length">未找到数据</div>
		</div>
	</div>
</template>
 
<script>
 export default {
  name:"VH-Select",
  data(){
		return {
			isopen:false,
			searchValue: '',
			current: this.curData,
			datalist:[],
			isShow:false
		}
  },
  props:{
		modelValue:null,
		label:null,
		vhKey:null,
		curData:String,
		itemData:Array,
		isNeedSearch:{
			type: Boolean,
			default: true
		},
		placeholder:{
			type: String,
			default: '搜索' 
		},
		width:{
			type: String,
			default: '150' 
		},
  },
  created(){
		this.datalist = this.itemData;
		document.addEventListener('click', (e) => {
			if (!this.$el.contains(e.target)){
				this.isopen = false;
				setTimeout(()=>{this.isShow = false},100)
			}
		}, false)
  },
  methods:{
		labelFunc(item){
			return item[this.label]
		},
		search(e){
			this.searchValue = e.target.value;
			this.datalist = this.itemData.filter((item)=>{
				return item[this.label].indexOf(this.searchValue) != -1;
			});
		},
		clickItem(item){
			this.isShow = false;
			let value = item[this.label]
			let key = item[this.vhKey]
			this.current = value;
			this.$emit('change',key);
			this.$emit('update:modelValue',key);
		},
		timeOutClose(){
			if(this.isShow == false){
				this.isopen = true;
				this.isShow = true;
			}else{
				this.isopen = false;
				setTimeout(()=>{this.isShow = false},100)
			}
		},
	}
}
</script>
 
<style scoped>
	*{
		margin: 0;
		padding: 0;
	}
	.vh-dropdown {
		z-index:10;
        background-color: #fff;
		cursor: pointer;
		user-select:none;
		-webkit-user-select:none; 
		position: relative;
		border-radius: 4px;
		border: 1px solid #dcdfe6 ;
		display: flex;
		flex-direction: column;
  		align-items: center;
	}
	.vh-dropdown:hover{
		border: 1px solid #409eff;
	}
    input::-webkit-input-placeholder{
		font-size: 14px;
	}
    .list-module {
        max-height: 200px;
		width: 100%;
        overflow-y: auto;
		border-bottom-left-radius: 8px;
		border-bottom-right-radius: 8px;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 5px 0;
    }
	
	.list-module::-webkit-scrollbar {
		width:3px;
	}
	
	.list-module::-webkit-scrollbar-track {
		-webkit-box-shadow:inset006pxrgba(0,0,0,0.3);
		border-radius:10px;
	}
	
	.list-module::-webkit-scrollbar-thumb {
		border-radius:10px;
		background:rgba(0,0,0,0.1);
		-webkit-box-shadow:inset006pxrgba(0,0,0,0.5);
	}

    li {
		border-radius: 5px;
		width: 80%;
		height: 55px;
		list-style: none;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 5px;
		text-align: center;
    }
    li:hover {
        cursor:pointer;
        color: #fff;
        background: #d9ecff;
    }
	.list-item-text{
		width: 100%;
		color: #606266;
		overflow: hidden;
		text-overflow:ellipsis;
		white-space: nowrap
	}
    ._self-show {
		display: block!important;
	}
    .search-module {
        position: relative;
    }
    .search-text {
        width: 100%;
        height: 30px;
        padding: 0 10px;
        box-shadow: none;
        outline: none;
        border: none;
        box-sizing:border-box;
        -moz-box-sizing:border-box;
        -webkit-box-sizing:border-box;
		text-align: center;
		border-bottom: 1px solid #ccc;
		border-top-left-radius: 8px;
		border-top-right-radius: 8px;
    }
	.search-text:hover{
		border-bottom: 1px solid #409eff;
	}
    .search-icon {
        position: absolute;
        top: 24%;
        right: 0.5em;
        color: #aaa;
    }
	.list-and-search{
		display: none;
		background: #fff;
		border: 1px solid #e4e7ed;
		position: absolute;
		width: 100%;
		border-radius: 8px;
		margin-top: 50px;
		box-shadow: 0px 0px 12px rgba(0, 0, 0, .12)
	}

	.squerSpen{
		position: absolute;
		top: -20px;
		border-right: 10px solid transparent;
        border-top: 10px solid transparent;
        border-left: 10px solid transparent;
        border-bottom: 10px solid #fff;
	}

    .on{
        display: flex;
		flex-direction: column;
		align-items: center;
    }

	.cur-name{
        width: 100%;
		height: 32px;
		line-height: 32px;
		position: relative;
		color: #a8abb2;
		box-sizing: border-box;
		-moz-box-sizing:border-box;
        -webkit-box-sizing:border-box;
   		padding: 0px 10px;
		display: flex;
    	justify-content: space-between;
	}
	.cur-name p{
		overflow: hidden;
		text-overflow:ellipsis;
		white-space: nowrap
	}
	.tip-nodata {
		font-size: 14px;
		padding: 10px;
	}
	.openSelect{
		animation: openDiv 0.2s ease-in;
	}
	.disSelect{
		animation: disDiv 0.2s ease-out;
	}
	.onSelect{
		animation: onClick 0.2s ease-out;
	}
	.driSelect{
		animation: disClick 0.2s ease-out;
	}
	@keyframes openDiv {
		0%{
			opacity: 0;
			
		}
		100%{
			opacity: 1;
		}
	}
	@keyframes disDiv {
		0%{
			opacity: 1;
			
		}
		100%{
			opacity: 0;
		}
	}
	@keyframes onClick {
		0%{
			transform: rotate(0deg);
			
		}
		100%{
			transform: rotate(360deg);
		}
	}
	@keyframes disClick {
		0%{
			transform: rotate(180deg);
			
		}
		100%{
			transform: rotate(0deg);
		}
	}
</style>