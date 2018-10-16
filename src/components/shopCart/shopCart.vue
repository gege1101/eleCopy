<template>
	<div class="shopcart-wrapper">
		<div class="left">
			<div class="icon-left">
				<div class="icon-wrapper">
					<div class="icon-text icon-active">购物车</div>
					<div class="icon-count">12</div>
				</div>
			</div>
			<div class="price-middle">
				<div class="price">￥0</div>
				<div class="deliver">另需配送费￥{{seller.deliveryPrice}}元</div>
			</div>
		</div>
		
		<div class="send-right">￥{{seller.minPrice}}起送</div>
		
	</div>
	
</template>

<script>
	export default{
		props:{
			seller:{
				type:Object,
			}
		},
		data(){
			return {
				
			}
		},
		created(){
			console.log(this.seller)
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
 @import "../../common/stylus/index.styl"
 
     *{
     	box-sizing:border-box;
     }
	.shopcart-wrapper{
		position:fixed;
		bottom:0;
		left:0;
		width:100%;
		height:46px;
		background-color: #141d27;
		display:flex;
		.left{
			flex:1;
			.icon-left{
			padding:0 12px;
			width:82px;
			height:100%;
			.icon-wrapper{
				position:absolute;
				top:-12px;
				left:12px;
				width:58px;
				height:58px;
				border-radius:50%;
				background-color:#141d27;
				padding:6px;
				.icon-text{
					width:44px;
					height:44px;
					border-radius:50%;
					background-color: #2B343C;
					font-size:10px;
					color:#fff;
					text-align:center;
					line-height:44px;
					}
				.icon-active{
					background-color: #00A0DC;
				}
				.icon-count{
					    position: absolute;
					    top: 3px;
					    right: -3px;
					    padding: 0 6px;
					    height: 16px;
					    line-height: 16px;
					    color: #fff;
					    background-color: #f00;
					    text-align: center;
					    border-radius: 16px;
				}
					
					
				}
			}
			.price-middle{
				position:absolute;
				left:82px;
				top:0;
				height:100%;
				padding:12px 0;
				font-size:0;
				color:#ccc;
				.price{
					display:inline-block;
					font-size:14px;
					font-weight:700;
					padding-right:12px;
					border-right:1px solid rgba(255,255,255,.1);
					height:100%;
					
				}
				.deliver{
					display:inline-block;
					font-size:10px;
					height:100%;
					padding-left:6px;
				}
			}
		}
		.send-right{
			flex:0 0 105px;
			width:105px;
			background-color: #2B333B;
			text-align:center;
		    height:46px;
		    line-height:46px;
		    color:rgba(255,255,255,.4);
		    font-weight:700;
		}
		
	}
	
</style>