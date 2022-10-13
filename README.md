
#Waring 注意
前端组件仅为部分，其主要目的是分享各类案例，更多组件请前往我的主页查看更多的前端开源项目内容，部分开源涵盖了市场主流的语言。

# VueComponents
基于Vue的自定义组件集合可任意组合修改 - VueComponents

# 使用方法 Usage method
## 在Vue3中main.js内加入以下代码片段
``` js
import AlertMsg from '@/components/AlertMsg/AlertMsg.vue'
import VHSelect from '@/components/VH-Select/VH-Select.vue'

app.component("AlertMsg",AlertMsg)
app.component("VHSelect",VHSelect)
```
# Alert提示组件使用方法 Alert component usage method
## 在模版中使用方法

### HTML代码片段
``` html
<template>
  <AlertMsg ref="AlertMsg"></AlertMsg>
</template>
```
### Js代码片段
``` js
this.$refs.AlertMsg.addMsg(1,"测试提示")
```
其中参数一是为提示类型：1为成功、2为错误、3为警告    
参数二是提示的内容

# Select选择器组件使用方法 Select component usage method
## 在模版中使用方法

### HTML代码片段
``` html
<VH-Select width="120px" @change="onClick" v-model="select" :curData="curData" :itemData="itemData" label="item" vh-key="m"></VH-Select>
```
参数介绍：width（宽度设置，默认为120px） @change（选择触发器，返回对应的vh-key对应键值） v-model（接收返回的参数vh-key对应的键值）    
curData （返回选择的label名称） itemData（选择器内部选择数据） label（选择器选项的名称） vh-key（选择器选择返回的指定键值参数）

### Js代码片段
``` js
export default {
	data() {
		return {
			select:'',
			curData: '选项1',
			itemData: [{m:'m1',item:'选项1',key:2},{m:'m2',item:'选项2',key:4},{m:'m3',item:'选项3',key:6},{m:'m4',item:'选项4',key:8},
			{m:'m5',item:'选项5',key:10},{m:'m6',item:'选项6',key:12},{m:'m7',item:'选项7',key:14},{m:'m8',item:'选项8',key:16}],
		}
	},
	watch: {
		select(n,o){
			console.log(this.select)
		}
	},
  methods: {
		onClick(e) {
		   console.log(e)
    },
  }
}
```

