<script lang="ts" setup>
import Map from '@/component/HomePage/Map.vue'
import Pie from '@/component/HomePage/Pie.vue'
import {onMounted, reactive, ref} from "vue";
import {getData} from "@/api/HomePageApi";


// 地图数据
const data = reactive<IHomeData>({
	salePie: [],
	saleMap: []
})

// 获取城市数据
onMounted(() => {
	getData().then(res => {
		console.log(res)
		// @ts-ignore
		data.saleMap = res.data.data.saleMap
		// @ts-ignore
		data.salePie = res.data.data.salePie
	})
})
</script>

<template>
	<div class="box">
		<el-breadcrumb separator="/" class="breadcrrumb">
			<el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
		</el-breadcrumb>
		<el-divider />
		<Pie :data="data.salePie"></Pie>
		<Map :data="data.saleMap"> </Map>
	</div>
</template>

<style lang="scss" scoped>
.breadcrrumb{
	margin-bottom: 20px;
}
</style>