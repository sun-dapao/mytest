<template>
  <div>
    <search-bar @onSearch="searchResult" ref="searchBar"></search-bar>
  <el-table
    :data="tableData.slice((curPage-1)* pageSize, curPage * pageSize)"
    stripe
    style="width: 100%">
    <el-table-column
      prop="date"
      label="日期"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="地址">
    </el-table-column>
  </el-table>
    <edit-form @onSubmit="loadBooks()" ref="edit"></edit-form>
  <el-row>
    <el-pagination
      @current-change="handleCurrentChange"
      :current-page="curPage"
      :page-size="pageSize"
      :total="tableData.length">
    </el-pagination>
  </el-row>
  </div>
</template>

<script>
import EditForm from './EditForm'
import SearchBar from './SearchBar'
export default {
  name: 'WorkReport',
  components: {EditForm, SearchBar},
  data () {
    return {
      pageSize: 2,
      curPage: 1,
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄'
      }]
    }
  },
  methods: {
    getData () {
      // 这里使用axios，使用时请提前引入
      this.$axios.post('workReport/queryList', {
        orgCode: 1
      }, {emulateJSON: true},
      {
        headers: { 'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8' }
      }
      ).then(response => {
        console.log(response)
        // 将数据赋值给tableData
        this.tableData = response.data
        // 将数据的长度赋值给totalCount
        this.totalCount = response.data.length
      })
    },
    // 分页
    // 每页显示的条数
    handleSizeChange (val) {
      // 改变每页显示的条数
      this.PageSize = val
      // 注意：在改变每页显示的条数时，要将页码显示到第一页
      this.currentPage = 1
    },
    // 显示第几页
    handleCurrentChange (val) {
      // 改变默认的页数
      this.currentPage = val
    }
  },
  created: function () {
    this.getData()
  }
}
</script>

<style scoped>

</style>
