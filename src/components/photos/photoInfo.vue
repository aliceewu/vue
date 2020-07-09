<template>
	<div class="photoinfo-container">
		<!-- 大标题 -->
		<h3 class="title">{{photoinfo.title}}</h3>
		<!-- 子标题 -->
		<p class='subtitle'>
			<span>发表时间:{{photoinfo.add_time|dataFormat}}</span>
			<span>点击:{{photoinfo.click}}次</span>
		</p>
		<hr />
		<!-- 缩略图区域 -->
		<div class="thumbs">
			<vue-preview :slides="list" class="preview" @close="handleClose"></vue-preview>
			<!-- <img class="preview-img" v-for="(item, index) in list" :src="item.src" height="100" @click="$preview.open(index, list)" :key="item.src"> -->
		</div>
		<!-- 图片内容区域 -->
		<div class="content" v-html="photoinfo.content"></div>

		<!-- 放置一个现成的 评论子组件 -->
		<cmt-box :id="id"></cmt-box>
	</div>
</template>

<script>
	//1.导入评论子组件
	import comment from '../subcomponents/comment.vue'

	export default {
		data() {
			return {
				id: this.$route.params.id, //从路由中获取到的图片Id
				photoinfo: {}, //图片详情
				list: [] //缩略图的数组
			}
		},
		created() {
			this.getImageInfo();
			this.getThumbs();
		},
		methods: {
			getImageInfo() {
				//获取图片的详情
				this.$http.get('api/getimageInfo/' + this.id).then(result => {
					if (result.body.status === 0) {
						this.photoinfo = result.body.message[0];
					}
				})
			},
			handleClose() {
				console.log('close event')
			},
			getThumbs() {
				//获取缩略图
				this.$http.get('api/getthumimages/' + this.id).then(result => {
					if (result.body.status === 0) {
						console.log(result.body);
						//循环每个图片数据，补全宽和高
						result.body.message.forEach(item => {
							item.w = 600; //设置以大图浏览时的宽度
							item.h = 400; //设置以大图浏览时的高度
							item.src = item.src; //大图
							item.msrc = item.src; //小图
						});

						this.list = result.body.message;

					}
				})
			}
		},
		components: { //注册评论子组件
			'cmt-box': comment
		}
	}
</script>

<style lang="scss" scoped>
	.photoinfo-container {
		padding: 3px;

		.title {
			font-size: 14px;
			text-align: center;
			color: #23A2ff;
			margin: 15px;
		}

		.subtitle {
			font-size: 12px;
			display: flex;
			justify-content: space-between;
		}

		.content {
			font-size: 10px;
			line-height: 30px;
			clear: both;
		}

		.thumbs {
			img {
				margin: 10px;
				box-shadow: 0 0 8px #999;
			}
		}

	}
</style>
