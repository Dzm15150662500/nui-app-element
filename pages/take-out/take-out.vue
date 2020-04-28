<template>
	<view>
		<mSearch :mode="2" button="inside" :show="false" @search="search($event,3)" @tap='gotoLunBo'></mSearch>

	<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
		<swiper-item>
			<view class="swiper-item" v-for="(item,index) in meishi1" :key='index'>
				<image :src="item.image_hash | urlFormatter" mode=""></image>
			</view>
		</swiper-item>
	</swiper>









	</view>
</template>

<script>
	import mSearch from '@/components/mehaotian-search/mehaotian-search.vue';
	export default {
		components: {
			mSearch,
		},
		data() {
			return {
				val3: '',
				meishi1:[],
			}
		},
		onLoad() {
			this.meishi()
		},
		
			// 过滤器
					  filters:{
					        urlFormatter(oldValue){
					            const first = "https://fuss10.elemecdn.com/";
					            const second = oldValue.slice(0,1);
					            const third = oldValue.slice(1,3);
					            const forth = oldValue.slice(3);
					            const fifth = ".jpeg?imageMogr/thumbnail/!90x90r/gravity/Center/crop/90x90/";
					            return `${first}${second}/${third}/${forth}${fifth}`;
					        }
					    },
						
		methods: {
			// 搜索框
			search(e, val) {
				console.log(e, val);
				this['val' + val] = e;
			},
			gotoLunBo() {
				uni.navigateTo({
					// url: 'test?id=1&name=uniapp'  c传递参数
					url: "/pages/sousuo/sousuo"
				})
			},
			
		
				meishi(){
					uni.request({
						url:'http://localhost:3000/restapi/shopping/v2/entries',
						method:"GET",
						success: (res) => {
							console.log(res)
							this.meishi1 = res.data[0].entries
						},
						fail: (error) => {
								console.log(error,2)
						}
					})
				}
		},
		
		
	}
</script>

<style>

</style>
