<template>
  <el-container>
    <el-header>
      <entity-view 
        @bucket-selected="((data)=>{ onSetBucket(data); })"
        @entity-selected="((data)=>{ onSetEntity(data); })"></entity-view>
    </el-header>
    <el-main style="padding-top:5px;">
        <tsdb-view :bucket="bucket" :entity="entity"></tsdb-view>
    </el-main>
  </el-container>
</template>

<script>
import TsdbView from './TsdbView.vue'
import EntityView from './EntityView.vue'
export default {
  components: { TsdbView, EntityView },
  name: 'MainView',
  props: {
    global: Object
  },
  data(){
    return {
      entity: null,
      bucket: null
    }
  },
  methods: {
    //选择的bucket定义
    onSetBucket(data){
      this.bucket = data;
    },
    //选择的实体
    onSetEntity(data){
      this.entity = data;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .el-container{
    height:calc(100vh - 80px);
  }
  .el-header{
    line-height: 60px;
  }
</style>
