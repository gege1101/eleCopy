<template>
	<div class="goods-wrapper">
		<div class="goods-left"  ref="menuWrapper">
			<ul class="menu-list">
				<li class="menu-item  menu-item-hook"  :class="{active:currentIndex == index}" v-for="(item,index) in goods" @click="selectItem(index,$event)">
					<div class="item-wrapper">
						<span v-if="item.type!=-1" class="iconbar" :class="classMap[item.type]"></span><span class="text">{{item.name}}</span>
					</div>
				</li>
			</ul>
		</div>
		<div class="goods-right" ref="foodsWrapper">
			<ul class="content">
				<li class="content-item content-item-hook"  v-for="good in goods">
					<div class="title">{{good.name}}</div>
					<ul class="detail-itemwrapper">
						<li class="detail-item"  v-for="item in good.foods">
							<div class="img">
								<img :src="item.image" alt="头像" width="100%" height="100%" />
							</div>
							<div class="detail">
								<div class="name">{{item.name}}</div>
								<div class="detail">{{item.description}}</div>
								<div class="sale-number">月售{{item.sellCount}}份 好评率{{item.rating}}%</div>
								<div class="price"> <span class="text">￥{{item.price}}</span> <span class="old-price" v-if="item.oldPrice">￥{{item.oldPrice}}</span></div>
							</div>
						</li>
					</ul>
				</li>
			</ul>
		</div>
		<v-shopcart :seller="seller"></v-shopcart>
	</div>
</template>

<script>
	import BScroll from "better-scroll"
	import vShopcart from "../shopCart/shopCart"
	var ERR_OK = 0
	
	export default{
		props:{
			seller:{
				type:Object
			}
		},
		data(){
			return{
				goods:[],
				classMap:["decrease","discount","special","invoice","guarantee"],
				listHeight:[],
				scrollY:0,
				clickEvent:false
				
			}
		},
		components:{
			vShopcart
		},
		created(){
			this.$http.get('/api/goods').then((response) => {
		        response = response.body;
		        console.log(response.data)
		        if (response.errno === ERR_OK) {
		          this.goods = response.data;
		          this.$nextTick(()=>{
		          	this._initScroll();
		          	this._getHeight();
		          })
		        }
		      });
		},
		computed:{
			currentIndex(){
				for(let i=0;i<this.listHeight.length;i++){
					let h1 = this.listHeight[i];
					let h2 = this.listHeight[i+1];
					if( !h2 ||( this.scrollY<h2 && this.scrollY >=h1 )){
						return i
						
					}
				}
				return 0
			}
		},
		methods:{
			_initScroll(){
				console.log(this.$refs)
				this.menuScroll = new BScroll(this.$refs.menuWrapper,{
					click:true
				})
				this.foodsScroll = new BScroll(this.$refs.foodsWrapper,{
					probeType:3
				})
				this.foodsScroll.on('scroll',(pos)=>{
					this.scrollY = Math.abs((Math.round(pos.y)));
					let elmenus = this.$refs.menuWrapper.getElementsByClassName("menu-item-hook")
					let el = elmenus[this.currentIndex];
					this.menuScroll.scrollToElement(el,300);
				})
			},
			_getHeight(){
				let rightItems = this.$refs.foodsWrapper.getElementsByClassName("content-item-hook");
				let height = 0;
				this.listHeight.push(height);
				for(let i=0;i<rightItems.length;i++){
					height +=rightItems[i].clientHeight;
					this.listHeight.push(height)
				}
			},
			selectItem(index,event){
				this.clickEvent = true;
				let rightItems = this.$refs.foodsWrapper.getElementsByClassName("content-item-hook");
				let el = rightItems[index];
				this.foodsScroll.scrollToElement(el,300);
			}
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
 @import "../../common/stylus/index.styl"
 
	*
	  box-sizing:border-box
	.goods-wrapper
	  position:absolute
	  top:168px
	  bottom:46px
	  width:100%
	  display:flex
	  overflow:hidden
	  .goods-left
	    flex:0 0 80px
	    width:80px
	    .menu-list
	      width:100%
	      .menu-item
	        display:table
	        padding:0 12px
	        font-size:0
	        background-color:#f3f5f7
	        height:60px
	        width:100%
	        .item-wrapper
	          display:table-cell
	          vertical-align:middle
	          border-1px(rgba(7,17,27,0.1))
	          .iconbar
	            display:inline-block
	            width:20px
	            height:20px
	            vertical-align:top
	            background-size:20px 20px
	            &.decrease
	              background-image: url(./decrease_3@2x.png)
	            &.discount
	              background-image: url(./discount_3@2x.png)
			   	&.special
			   	  background-image: url(./special_3@2x.png)
			   	&.invoice
			   	  background-image: url(./invoice_3@2x.png)
			   	&.guarantee
			   	  background-image: url(./guarantee_3@2x.png)
			  .text
		        font-size:12px
		        color:rgb(7,17,27)
		        font-weight:200
		        line-height:14px
		  .active
		    background-color: #fff !important
	  .goods-right
	    flex:1
	    .content
	      width:100%
	      .title
		      width:100%
		      padding-left:14px
		      background-color: #f3f5f7
		      color:rgb(147,153,159)
		      font-size:12px
		      line-height:26px
		      height:26px
		      border-left:2px solid #d9dde1
	      .detail-itemwrapper
	          width:100%
	          .detail-item
	            display:flex
	            padding:18px 0
	            padding-left:10px
	            border-1px(rgba(7,17,27,0.1))
	            .img
	              flex:0 0 80px
	              width:80px
	              height:80px
	            .detail
	              flex:1
	              padding-left:6px
	              .name
	                font-size:14px
	                color:rgb(7,17,27)
	                line-height:14px
	                padding-top:2px
	              .detail,.sale-number
	                font-size:10px
	                color:rgb(147,153,159)
	                line-height:10px
	              .detail
	                padding:8px 0 
	              .price
	                font-size:10px
	                color:rgb(147,153,159)
	                line-height:24px
	                .text
	                  font-size:14px
	                  color:red
	                  font-weight:700
	                .old-price
	                  margin-left:8px
	                  text-decoration:line-through
</style>