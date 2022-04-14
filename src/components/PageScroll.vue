<template>
  <div class="fullPage" ref="fullPage">
    <div
      class="fullPageContainer"
      ref="fullPageContainer"
      @mousewheel="mouseWheelHandle"
      @DOMMouseScroll="mouseWheelHandle"
    >
      <home-view />
      <div class="section section2">2</div>
      <div class="section section3">3</div>
      <div class="section section4">4</div>
      <div class="section section5">5</div>
    </div>
  </div>
</template>

<script>
import HomeView from "@/pages/home/homeView.vue"
export default {
  name: 'PageScroll',
  components: { HomeView },
  data() {
    return {
      isHeaderClick: false,
      fullpage: {
        current: 1, // 当前的页面编号
        isScrolling: false, // 是否在滚动,是为了防止滚动多页，需要通过一个变量来控制是否滚动
        deltaY: 0  // 返回鼠标滚轮的垂直滚动量，保存的鼠标滚动事件的deleteY,用来判断是往下还是往上滚
      }
    };
  },
  mounted() {
    let that = this
    this.emitter.on("toggle-headerDidClick", index => {
      that.isHeaderClick = true
      that.move(index+1)
    });
  },
  methods: {
    next() { // 往下切换
      let len = 4; // 页面的个数
      if (this.fullpage.current + 1 <= len) { // 如果当前页面编号+1 小于总个数，则可以执行向下滑动
        this.fullpage.current += 1; // 页面+1
        this.move(this.fullpage.current); // 执行切换
      }
    },
    pre() {// 往上切换
      if (this.fullpage.current - 1 > 0) {  // 如果当前页面编号-1 大于0，则可以执行向下滑动
        this.fullpage.current -= 1;// 页面+1
        this.move(this.fullpage.current);// 执行切换
      }
    },
    move(index) {
      this.fullpage.isScrolling = true; // 为了防止滚动多页，需要通过一个变量来控制是否滚动
      this.directToMove(index); //执行滚动
      setTimeout(() => {       //这里的动画是1s执行完，使用setTimeout延迟1s后解锁
        this.fullpage.isScrolling = false;
      }, 800);
    },
    directToMove(index) {
      let height = this.$refs["fullPage"].clientHeight;  //获取屏幕的宽度
      let scrollPage = this.$refs["fullPageContainer"];    // 获取执行tarnsform的元素
      let scrollHeight; // 计算滚动的告诉，是往上滚还往下滚
      scrollHeight= -(index - 1) * height + "px";
      scrollPage.style.transform = `translateY(${scrollHeight})`;
      this.fullpage.current = index;
      if (this.isHeaderClick) return this.isHeaderClick = false
      this.emitter.emit("toggle-PageScrollDidScroll", index)
    },
    mouseWheelHandle(event) { // 监听鼠标监听
      // 添加冒泡阻止
      let evt = event || window.event;
      if (evt.stopPropagation) {
        evt.stopPropagation();
      } else {
        evt.returnValue = false;
      }
      if (this.fullpage.isScrolling) { // 判断是否可以滚动
        return false;
      }
      let e = event.originalEvent || event;
      this.fullpage.deltaY = e.deltaY || e.detail; // Firefox使用detail
      if (this.fullpage.deltaY > 0) {
        this.next();
      } else if (this.fullpage.deltaY < 0) {
        this.pre();
      }
    }
  }
};
</script>

<style scoped>
.fullPage{
  height: 100%;
  overflow: hidden;
  background-color: rgb(189, 211, 186);
}
.commonHeader {
  height: 120px;
  width: 100%;
  background-color: aqua;
}
.fullPageContainer{
  width: 100%;
  height: 100%;
  transition: all linear 0.5s;
}
.section {
  width: 100%;
  height: 100%;
  background-position: center center;
  background-repeat: no-repeat;
}
.section1 {
  background-color: rgb(18, 21, 25);
  /* background: url("@/assets/intro-bg.png"); */
}
.section2 {
  /* background-color: #131516; */
  background-color: yellow;
}
.section3 {
  /* background-color: rgb(18, 21, 25); */
  background-color: purple;
}
.section4 {
  background-color: #131516;
}
.section5 {
  background-color: green;
}
</style>

