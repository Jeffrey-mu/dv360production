<template>
  <div>
    <el-header style="border-bottom: 1px solid #ccc; line-height: 60px;">
      <div style="font-size: 25px;">Production materials</div>
    </el-header>
    <el-main style="height: calc(100vh - 60px); overflow:auto">
      <Index />
    </el-main>

  </div>
</template>
<script>
import Index from './view'
export default {
  components: {
    Index
  }
}
</script>
