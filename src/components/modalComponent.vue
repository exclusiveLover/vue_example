<template>
    <div role="dialog" class="modal fade bs-example-modal-sm" id="layer">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                    <div class="form-group">
                        <label for="exampleInputEmail1">添加标签</label>
                        <input type="email" v-model="newTag" class="form-control" id="exampleInputEmail1">
                    </div>
                </div>
                <div class="modal-body text-right">
                    <button data-dismiss="modal" class="btn btn-primary btn-sm">取消</button>
                    <button data-dismiss="modal" class="btn btn-danger btn-sm" @click="addTag">确认</button>
                </div>
            </div>
        </div>
    </div>
</template>
<style>

</style>
<script>
    export default{
        props:["index"],
        data(){
            return{
                newTag:''
            }
        },
        methods: {
            addTag: function(){
                this.$emit("addTag",this.newTag);
                this.newTag='';
            }
        }
    }
</script>
