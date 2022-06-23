<template>
    <div class="empty-box">
        <span class="bigBox iconfont icon-box-empty"></span>
        <p>{{description}}</p>
    </div>
</template>

<script>
export default {
    name: 'VH-Empty',
    data () {
        return {
            
        }
    },
    props:{
        description:{
            type: String,
            default:'空的哦'
        }
    },
    methods:{
        
    },
}
</script>

<style  scoped>
*{
    margin: 0;
    padding: 0;
}
.empty-box{
    width: 100%;
    height: 210px;
    display: flex;
    flex-direction: column;
    align-items: center;
    user-select: none;
}
.bigBox{
    font-size: 200px;
    color: #e5e7e9;
}
.empty-box p{
    color: #909399;
}
</style>
