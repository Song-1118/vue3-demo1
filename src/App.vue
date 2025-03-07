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
    <el-table-column prop="date" label="日期" width="150" />
    <el-table-column prop="name" label="姓名" width="120" />
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
</template>

<script lang="ts" setup>
  import { ref } from 'vue'
  // 数据
  let queryInput = ref('')

  const tableData = ref([
    { date: '2025-03-07', name: '王小虎', state: '已发布', city: '上海' },
    { date: '2025-03-07', name: '王二虎', state: '已发布', city: '上海' },
    { date: '2025-03-07', name: '王三虎', state: '已发布', city: '上海' },
    { date: '2025-03-07', name: '王四虎', state: '已发布', city: '上海' },
    { date: '2025-03-07', name: '王五虎', state: '已发布', city: '上海' },
    { date: '2025-03-07', name: '王大虎', state: '已发布', city: '上海' }
  ])
  let multipleSelection = ref([])

// 方法
const selectable = (row) => ![1, 2].includes(row.id)
let delClick = () => {
  console.log('删除');
}
let editClick = () => {
  console.log("编辑");
} 
let queryClick = () => {
  console.log("增加");
}
const handleSelectionChange = (val) => {
  multipleSelection.value = val
  console.log(val);
  
}
</script>

<style scoped>
  .table-box {
    width: 800px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
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