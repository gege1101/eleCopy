<template>
	<div class="shopcart-wrapper">
		<div class="left">
			<div class="icon-left">
				<div class="icon-wrapper">
					<div class="icon-text" :class="{'icon-active':totalCount>0}">购物车</div>
					<div class="icon-count" v-show="totalCount>0">{{totalCount}}</div>
				</div>
			</div>
			<div class="price-middle">
				<div class="price">￥{{totalPrice}}</div>
				<div class="deliver">另需配送费￥{{seller.deliveryPrice}}元</div>
			</div>
		</div>
		
		<div class="send-right" :class="payClass">{{payDes}}</div>
		<div class="ball-wrapper" >
			<transition-group  tag="div"
			        v-on:before-enter="beforeEnter"
			        v-on:enter="enter"
			        v-on:after-enter="afterEnter">
			        <div class="ball" v-for="(ball,index) in balls" v-show="ball.show" :key="index">
			          <div class="inner inner-hook">
			          </div>
			        </div>
			</transition-group>
			<!--<transition name="fade"
				@before-ender="beforeEnter"
				@enter="enter"
				@after-enter="afterEnter"
				v-for="ball in balls" 
				
				>
				<div class="ball"  v-show="ball.show" >
				    <div class="innner inner-hook"></div>
			    </div>
			</transition>-->
			
		</div>
		
	</div>
	
</template>

<script>
	import vcartContral from "../cartContral/cartContral" 
	export default{
		props:{
			seller:{
				type:Object,
			},
			/*cartList:{
				type:Array,
				default(){
					return [
					  {
					    price:10,
					    count:1
					  }
					]
				}
			}*/
		},
		data(){
			return{
				balls:[
				{
					show:false
				},
				{
					show:false
				},
				{
					show:false
				},
				{
					show:false
				},
				{
					show:false
				}
				],
				dropBalls:[],
				cartList:[
				       {
					    price:10,
					    count:2
					  }
				]
			}
			
		},
		computed:{
			totalPrice(){
				let totalPrice=0;
				this.cartList.forEach((v,i)=>{
					totalPrice = totalPrice+(v.count*v.price)
				})
				return totalPrice
			},
			totalCount(){
				let totalCount=0;
				this.cartList.forEach((v,i)=>{
					totalCount = totalCount+v.count
				})
				return totalCount;
			},
			payDes(){
				let Desmsg;
				if(this.totalPrice==0){
					Desmsg =`${this.seller.minPrice}元起送`
				}else if(this.totalPrice<this.seller.minPrice){
					Desmsg =`还差${this.seller.minPrice-this.totalPrice}元起送`
				}else if(this.totalPrice>=this.seller.minPrice){
					Desmsg =`结算`
				}
				return Desmsg;
			},
			payClass(){
				if(this.totalPrice>=this.seller.minPrice){
					return 'send-right-active'
				}
			}
		},
		methods:{
			drop(el){
				console.log(el);
				for(let i=0;i<this.balls.length;i++){
					var ball = this.balls[i];
					if(!ball.show){
						ball.show=true;
						ball.el=el;
						this.dropBalls.push(ball);
						console.log(this.dropBalls);
						console.log(this.dropBalls[0].el.getBoundingClientRect());
						return;
					}
				}
			},
			beforeEnter(el){
				let count = this.balls.length;
				while(count--){
					let ball = this.balls[count];
					if(ball.show){
						let rect = ball.el.getBoundingClientRect();
						console.log(rect)
						let x = rect.left-32;
						let y = -(window.innderHeight -rect.y-22-128);
						
						
						//外层动画
						el.style.display='';
						el.style.webkitTransform =`translate3d(0,${y}px,0)`;
						el.style.transform =`translate3d(0,${y}px,0)`;
						
						//内层动画
						let inner = el.getElementsByClassName("inner-hook")[0];
						inner.style.webkitTransform=`translate3d(${x}px,0,0)`;
						inner.style.transform=`translate3d(${x}px,0,0)`;
						
					}
				}
			},
			enter(el,done){
				
				//触发浏览器重排；
				let rf = el.offsetHeight;
				this.$nextTick(()=>{
						//外层动画
						el.style.display='';
						el.style.webkitTransform =`translate3d(0,0,0)`;
						el.style.transform =`translate3d(0,0,0)`;
						
						//内层动画
						let inner = el.getElementsByClassName("inner-hook")[0];
						inner.style.webkitTransform=`translate3d(0,0,0)`;
						inner.style.transform=`translate3d(0,0,0)`;
					//	el.addEventListener('transitionend', done);
				})
				
			},
			afterEnter(el){
				let ball = this.dropBalls.shift();
				if(ball){
					ball.show = false;
					el.style.dislay="none";
				}
				
					
			}
			
		},
		components:{
			vcartContral
		},
		created(){
			
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
		.ball-wrapper{
		   .ball{
		   	  position:fixed;
		   	  left:32px;
		   	  bottom:22px;
		   	  z-index:200;
		   	  transition: all .6s cubic-bezier(.72,.23,.73,.75) ;
		   	  .inner{
		   	  	width:16px;
		   	  	height:16px;
		   	  	border-radius: 50%;
		   	  	background-color:#00A0DC;
		   	  	transition:all .4s linear;
		   	  }
		   }
		}
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
		    font-size:12px;
		}
		.send-right-active{
			background-color:#00A0DC;
			color:#fff;
			font-size:16px;
		}
		
	}
	
</style>