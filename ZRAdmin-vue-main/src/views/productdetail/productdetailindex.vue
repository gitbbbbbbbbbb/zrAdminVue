<template>
	<el-tabs type="border-card" class="demo-tabs">
		<el-tab-pane label="商品信息查询">
			商品录入
		</el-tab-pane>
		
		<el-tab-pane label="商品信息录入">
			商品录入
		</el-tab-pane>
		<el-tab-pane label="商品分类">
			商品分类
		</el-tab-pane>
		<el-tab-pane label="商品规格">
			<specification></specification>
		</el-tab-pane>
	</el-tabs>


</template>

<script>
	import {
		defineComponent,
		ref
	} from 'vue'
	import specification from './specification.vue'
	export default defineComponent({
		components: {
			specification
		}, //引入子组件
		setup() {
			
		}
	})
</script>

<style>
</style>
