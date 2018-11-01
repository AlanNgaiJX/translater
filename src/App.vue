<template>
  <div id="app">
    <div class="container">
      <!-- 标题 -->
      <h1 class="text-center">林家翻译</h1>
      <h4 class="text-center text-muted">列表翻译 / 随心所译</h4>
      <!-- 表单模块 -->

      <div class="row mt">
        <translaterForm @submit="translateIt" @clear_translated="clear_translated" class="col-xs-6 col-xs-offset-3 "></translaterForm>
      </div>

      <!-- 表格模块 -->
      <div class="row">
        <translaterOutput :translated="translated" :makeList="makeList" class="col-xs-10 col-xs-offset-1 col-sm-6 col-sm-offset-3"></translaterOutput>  
      </div>
    </div>
  </div>

</template>

<script>
  import translaterForm from './components/translaterForm'
  import translaterOutput from './components/translaterOutput'

  export default {
    name: 'App',
    components: {
      // 表单组件
      translaterForm,
      // 表格组件
      translaterOutput
    },
    data(){
      return{
        // 贮存翻译结果
        translated:'',
        // 贮存翻译列表
        makeList:[]
      }
    },
  methods:{
    // 异步请求API获取结果、贮存结果（由子组件translaterForm触发并传参）
    translateIt:function(textIn,typeIn){
      this.$axios.get("/apis/translate?doctype=json&type="+typeIn+"&i="+textIn)
      .then(res=>{
        //获取翻译值赋予translated
        // console.log(res.data.translateResult[0][0].tgt);
        this.translated=res.data.translateResult[0][0].tgt;
        this.makeList.push({"textIn":textIn,"translated":this.translated});
      })
      .catch(error=>{
        console.log("error");
      });
    },
    // 清空列表以清空表格（由子组件translaterForm触发）
    clear:function(){
      this.makeList=[];
    },
    // 清空翻译结果贮存（由子组件translaterOutput触发）
    clear_translated:function(){
      this.translated = '';
    }
  }
}
</script>

<style>
.mt{
  padding-top: 20px;
}
</style>
