<template>
  <div id="app">
      <header-component></header-component>
      <form-component v-on:addItem="addItem"></form-component>
      <search-component v-on:updateSelect="updateSelect"></search-component>
      <detail-component v-for="(item, index) in detailListObj"
                        v-bind:item="item"
                        v-bind:select="select"
                        v-on:deleteItem="deleteItem(index)"
                        v-on:deleteTag="deleteTag"
                        v-on:updateValue="updateValue">
      </detail-component>
      <modal-component v-on:addTag="addTag"></modal-component>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import FormComponent from './components/FormComponent.vue'
import SearchComponent from './components/SearchComponent.vue'
import DetailComponent from './components/DetailComponent.vue'
import ModalComponent from './components/modalComponent.vue'

export default {
  name: 'app',
  data () {
    return {
        //通过value值监控正在操作标签的组件的index值
        value: 0,
        //通过select监控搜索的词条
        select:'',
        //使用localStorage来模拟数据库存储数据
        detailListObj: localStorage.detailList?JSON.parse(localStorage.detailList):[]
    }
  },
  methods: {
    //添加一条留言
    addItem: function(userName,content){
        var newObj = {
            "userName": userName,
            "content": content,
            "tags": [],
            "index":this.detailListObj.length
        }
        this.detailListObj.push(newObj);
        this.update(this.detailListObj);
    },
    //删除一条留言
    deleteItem: function(index){
        this.detailListObj.splice(index, 1);
        this.update(this.detailListObj);
    },
    //添加一条标签
    addTag: function(newTag){
        this.detailListObj[this.value].tags.push(newTag);
        this.update(this.detailListObj);
    },
    //删除一条标签
    deleteTag: function(tagIndex){
        this.detailListObj[this.value].tags.splice(tagIndex, 1);
        this.update(this.detailListObj);
    },
    //监控是哪一条留言在修改标签
    updateValue: function(newValue){
        this.value=newValue;
    },
    //监控搜索词条的变化
    updateSelect: function(newSelect){
        this.select=newSelect;
    },
    //将改动的数据同步到localStorage
    update: function(newObj){
        this.detailListObj=newObj;
        localStorage.detailList = JSON.stringify(this.detailListObj);
    }
  },
  components:{
     'header-component':HeaderComponent,
     'form-component':FormComponent,
     'search-component':SearchComponent,
     'detail-component':DetailComponent,
     'modal-component':ModalComponent
  }
}
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}

</style>
