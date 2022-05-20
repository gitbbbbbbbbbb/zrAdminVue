<template>
	<el-tabs type="border-card" class="demo-tabs">
		<el-tab-pane label="商品查询">
			<vxe-table :column-config="{resizable: true}" border height="550" :data="tableData1">
				<vxe-column type="seq" title="序号" width="60"></vxe-column>
				<vxe-column field="age" title="省"></vxe-column>
				<vxe-column field="address" title="市" show-overflow></vxe-column>
				<vxe-column field="name" title="门店名称" sortable></vxe-column>
			 <!-- <vxe-column field="role" title="供应商名称" sortable></vxe-column> -->
				<vxe-column field="sex" title="地址"></vxe-column>
				<vxe-column field="age" title="联系方式"></vxe-column>
				<vxe-column field="address" title="备注" show-overflow></vxe-column>
			</vxe-table>
		</el-tab-pane>
		<el-tab-pane label="商品录入">
			商品录入
		</el-tab-pane>
		<el-tab-pane label="商品分类">
			商品分类
		</el-tab-pane>
		<el-tab-pane label="商品规格">
			商品规格
		</el-tab-pane>
	</el-tabs>


</template>

<script>
	import {
		defineComponent,
		ref
	} from 'vue'
	import supplieradd from './supplieradd.vue'
	export default defineComponent({
		components: {
			supplieradd
		}, //引入子组件
		setup() {
			const tableData1 = ref([{
					id: 10001,
					name: '金绿洲',
					role: '龙哥',
					sex: 'Man',
					age: '广西',
					address: '柳州'
				},
				{
					id: 10002,
					name: '金绿洲',
					role: '陈哥',
					sex: 'Women',
					age: 22,
					address: 'Guangzhou'
				},
				{
					id: 10003,
					name: '桂中',
					role: '龙哥',
					sex: 'Man',
					age: 32,
					address: 'Shanghai'
				},
				{
					id: 10004,
					name: '桂中',
					role: '刘哥',
					sex: 'Women',
					age: 23,
					address: 'test abc'
				},
				{
					id: 10005,
					name: 'Test5',
					role: 'Develop',
					sex: 'Women',
					age: 30,
					address: 'Shanghai'
				},
				{
					id: 10006,
					name: 'Test6',
					role: 'Designer',
					sex: 'Women',
					age: 21,
					address: 'test abc'
				},
				{
					id: 10007,
					name: 'Test7',
					role: 'Test',
					sex: 'Man',
					age: 29,
					address: 'test abc'
				},
				{
					id: 10008,
					name: 'Test8',
					role: 'Develop',
					sex: 'Man',
					age: 35,
					address: 'test abc'
				}
			])
			return {
				tableData1
			}
		}
	})
</script>

<style>
</style>
