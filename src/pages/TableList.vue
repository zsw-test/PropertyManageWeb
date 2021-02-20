<template>
    <div class="row">
      <div class="col-12">
        <card :title="table1.title">
          <div class="table-responsive">
            <base-table :data="table1.data"
                        :columns="table1.columns"
                        thead-classes="text-primary">
            </base-table>
          </div>
        </card>
      </div>

      <div class="col-12">
        <card class="card-plain">
          <div class="table-full-width table-responsive">
            <base-table :title="table2.title" :sub-title="table2.subTitle" :data="table2.data"
                         :columns="table2.columns">

            </base-table>
          </div>
        </card>
      </div>

    </div>
</template>
<script>
import { BaseTable } from "@/components";
  const tableColumns = ['ID', 'Houseid', 'Water', 'Electric', 'Gas','Property']
export default {
  components: {
    BaseTable
  },
  data() {
    return {
      table1: {
        title: "Simple Table",
        columns: [...tableColumns],
        data: []
      },
      table2: {
        title: "Table on Plain Background",
        columns: [...tableColumns],
        data: []
      }
    };
  },
    created(){
 
      this.$axios.get('http://www.zsw.test:31717/api/manager/1/chargepage?pageindex=1&pagesize=10000')
       //then获取成功；response成功后的返回值（对象）
      .then(response=>{
         console.log(response.data.data);
         this.table1.data=response.data.data;
         this.table2.data=response.data.data;
         console.log( this.table1.data);
      })
       //获取失败
      .catch(error=>{
        console.log(error);
        alert('网络错误，不能访问');
      })
  }
};
</script>
<style>
</style>
