<template>
  <div class="main-content">
    <common-header />
    <page-scroll />
  </div>
</template>

<script>
import CommonHeader from '@/components/CommonHeader.vue'
import PageScroll from '@/components/PageScroll.vue'

export default {
  name: 'App',
  components: {
    CommonHeader,
    PageScroll
  }
}
</script>

<style scope lang="less">
.main-content {
    display: flex;
    flex-direction: column;
    height: 100%;
}
</style>
