<template>
  <el-container>
    <el-aside style="width: 200px;margin-top: 20px">
      <switch></switch>
      <!--<SideMenu></SideMenu>-->
    </el-aside>
    <el-main>
      <WorkReport class="books-area"></WorkReport>
    </el-main>
  </el-container>
</template>

<script>
import WorkReport from './WorkReport'
export default {
  name: 'WorkReportIndex',
  components: {WorkReport}
}
</script>

<style scoped>

</style>
