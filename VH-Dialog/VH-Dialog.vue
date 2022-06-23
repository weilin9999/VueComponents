<template>
    <div class="dialog-box">
        <div class="black-box" @click="close"></div>
        <div :style="'width:'+width+'px;height:'+height+'px;'" class="dialog">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'VH-Dialog',
    data () {
        return {
            
        }
    },
    props:{
        width:{
			type: String,
			default: '800' 
		},
        height:{
			type: String,
			default: '460' 
		},
    },
    methods:{
        close(){
            this.$emit('close',true)
        }
    },
}
</script>

<style  scoped>
*{
    margin: 0;
    padding: 0;
}
.dialog-box{
    position: fixed;
    width: 100%;
    height: 100%;
    z-index: 200;
    display: flex;
    justify-content: center;
    align-items: center;
}
.black-box{
    position: fixed;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 201;
}
.dialog-box .dialog{
    background-color: #fff;
    border-radius: 8px;
    z-index: 202;
}
</style>
