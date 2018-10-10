<template>
	<div class="headerWrapper">
		<div class="top">
			<div class="avatar">
			  <img :src="seller.avatar" alt="头像" />
			</div>
			<div class="contentWrapper">
				<div class="title">
					<span class="icon"></span><span class="text">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}
				</div>
				<div class="supports">
					<img class="icon"  :src="supportIcon[type0]"></img><span class="text">{{seller.supports[0].description}}</span>
					
				</div>
			</div>
			<div  class="supportsMore">
				5个 >
			</div>
		</div>
		<div class="bottom">
			<span class="icon"></span>
			<span class="text">{{seller.bulletin}}</span>
			<span class="arrow"> ></span>
			
		</div>
		
		
	</div>
</template>

<script>
	export default{
		props:{
			seller:{
				type:Object
			}
		},
		data(){
			return {
				type0:0,
				supportIcon: ["decrease_1@2x.png","discount_1@2x.png","special_1@2x.png","invoice_1@2x.png","guarantee_2@2x.png"]
			}
			
		},
		created(){
			this.type0 = seller.supports[0].type
		},
		methods:{
			
		}
	}
</script>

<style >
	.headerWrapper{
		background-color:rgba(7,17,27,.5);
		color:#fff;
		
	}
   .top{
   	width:100%;
   	padding:24px 0 0 24px;
   	display:flex;
   	position:relative;
   }
   .top .avatar{
    flex:0 0 64px;
   	width:64px;
   	height:64px;
   	border-radius: 4px;
   	
   }
   .top .avatar img{
   	width:100%;
   	height:100%;
   	border-radius: 4px;
   }
   .title .icon{
   	
   }
   .top .contentWrapper {
   	flex:1 0 auto;
   	padding-left:16px;
   }
   .supports .icon{
   	display:inline-block;
   	width:12px;
   	height:12px;
   	background:url("./decrease_1@2x.png") no-repeat center;
   	background-size: 12px 12px;
   	vertical-align: middle;
   }
    .supports  .text{
    	font-size:12px;
    	padding-left:6px;
    }
  .supportsMore{
  	position:absolute;
  	bottom:0;
  	right:34px;
  	padding: 0 16px;
  	height:24px;
  	line-height: 24px;
  	font-size:20px;
  	background-color:rgba(0,0,0,.2);
  	text-align:center;
  	border-radius: 12px;
  }
  .bottom{
  	box-sizing: border-box;
  	width:100%;
  	padding:12px;
  	display:flex;
  }
  .bottom .icon{
  	display:inline-block;
  	width:22px;
  	background:url(./bulletin@2x.png) no-repeat center;
  	background-size:100%;
  	
  }
   .bottom  .text{
   		display:inline-block;
   	text-overflow: ellipsis;
   	font-size:12px;
   }
   .bottom .arrow{
   		display:inline-block;
   }
	  
</style>