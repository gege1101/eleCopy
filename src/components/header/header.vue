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
					
				</div>
			</div>
		</div>
		<div class="bottom">
			<span class="icon"></span>
			<span class="text"></span>
			<span class="arrow"></span>
			
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
			
		},
		created(){
			
		},
		methods:{}
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
   .top .contentWrapper {
   	flex:1 0 auto;
   	padding-left:16px;
   	
   }
	 
	  
</style>