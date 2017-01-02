<template>
    <div class="form">
        <div class="container">
            <div class="form-group col-xs-8">
                <input type="email" ref="userName" class="form-control userName" placeholder="请输入昵称">
            </div>
            <div class="form-group col-xs-12">
                <textarea ref="content" class="form-control content" maxlength="300" rows="4" style="resize:none"
                          placeholder="请输入留言内容，不超过300字" @keyup="getNum"></textarea>
                <span>{{num}}/300</span>
                <button class="btn btn-primary" @click="addItem">发布</button>
            </div>
        </div>
    </div>
</template>
<style>
.form {
    padding-top: 20px;
    padding-bottom: 40px;
    background: url("../assets/bgi.jpg");
}

.form span {
    position: absolute;
    left: 30px;
    bottom: 10px;
}

.form button {
    position: absolute;
    right: 30px;
    bottom: 10px;
}

</style>
<script>

    export default{
        data(){
            return{
                num:0,
                userName:'',
                content:''
            }
        },
        methods:{
            getNum: function(event){
                this.num = event.target.value.toString().length;
            },
            addItem: function(){
                //console.log(newDetail);
                this.$emit('addItem',this.$refs.userName.value,this.$refs.content.value);
                userName: this.$refs.userName.value='';
                content: this.$refs.content.value='';
                this.num=0;
            }
        }
    }

</script>
