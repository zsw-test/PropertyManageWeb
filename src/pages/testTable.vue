<template>
  <el-table
    :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
    style="width: 100%">
    <el-table-column
      label="ID"
      prop="ID">
    </el-table-column>
    <el-table-column
      label="Username"
      prop="Username">
    </el-table-column>
    <el-table-column
    label="操作"
      align="right">
      
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">Delete</el-button>
      </template>
    </el-table-column>
  </el-table>

</template>

<script>
  export default {
    data() {
      return {
        tableData: [],
        search: '',
      }
    },
    methods: {
      getdata(){
          this.$axios.get('http://www.zsw.test:31717/api/manager/1/page?pageindex=1&pagesize=10000')
        //then获取成功；response成功后的返回值（对象）
        .then(response=>{
          console.log(response.data.data);
          this.tableData = response.data.data
        })
        //获取失败
        .catch(error=>{
          console.log(error);
          alert('网络错误，不能访问');
        })
  
      },
      handleEdit(index, row) {
        console.log(index, row);
      },
      handleDelete(index, row) {
        console.log(index, row);
      }
    },
    created(){
      this.getdata()
    }
  }
</script>