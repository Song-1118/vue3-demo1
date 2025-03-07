<template>
  <div class="table-box">
  <!-- 标题 -->
  <div class="title">
    <h2>CRUD后台界面</h2>
  </div>
  <!-- 功能区 -->
   <div class="query-box">
    <el-input v-model="queryInput"
    style="width: 240px" 
    placeholder="请输入姓名搜索"
    clearable
  />
  <el-button type="primary" @click="queryClick">增加</el-button>
</div>
    <el-table :data="tableData" border  
    style="width: 100%" 
    ref="multipleTableRef"
    @selection-change="handleSelectionChange">
    <el-table-column type="selection" width="55" />
    <el-table-column prop="name" label="姓名" width="120" />
    <el-table-column prop="email" label="邮箱" width="170" />
    <el-table-column prop="state" label="状态" width="120" />
    <el-table-column prop="city" label="城市" width="120" />
    <el-table-column fixed="right" label="功能" min-width="120">
      <template #default>
        <el-button link type="primary" size="small" @click="delClick">删除</el-button>
        <el-button link type="primary" size="small" @click="editClick">编辑</el-button>
      </template>
    </el-table-column>
  </el-table>
  </div>

    <!-- 弹窗 -->
    <el-dialog v-model="dialogFormVisible" title="添加" width="500">
    <el-form :model="tableForm">
      <el-form-item label="姓名" :label-width="80">
        <el-input v-model="tableForm.name" autocomplete="off" />
      </el-form-item>
      <el-form-item label="邮箱" :label-width="80">
        <el-input v-model="tableForm.email" autocomplete="off" />
      </el-form-item>
      <el-form-item label="状态" :label-width="80">
        <el-input v-model="tableForm.state" autocomplete="off" />
      </el-form-item>  
      <el-form-item label="城市" :label-width="80">
        <el-input v-model="tableForm.city" autocomplete="off" />
      </el-form-item>  
    </el-form>
    <template #footer>
      <div class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">
          确认
        </el-button>
      </div>
    </template>
  </el-dialog>

</template>

<script lang="ts" setup>
  import { ref } from 'vue'
  import { ElMessage } from 'element-plus'
  // 数据
  let queryInput = ref('')
  let tableForm = ref({
    name: '',
    email: '',
    state: '',
    city: ''
  })

  const tableData = ref([
    {name: '王小虎',email:'123456@163.com', state: '已发布', city: '上海' },
    {name: '王二虎',email:'123456@163.com', state: '已发布', city: '上海' },
    {name: '王三虎',email:'123456@163.com', state: '已发布', city: '上海' },
    {name: '王四虎',email:'123456@163.com', state: '已发布', city: '上海' },
    {name: '王五虎',email:'123456@163.com', state: '已发布', city: '上海' },
    {name: '王大虎',email:'123456@163.com', state: '已发布', city: '上海' }
  ])
  let multipleSelection = ref([])
  let dialogFormVisible = ref(false)

// 方法
const selectable = (row) => ![1, 2].includes(row.id)
let delClick = () => {
  console.log('删除');
}
let editClick = () => {
  console.log("编辑");
} 
let queryClick = () => {
  dialogFormVisible.value = true
  console.log("增加");
}
const handleSelectionChange = (val) => {
  multipleSelection.value = val
  console.log(val);
}
const open2 = () => {
  ElMessage({
    showClose: true,
    message: '成功！',
    type: 'success',
  })
}
</script>

<style scoped>
  .table-box {
    width: 800px;
    margin: 80px auto;
  }
  .title {
    text-align: center;
  }
  .query-box {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }
</style>