<template>
    <li class="detail" v-show="show">
        <div class="container">
            <div class="clearfix">
                <p class="col-xs-10">{{item.userName}}：{{item.content}}</p>
                <span class="glyphicon glyphicon-trash col-xs-1 deleteItem" @click="$emit('deleteItem')"></span>
            </div>
            <div class="tagList">
                <div class="tag col-xs-3" v-for="(tag,tagIndex) in item.tags">{{tag}}<span class="glyphicon glyphicon-remove deleteTag pull-right" @click="deleteTag(tagIndex)"></span></div>
                <div class="addTag pull-left glyphicon glyphicon-plus" data-toggle="modal" data-target="#layer" @click="$emit('updateValue',index)"></div>
            </div>
            <input type="hidden" v-model="index"/>
            <hr class="col-xs-12"/>
        </div>
    </li>
</template>
<style>
.detail {
    padding: 20px;
}

li {
    list-style: none;
}

.detail .tagList {
    padding: 0 12px;
}

.detail .deleteItem {
    cursor: pointer;
}

.detail .tag {
    text-align: center;
    border: 1px solid #ccc;
    margin-top: 20px;
    margin-bottom: 20px;
}

.detail .tag .deleteTag {
    cursor: pointer;
}

.detail .addTag {
    margin: 20px 0;
    cursor: pointer;
}
</style>
<script>

    export default{
        props: ["item","select"],
        data(){
            return{
                index:this.item.index
            }
        },
        computed: {
            show: function(){
                if(this.select===''||this.item.tags.indexOf(this.select)!=-1){
                    return true;
                }else{
                    return false;
                }
            }
        },
        methods: {
            deleteTag: function(tagIndex){
                this.$emit('updateValue',this.index);
                this.$emit('deleteTag',tagIndex);
            },

        }
    }
</script>
