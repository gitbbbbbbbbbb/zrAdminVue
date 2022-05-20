<template>
	<el-form :model="form" label-width="120px">
		<el-form-item label="供应商名称">
			<el-input v-model="form. suppliername" />
		</el-form-item>
		<el-form-item label="地址">
			<el-input v-model="form.address" />
		</el-form-item>
		<el-form-item label="联系方式">
			<el-input v-model="form.context" />
		</el-form-item>
		<el-form-item label="备注">
			<el-input v-model="form.remark" type="textarea" />
		</el-form-item>
		<el-form-item>
			<el-button type="primary" @click="onSubmit">保存</el-button>
			<el-button type="primary" @click="empty">清空</el-button>
		</el-form-item>
	</el-form>
</template>

<script lang="ts" setup>
	import {
		reactive
	} from 'vue'
	import {
		supplieradd
	} from '@/api/myself/supplier.js'
	// do not use same name with ref
	const form = reactive({
		suppliername: '',
		address: '',
		context: '',
		remark: '',
	})

	const onSubmit = () => {

		supplieradd(form).then((response) => {
			window.console.log(response)
			if (response.data.code == 0) {
				alert("保存成功")
			} else {
				alert("供应商名称重复，不能保存！")
			}
		})
	}

	const empty = () => {
		form.suppliername = '';
		form.address = '';
		form.context = '';
		form.remark = '';
	}
</script>
