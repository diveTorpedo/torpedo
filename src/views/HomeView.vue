<template>
	<div>
		<el-carousel :interval="4000" type="card" height="400px">
			<el-carousel-item v-for="item in imgBox.list" :key="item">
				<img :src="item.url_image" alt="" srcset="" class="img-item" />
			</el-carousel-item>
		</el-carousel>

	</div>
</template>


<script lang="ts" setup>
import { ref, onMounted, reactive, inject } from 'vue';
import { Menu as IconMenu, Message, Setting } from '@element-plus/icons-vue';
import axios from 'axios';
const $http = inject('$http');
let imgBox = reactive({ list: [] });


onMounted(() => {
	getNewImage();
});
let getNewImage = () => {
	console.log(this);

	let url = `https://wall.alphacoders.com/api2.0/get.php?auth=1a1e07617b922b49f1f1efb53cf1326f&method=newest&width=1920&height=1080&page=10&info_level=2`;
	$http
		.get(url, {
			headers: {
				'Content-Type': 'application/json'
			}
		})
		.then(res => {
			imgBox.list = res.data.wallpapers;
			console.log(res);
		});

	$http
		.get(
			'https://v2.jinrishici.com/one.json?client=npm-sdk/1.0&X-User-Token=OGFrpjvnhgaIKrR9oRhA66KdRkaxFa0D'
		)
		.then(result => {
			console.log(result);
			poetry.val = result.data.data.origin;
		})
		.catch(err => {});
};
</script>

<style scoped>
.img-item {
	width: 100%;
	height: 100%;
}

.el-carousel__item h3 {
	color: #475669;
	opacity: 0.75;
	line-height: 200px;
	margin: 0;
	text-align: center;
}

.el-carousel__item:nth-child(2n) {
	background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
	background-color: #d3dce6;
}
</style>
