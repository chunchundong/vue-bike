<template>
	<div class="detail">
		<h1>{{ msg }}</h1>
		<p>车辆编号:{{$route.params.id}}</p>
		<p>故障信息:{{$route.params.detail}}</p>
		<mt-checklist title="" v-model="method" :options="['更换二维码', '更换轮胎', '更换车锁']"></mt-checklist>
		<mt-button type="primary" @click="repairDong" size="large">维修完成</mt-button>
		<mt-button type="default" @click="back" size="large">返回</mt-button>
	</div>
</template>

<script>
	export default {
		name: 'Detail',
		data() {
			return {
				msg: '欢迎来到维修界面',
				method: []
			}
		},
		methods: {
			repairDong() {
				let id = this.$route.params.id;
				let method = this.method;
				fetch(`/api/repair?id=${id}&method=${method}`)
					.then((res) => {
						return res.json();
					}).then((json) => {
						console.log(json);
						if(json.message) {
							alert(json.message);
						}
					})
			},
			back() {
				this.$router.push({
					path: "/"
				});
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.detail{
		text-align: left;
	}
	.mint-button{
		width: 98%;
		margin: 10px auto 0 auto;
	}
	.mint-cell{
		opacity: 0.5;
	}
</style>