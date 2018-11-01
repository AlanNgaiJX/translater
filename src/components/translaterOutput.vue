<template>	
  <div class="translaterOutput" >

  	<div class="row">
  		<span class="translated center-block text-center text-danger bg-warning ">{{translated}}</span>
  	</div>
   	
   	<div class="row">
	   	<table class="table table-condensed table-striped table-hover">
	   		<!-- <caption class="text-center">单词表</caption> -->
	   		<tbody>
	   			<tr v-for="(item,index) in makeList" class="row">
	   				<td class="col-xs-2">{{index | double_unit}}</td>
	   				<td class="col-xs-5">{{item.translated}}</td>
	   				<td class="col-xs-5">{{item.textIn}}</td>
	   			</tr>
	   		</tbody>
	   	</table>   		
   	</div>

<!-- http://www.cnblogs.com/fanyang1/p/9414088.html -->
   	<button @click="clear" class="btn btn-default">清空</button>
	<button type="button" class="btn btn-default">生成每日单词</button>
  </div>
</template>

<script>
export default {
  name: 'translaterOutput',
  data () {
    return {
     
    }
  },
  props:{
  	// 父传参数，翻译结果
  	 translated:{
  	 	type:String,
  	 	default:''
  	 },
  	 // 父传参数，翻译结果列表
  	 makeList:{
  	 	type:Array,
  	 	default:[]
  	 }
  },
  methods:{
  	// 调用父级clear清空列表
  	clear:function(){
  		this.$parent.clear();
  	}
  },
  fillter:{
  	double_unit:function(index){
  		index+=1;
  		// if (index<10) {
  		// 	return "0"+index;
  		// }
  		return "nmb";
  	}
  }
 
 
}
</script>

<style>
  .translated{
  	display: block;
  	font-size: 20px;
  	font-weight: bold;
  	height: 40px;
  	line-height: 40px;
  }
</style>
