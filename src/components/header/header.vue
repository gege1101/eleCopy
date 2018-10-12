<template>
	<div class="wrapper">
		<div class="headerWrapper">
			<div class="top">
				<div class="avatar">
				  <img :src="seller.avatar" alt="头像" />
				</div>
				<div class="contentWrapper">
					<div class="title">
						<span class="icon"></span><span class="text" >{{seller.name}}</span>
					</div>
					<div class="description">
						{{seller.description}}
					</div>
					<div class="supports">
						<span class="icon"  :class="classMap[seller.supports[0].type]"></span><span class="text">{{seller.supports[0].description}}</span>
						
					</div>
				</div>
				<div  class="supportsMore" @click="showSupports()">
					{{seller.supports.length}}个 >
				</div>
			</div>
			
			<div class="bottom"  @click="showSupports()" >
				<span class="icon"></span>
				<span class="text" >{{seller.bulletin}}</span>
				<span class="arrow"> ></span>
			</div>
			
			<div class="bgimg">
				<img :src="seller.avatar"  alt="" width="100%" height="100%"/>
			</div>
	    </div>
		<div  class="supportsMoremodel" v-show="isShowSupport">
			<div class="mainContent">
				   <div class="title">{{seller.name}}</div>
				     <div class="item">
				     	<div class="item-title">
				     		<div class="line"></div>
				     		<div class="item-name">优惠信息</div>
				     		<div class="line"></div>
				     	</div>
				     	<ul class="supports-wrapper">
				     		<li class="support-item" v-for="suppport in seller.supports"><span class="icon" :class="classMap[suppport.type]"></span><span>{{suppport.description}}</span></li>
				     	</ul>
				     </div>
				     <div class="item">
				     	<div class="item-title">
				     		<div class="line"></div>
				     		<div class="item-name">商家公告</div>
				     		<div class="line"></div>
				     	</div>
				     	<div class="bulletintext">
				     		{{seller.bulletin}}
				     		{{seller.bulletin}}
				     		{{seller.bulletin}}
				     		{{seller.bulletin}}
				     		{{seller.bulletin}}
				     		
				     	</div>
				     </div>
			</div>
			<div class="stickerclose" @click="showSupports()">X</div>
		  
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
				classMap:["decrease","discount","special","invoice","guarantee"],
				isShowSupport:false,
			}
			
		},
		created(){
			this.type0 = seller.supports[0].type
		},
		
		methods:{
			showSupports(){
				this.isShowSupport = !this.isShowSupport ;
				
			}
			
		}
	}
</script>

<style >
	.wrapper{
		position:absolute;
		top:0;
		left:0;
		width:100%;
		height:100%;
		overflow:auto;
	}
	.headerWrapper{
		background-color:rgba(7,17,27,.5);
		color:#fff;
		position:relative;
		overflow: hidden;
		
	}
	.bgimg{
		position:absolute;
		top:0;
		left:0;
		z-index:-1;
		width: 100%;
        height: 100%;
		filter: blur(10px);
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
   /*//	background:url("./decrease_1@2x.png") no-repeat center;*/
   	background-size: 12px 12px;
   	background-repeat:no-repeat;
   	vertical-align: middle;
   }
  .decrease{
   	background-image: url(./decrease_1@2x.png);
   }
    .discount{
   	background-image: url(./discount_1@2x.png);
   }
    .special{
   	background-image: url(./special_1@2x.png);
   }
   .invoice{
   	background-image: url(./invoice_1@2x.png);
   }
    .guarantee{
   	background-image: url(./guarantee_1@2x.png);
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
  	font-size:12px;
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
  	width:28px;
  	background:url(./bulletin@2x.png) no-repeat center;
  	background-size:100%;
  	vertical-align: top;
  	
  }
   .bottom  .text{
   	margin-left:6px;
   	display:inline-block;
   	font-size:12px;
   	width:90%;
   	overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
   }
   .bottom .arrow{
   		display:inline-block;
   }
   .supportsMoremodel{
   	position:absolute;
   	top:0;
   	left:0;
   	z-index:100;
   	width:100%;
   	min-height:100%;
   	background-color:rgba(7,17,27,0.8);
    padding:64px 36px 32px 36px;
    box-sizing:border-box;
    padding-bottom: 64px;
   }
   .supportsMoremodel .mainContent{
  
   	color:rgb(255,255,255);
   	     
   }
   .mainContent .title{
   	 text-align:center;
   	 font-size:16px;
   	 font-weight:700;
   	 line-height:16px;
   }
   .mainContent .item{
   	
   }
    .mainContent .item .item-title{
    	display:flex;
    	width:100%;
    	margin:24px 0;
    	
    }
    .mainContent  .item-title .line{
    	flex:1 0 2%;
    	width:2%;
    	border-bottom:1px solid rgba(255,255,255,.2);
    	position:relative;
    	top:-10px;
    	
    }
    .mainContent .line-left{
    	left:0;
    	
    }
    .mainContent .line-right{
    	right:0;
    }
    .mainContent  .item-title .item-name{
    	padding: 0 24px;
    	font-size:20px;
        font-weight:700;
        
    }
    .supports-wrapper{
    	width:100%;
    
    	
    }
    .support-item{
    	margin-bottom:12px;
    	line-height:32px;
    	
    }
     .support-item:last-child{
    	margin-bottom:0px;
    }
     .support-item .icon{
     	display:inline-block;
     	width:24px;
     	height:24px;
     	margin-right:6px;
     	vertical-align: middle;
     }
     .bulletintext{
     	font-size:12px;
     	font-weight:200;
     	color:rgb(255,255,255);
     	line-height:24px;
     }
     .stickerclose{
     	position: absolute;
	    bottom: 0;
	    left: 0;
	   font-size: 32px;
	    line-height: 32px;
	    text-align: center;
	    color: rgb(255,255,255);
	    font-weight: 200;
	    width: 100%;
     }
</style>