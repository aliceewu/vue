<template>
<div class="mui-numbox" data-numbox-min='1' style="height:25px;">
		<button class="mui-btn mui-btn-numbox-minus" type="button">-</button>
		<input id="test" class="mui-input-numbox" type="number" :value="initcount"  @change="countChanged" ref="numbox" readonly=""/>
		<button class="mui-btn mui-btn-numbox-plus" type="button">+</button>
	</div>

	<!-- 分析： 子组件什么时候把 数据传递给父组件 -->
 
</template>

<script>
	import mui from "../../lib/mui/js/mui.min.js"
	
	export default{
		mounted() {
			mui(".mui-numbox").numbox();
		},
		methods:{
			countChanged(){
				//数量改变了
				  // 每当数量值改变，则立即把最新的数量同步到 购物车的  store 中，覆盖之前的数量值
				console.log(this.$refs.numbox.value);
				this.$store.commit("updateGoodsInfo",{
					id:this.goodsid,
					count:this.$refs.numbox.value
					
				});
				
			}
		},
		props:['initcount', 'goodsid'],
		// watch:{
		// 	// 属性监听
		// 	'initcount':function(newVal,o	ldVal){
		// 		 // 使用 JS API 设置 numbox 的最大值 
		// 		 mui(".mui-numbox").numbox().setOption("initcount",newVal);
		// 	}
		// }
	
	};
</script>

<style>
</style>
