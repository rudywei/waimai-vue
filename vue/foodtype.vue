<template>
	<div id="shop">
		<div class="m-result" style="float: left;">
			<ul id="showgoods">
				<li class="goods" v-for="item in list">
					<div class="goodswrap promotion">
						<a href="#">
							<div class="img">
								<img :src="host+item.fphoto">
							</div>
						</a>
						<div class="desc clearfix">
							<p class="price"> <span class="cur"><i>¥</i>{{item.fprice}}</span> </p>
							<div class="titlewrap">
								<a class="title" href="#">
									<h4>{{item.fname}}</h4>
									<h4>{{item.finfo}}</h4>
								</a>
							</div>
							<a href="#" class="addcart" title="gid">
								<button class="btn btn-danger glyphicon glyphicon-shopping-cart" style="font-size: 18px;">加入购物车</button>
							</a>
						</div>
					</div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	export default {
		created() {
           this.getList();
		},
		data() {
			return {
				list: [],
				tid:this.$route.query.id,
				host: "http://localhost/images/",
			}
		},
		methods: {
			getList() {
				axios.post('http://localhost/food/findByTid/'+this.tid)
					.then(res => {
						this.list = res.data;
						
					})
					.catch(err => {
						console.error('获取数据失败' + err);
					})
			}
		}
	}
</script>

<style scoped="scoped">
	#shop {
		height: 100%;
		width: 100%;
		background-color: azure;
		text-align: center;
		border-radius: 5px;
		float: left;
	}
	
	ul {
		list-style: none;
	}
	
	.m-result {
		width: 1200px;
		margin-bottom: 6px;
		margin-left: -37px;
		margin-top: 10px;
	}
	
	.m-result .goods {
		position: relative;
		float: left;
		width: 262px;
		height: 387px;
		margin: 0 7px 14px;
		_margin: 0 6px 14px;
		background-color: #fff;
		font-size: 12px
	}
	
	.m-result .goodswrap {
		position: absolute;
		width: 262px;
		background-color: #fff;
		border: 1px solid #f3f3f3;
		border-bottom: none
	}
	
	.m-result .goods .img {
		position: relative
	}
	
	.m-result .goods a {
		display: block;
		color: #333
	}
	
	.m-result .img img {
		transition: transform 0.5s;
		display: block;
		width: 260px;
		height: 257px;
		padding: 12px 12px 10px
	}
	
	.m-result .img img:hover {
		transform: scale(1.1);
	}
	
	.m-result .goods .desc {
		width: 234px;
		padding: 0 14px 11px
	}
	
	.m-result .goods .title {
		height: 40px;
		margin-top: 5px;
		overflow: hidden;
		font-size: 13px;
		line-height: 20px;
		word-wrap: break-word;
		word-break: break-all
	}
	
	.m-result .title:hover {
		color: #e31436
	}
	
	.m-result .goods .price {
		height: 20px;
		color: #e31436;
		overflow: hidden;
		font-size: 0
	}
	
	.m-result .price .cur {
		display: inline-block;
		margin-right: 2px;
		font-weight: 700;
		font-size: 22px;
		line-height: 24px
	}
	
	.m-result .price i {
		font-size: 12px;
		font-weight: 700
	}
	
	.m-result .goods:hover .title {
		min-height: 40px;
		height: auto
	}
	
	.m-result .goods:hover {
		z-index: 99;
		*zoom: 1
	}
	
	.m-result .goods:hover .goodswrap {
		border: 1px solid #e31436;
		box-shadow: 1px 2px 3px rgba(0, 0, 0, .2)
	}
	
	.m-result .addcart:hover {
		color: #e31436
	}
</style>