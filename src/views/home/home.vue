<template>
  <el-container>
    <layout-aside></layout-aside>

    <el-container>
      <el-header style='padding:0'>
        <layout-header></layout-header>

      </el-header>
      <el-main style="margin:0;padding:0">
        <layout-main></layout-main>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import Layoutaside from '../../components/home/layout-aside.vue'
import layoutheader from '../../components/home/layout-header.vue'
import layoutmain from '../../components/home/layout-main.vue'

export default {
  components: {
    'layout-aside': Layoutaside,
    'layout-header': layoutheader,
    'layout-main': layoutmain
  }
}
</script>

<style>
</style>
