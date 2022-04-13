<template>
  <div class="common-header">
    <div class="header-content">
      <img class="content-logo" src="../assets/logo.png">
      <div class="content-menus">
        <a class="menus-item" v-for="item in menus" :key="item.index" :class="{'active':item.index==selected}" @click="menusDidClick(item)">{{ item.title }}</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CommonHeader',
  props: {
    msg: String
  },
  data() {
    return {
      selected: 0,
      menus: [
        { 'index':0, 'title': '首页' },
        { 'index':1, 'title': '游戏规则' },
        { 'index':2, 'title': '参与流程' },
        { 'index':3, 'title': '平台优势' },
        { 'index':4, 'title': '常见问题' }
      ]
    }
  },
  mounted() {
    let that = this
    this.emitter.on("toggle-PageScrollDidScroll", index => {
      that.selected = index-1
    });
  },
  methods: {
    menusDidClick(item) {
      this.selected = item.index
      this.emitter.emit("toggle-headerDidClick", item.index)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.common-header {
  width: 100%;
  height: 80px;
  background-color: #292e3a;
  position: absolute;
  left: 0px;
  top: 0px;
  z-index: 100; 
}
.header-content {
  width: 1250px;
  height: 80px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.content-logo{
  margin-right: 80px;
}
.content-menus{
  flex: 1;
  display: flex;
  justify-content: space-between;
  align-self: center;
}
.menus-item{
  font-size: 18px;
  padding: 6px 12px;
  font-weight: 700;
  border-radius: 4px;
  white-space: nowrap;
  color: white;
}
.active{
  background-image: linear-gradient(177deg, rgb(194, 163, 7), rgb(186, 146, 0));
  background-color: initial;
  color: rgb(200, 195, 188);
}
</style>
