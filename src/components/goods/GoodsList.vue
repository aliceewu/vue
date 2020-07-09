<template>
	<div class="goods-list">
		<router-link class="goods-item" v-for="item in goodslist" :key="item.id" :to="'/home/goodsinfo/'+item.id" tag="div">
			<img :src="item.img_url" />
			<h1 class="title">{{item.title}}</h1>
			<div class="info">
				<p class="price">
					<span class="now">￥{{item.sell_price}}</span>
					<span class="old">￥{{item.market_price}}</span>
				</p>
				<p class="sell">
					<span>热卖中</span>
					<span>剩{{item.stock_quantity}}件</span>
				</p>
			</div>
		</router-link>
		<mt-button type="danger" size="large" @click="getMore">加载更多</mt-button>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				pageindex:1,//默认展示第一页数据
				goodslist:[]
			}
		},
		created() {
			this.getGoods();
		},
		methods:{
			getGoods(){
				// 获取商品列表数据
				this.$http.get("api/getgoods?pageindex="+this.pageIndex).then(result=>{
					if(result.body.status === 0){
						this.goodslist = this.goodslist.concat(result.body.message);
					}
				})
			},
			getMore(){
				this.pageindex++;
				this.getGoods();
			},
			// goDetail(id) {
			//   // 使用JS的形式进行路由导航
			
			//   // 注意： 一定要区分 this.$route 和 this.$router 这两个对象，
			//   // 其中： this.$route 是路由【参数对象】，所有路由中的参数， params, query 都属于它
			//   // 其中： this.$router 是一个路由【导航对象】，用它 可以方便的 使用 JS 代码，实现路由的 前进、后退、 跳转到新的 URL 地址
			
			//   console.log(this);
			//   // 1. 最简单的 
			//   // this.$router.push("/home/goodsinfo/" + id);
			//   // 2. 传递对象
			//   // this.$router.push({ path: "/home/goodsinfo/" + id });
			//   // 3. 传递命名 的路由
			//   this.$router.push({ name: "goodsinfo", params: { id } });
			// }
		}
	}
</script>

<style lang="scss" scoped>
	.goods-list {
		display: flex;
		flex-wrap: wrap;
		padding: 7px;
		justify-content: space-between;

		.goods-item {
			width: 49%;
			border: 1px solid #ccc;
			box-shadow: 0 0 8px #ccc;
			margin: 4px 0;
            padding: 2px;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			min-height: 293px; 
			img {
				width: 100%;
			}

			.title {
				font-size: 14px;
			}

			.info {
				background-color: #eee;
				p{
					margin: 0;
					padding: 5px;
				}
				.price {
					
					.now {
						color: red;
						font-size: 16px;
						font-weight: bold;
						
					}
					.old {
						text-decoration: line-through;
                         font-size: 12px;
						 margin-left: 10px;
					}

				}
				.sell{
					font-size: 13px;
					display: flex;
					justify-content: space-between;
				}
			}

		}

	}
</style>
