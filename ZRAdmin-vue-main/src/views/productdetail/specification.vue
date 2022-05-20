<template>

	<vxe-toolbar>
		<template #buttons>
			<label>规格名称:</label>
			<el-input    style="width: 200px;margin-left: 8px;margin-right: 10px;" v-model="SpecificationNameQuery"
				placeholder="请输入规格名称" />
			<el-button type="primary"  @click="SpecificationQuerys">查询</el-button>
			<el-button type="primary" @click="addSpecification">新增规格</el-button>

		</template>
		<template #tools>

		</template>
	</vxe-toolbar>

	<vxe-table border :column-config="{resizable: true}" show-header-overflow show-overflow
		:row-config="{isHover: true}" :data="tableData2"    :sort-change="handlePageChange" >
		<vxe-column type="seq" title="序号" width="60"></vxe-column>
		<vxe-column field="specificationName" title="规格名称" sortable></vxe-column>
		<vxe-column field="sex" title="操作">
		<template v-slot="{ row }">
		              <el-button
		               
		                @click="specificationedit(row)"
		                size="mini"
		                icon="el-icon-edit"
		                type="primary"
		                >编辑</el-button
		              >
		              <el-button
						@click="specificationdel(row)" 
		                size="mini"
		                icon="el-icon-delete"
		                type="danger"
		                >删除</el-button
		              >
		            </template>
		</vxe-column>
		
		>
		<!-- <template #pager>
		            <vxe-pager
		              :layouts="['Sizes', 'PrevJump', 'PrevPage', 'Number', 'NextPage', 'NextJump', 'FullJump', 'Total']"
		              v-model:current-page="tablePage.currentPage"
		              v-model:page-size="tablePage.pageSize"
		              :total="tablePage.total"
		              @page-change="handlePageChange">
		            </vxe-pager>
		          </template> -->
	</vxe-table>
	<vxe-pager perfect v-model:current-page="tablePage.currentPage" v-model:page-size=" tablePage.pageSize"
		:total=" tablePage.totalResult"
		:page-sizes="[10, 20, 100, {label: '大量数据', value: 1000}, {label: '全量数据', value: -1}]"
		:layouts="['PrevJump', 'PrevPage', 'Number', 'NextPage', 'NextJump', 'Sizes', 'FullJump', 'Total']">

	</vxe-pager>


	<!-- 新增、修改弹出框 -->
	<el-dialog v-model="dialogVisible" :title="titletype" width="30%" heigh="600px" :draggable="true">
		<div>
			<label>规格名称：</label>
			<el-input clearable style="width: 200px;margin-left: 8px;margin-right: 10px;"
				v-model="form.SpecificationName" placeholder="请输入规格名称" />
		</div>

		<div style="margin-top: 40px; margin-left: 40px;">
			<el-button type="primary" @click="saveSpecification">保存</el-button>

		</div>
	</el-dialog>


</template>


<script setup name="pecification">
	import {
		SpecificationAddOrEdit,
		SpecificationQuery ,SpecificationDel
	} from '@/api/myself/productdetail.js'
	const tablePage = reactive({
		totalResult: 0,
		currentPage: 1,
		pageSize: 10,
		Sort: "SpecificationId",
		SortType: "desc"
	})

	const dialogVisible = ref(false)
	const tableData2 = ref([])
	const form = reactive({
		SpecificationName: '',
		SpecificationId: 0,
	})
	const titletype = ref("新增规格")
	const typeflag = ref("AddSpecification") //默认是新增状态

	const SpecificationNameQuery = ref("")

	SpecificationQuerys();

	function handlePageChange() {
		alert("点击了分页")
	}

	function addSpecification() {
		
		typeflag.value = "AddSpecification";
		dialogVisible.value = true
		titletype.value = "新增规格"

	}



	function SpecificationQuerys() {
		const queryparam = {
			SpecificationNameQuery: SpecificationNameQuery.value,
			pagerinfo: tablePage
		}


		SpecificationQuery(queryparam).then((res) => {
			//alert(res.data.totalnum)
			tablePage.totalResult=res.data.totalnum;
			tableData2.value = res.data.list
		})
	}

	function specificationedit(row){
		
		// alert(row.specificationName)
		typeflag.value = "EditSpecification";
		dialogVisible.value = true;
		form.SpecificationId=row.specificationId;
		form.SpecificationName=row.specificationName;
		titletype.value = "编辑规格"
	}
	
	function specificationdel(row){
		
		SpecificationDel(row.specificationId ).then((res)=>{
			if(res.data.code==1){
				alert("规格删除成功")
				SpecificationQuerys()
			}else{
				alert("删除失败")
			}
		})
	}
	
	function saveSpecification() {
		var saveparamdata = {
			SpecificationType: typeflag.value, //操作状态
			form: form //提交的数据
		}
		SpecificationAddOrEdit(saveparamdata).then((res) => {
			if (res.data.code == 1) {
				dialogVisible.value = false;
				form.SpecificationId = 0;
				form.SpecificationName = "";
				alert("规模名称保存成功")
				SpecificationQuerys();
			} else {
				if (res.data.errmsg != "")
					alert(res.data.errmsg + "   ,规模名称保存失败！")
			}
		})

	}
</script>




<style>
</style>
