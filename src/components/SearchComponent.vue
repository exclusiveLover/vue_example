<template>
    <div class="search">
        <div class="container">
            <div class="form-group col-xs-12">
                <input type="email" v-model="select" class="form-control" id="exampleInputEmail1" placeholder="输入标签筛选留言，如：用户反馈">
                <button type="submit" class="btn btn-search glyphicon glyphicon-search" @click="$emit('updateSelect',select)"></button>
            </div>
        </div>
    </div>
</template>
<style scoped>
.search {
    padding: 20px 0;
    position: relative;
}

.search .btn-search {
    position: absolute;
    right: 15px;
    top: 0px;
}

</style>
<script>

    export default{
        data(){
            return{
                select:''
            }
        }
    }
</script>
