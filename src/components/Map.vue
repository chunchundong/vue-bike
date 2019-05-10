<template>
	<div id="container">
	</div>
	<!--<div class="hello">
    <h1>{{ msg }}</h1>
    <router-link :to="{name:'Detail',params:{id:18806}}">跳转到Detail页面</router-link>
  </div>-->
</template>

<script>
	import img from '../assets/smail.png'
	export default {
		name: 'Map',
		data() {
			return {

			}
		},
		methods: {
			addMarker: function (map, point, data) { // 创建图标对象   
				var myIcon = new BMap.Icon(img, new BMap.Size(34.5, 37.5), {
					// 指定定位位置。   
					anchor: new BMap.Size(10, 25),
				});
				var self = this;
				// 创建标注对象并添加到地图   
				var marker = new BMap.Marker(point, {
					icon: myIcon
				});
				map.addOverlay(marker);
				
				//给每一个图标添加点击事件
				marker.addEventListener("click",function(){
					self.$router.push({name:"Detail",params:data});
				});
			}
		},
		mounted() {
			var map = new BMap.Map("container");
			var point = new BMap.Point(116.331398, 39.897445);

			//定位
			var that = this;
			var geolocation = new BMap.Geolocation();
			geolocation.getCurrentPosition(function(r) {
				if(this.getStatus() == BMAP_STATUS_SUCCESS) {
					//alert('您的位置：' + r.point.lng + ',' + r.point.lat);
					point = new BMap.Point(r.point.lng, r.point.lat);
				} else {
					alert('failed' + this.getStatus());
				}
				//初始化地图设置中心点
				map.centerAndZoom(point, 12);
				
				//取得数据
				//console.log(r.point);
				fetch(`/api/broken-bikes?lat=${r.point.lat}&lng=${r.point.lng}`)
				.then((res)=>{
					console.log(res);
					return res.json();
				}).then((json)=>{
					for (let i = 0;i < json.length;i++) {
						let point = new BMap.Point(json[i].lng, json[i].lat);
						that.addMarker(map,point,json[i]);
					}
				})
			}, {
				enableHighAccuracy: true
			})
			//关于状态码
			//BMAP_STATUS_SUCCESS	检索成功。对应数值“0
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
	#container {
		height: 100%;
	}
	.BMap_Marker img{
		width: 100%;
	}
</style>