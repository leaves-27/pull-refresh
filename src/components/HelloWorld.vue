<template>
  <div class="hello">
    <vue-scroll
      :ops="options"
      @refresh-start="refresh"
      @load-start="loadMore"
      ref="vs">
      <div class="header-placeholder">
        <div class="header">
          <div class="header-inner">
            我是头部
          </div>
        </div>
      </div>
      <ul class="list">
        <li v-for="(item, index) in dataList" :key="index">
          {{ item.name }}
        </li>
      </ul>
       <div class="child-dom"></div>
    </vue-scroll>
  </div>
</template>
<script>
import vueScroll from 'vuescroll/dist/vuescroll-slide';
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    vueScroll
  },
  data() {
    return {
      options: {
        vuescroll: {
          mode: 'slide',
          renderMethod: 'position',
          pullRefresh: {
            enable: true,
            tips: {
              deactive: 'Pull to Refresh',
              active: 'Release to Refresh',
              start: 'Refreshing...',
              beforeDeactive: 'Refresh Successfully!'
            }
          },
          pushLoad: {
            enable: true,
            tips: {
              deactive: 'Push to Load',
              active: 'Release to Load',
              start: 'Loading...',
              beforeDeactive: 'Load Successfully!'
            },
            auto: false,
            autoLoadDistance: 0
          },
        },
        scrollPanel: {},
        rail: {},
        bar: {}
      },
      dataList: [{
        name: '111111'
      }, {
        name: '22'
      },{
        name: '333'
      },{
        name: '444'
      },{
        name: '5555'
      }]
    }
  },
  methods: {
    refresh(vm, refreshDom, done) {
      setTimeout(() => {
        done();
      }, 6000);
    },
    loadMore(vm, refreshDom, done) {
      setTimeout(() => {
        const arr = [];
        const length = this.dataList.length;
        for(let i = length;i < (length + 10); i ++) {
          arr.push({
            name: `${i}${i}${i}${i}`
          });
        }
        this.dataList.push(...arr);
        this.$refs.vs.refresh();
        done();
      }, 6000);
    },
  }
}
</script>
<style>
  .__pane{
    webkit-overflow-scrolling: touch
  }
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body{
  background-color: #333;
}
.list li{
  display: block;
  height: 200px;
  background-color: #00ffff;
}
.list li:nth-child(2n+1){
  display: block;
  height: 200px;
  background-color: #0088aa;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello{
  height: 100%;
}
.header{
  width: 100%;
  height: 44px;
  text-align: center;
  position: fixed;
  left:0;
  top:0;
  z-index: 1000;
  background-color: #ff0000;
  color: #fff;
}
.header-placeholder{
  width: 100%;
  height: 44px;
  line-height: 44px;
}
</style>
