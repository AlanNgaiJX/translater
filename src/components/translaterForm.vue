<template>
  <!-- 表单组件 -->
  <div class="translaterForm">
    <form action="translaterForm_submit" method="get" accept-charset="utf-8" class="inline">

      <div class="form-group">
        <input type="text" name="" value="" placeholder="输入翻译内容（中文）" v-model="textIn" class="form-control text-center" v-on:keydown="keyboard">
      </div>

      <div class="row">
        
        <span class="col-sm-4 lh text-right">Chinese To :</span>
        <div class="form-group col-sm-4 ">
          <select name="" v-model="typeIn" class="form-control wmd">
            <option value="ZH_CN2EN">English</option>
            <option value="ZH_CN2JA">Japanese</option>
            <option value="ZH_CN2KR">Korean</option>
            <option value="ZH_CN2FR">French</option>
          </select>
        </div>

        <button type="button" @click.prevent="submit" class="btn btn-default col-sm-2 col-sm-offset-0 col-xs-4 col-xs-offset-4">翻译</button>

      </div>

    </form>

  </div>

</template>

<script>
export default {
  name: 'translaterForm',
  data () {
    return {
      // 双向数据绑定input输入框
      textIn:'',
      // 双向数据绑定select
      typeIn:'ZH_CN2EN'
    }
  },
  methods:{
    // 向父级触发submit事件、并传参
    submit:function(){
      this.$emit('submit',this.textIn,this.typeIn);
    },
    // 输入框绑定键盘事件，enter键触发submit()
    keyboard:function(e){
      if (e.keyCode == 13) {
      e.preventDefault();
      this.submit();
      this.textIn="";
      }      
    }
  },
  watch:{
    // 监听输入框变化，向父级触发事件，清除兄弟级translaterOutput的显示
    textIn:function(){
    this.$emit('clear_translated');
    }
  }
}
</script>

<style>
.wmd{
  /*width:30%;*/
  text-align: center;
  text-align-last: center;
}
.lh{
  line-height: 35px;
  /*margin-left: 30px;*/
}

/*.vmiddle {
 
   float: none;
 
   display: inline-block;
 
   vertical-align: middle;
 
   }*/
 </style>
