<template>
	<div class="cart-contral">
		<transition name="roll">
			<div class="cart-decrease" v-show="food.count>0" @click="decrease()">
				<div class="inner">
					-
				</div>
			</div>
		</transition>
		<div class="count" v-show="food.count>0">{{food.count}}</div>
		<div class="cart-increase" @click="increase()">
			<div class="inner">
				+
			</div>
		</div>
		
	</div>
</template>
<script>
	import Vue from 'vue'
	export default{
		props:{
			food:{
				type:Object,
			}
		},
		created(){
		
		},
		methods:{
			decrease(){
				this.food.count--
				
			},
			increase(){
				if(!this.food.count){
					Vue.set(this.food,"count",1)
				}else{
					
					this.food.count++
				}
				this.$emit('increment', event.target);
				
			}
		}
	}
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
      .cart-contral{
      	overflow:hidden;
      	.roll-enter-active, .roll-leave-active{
      		transition: .3s all linear
      	}
      	.roll-enter, .roll-leave-to {
		    transform: translateX(20px) rotate(180deg) ;
		}
      	.cart-decrease{
      		float:left;
      		padding:10px;
      		.inner{
      			width:12px;
      			height:12px;
      			line-height:12px;
      			border:1px solid #00A0DC;
      			border-radius:50%;
                color:#00A0DC;
                text-align:center;
      		}
      	}
      	.count{
      		float:left;
      		width:34px;
      		color:rgb(7,17,27);
      		height:34px;
      		line-height:34px;
      		text-align:center;
      	}
      	.cart-increase{
      		float:left;
      		padding:10px;
      		.inner{
      			width:12px;
      			height:12px;
      			line-height:12px;
      			background-color #00A0DC;
      			border-radius:50%;
                color:#fff;
                text-align:center;
      		}
      	}
      		
      }
</style>

