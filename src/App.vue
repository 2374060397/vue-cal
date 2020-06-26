<template>
  <div id="app">
    <Toggler :size="2" :checked="checked[0]" @updated="(value) => updatedHandler(0, value)">Good</Toggler>
    <Toggler :size="2" :checked="checked[1]" @updated="(value) => updatedHandler(1, value)">Cheap</Toggler>
    <Toggler :size="2" :checked="checked[2]" @updated="(value) => updatedHandler(2, value)">Fast</Toggler>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Toggler from './components/Toggler.vue'


export default {
  name: 'App',
  components: {
    Toggler
  },
  data() {
    return {
      checked : [false, false, false],
      indexes: [],
    }
  },
  // 每当我打开一个按钮，他就会赋值到一个arr中，比如我把他放到indexes中，不过最多放两个值，
  // 当有第三个值，就把第一个值给踢出去，然后在把数组里的按钮标号为true，其余的为false
  methods: {
    updatedHandler(index, value) {
      // console.log(index, value) //0-true,1-false
      // 下面这个this.indexes.includes(index)的意思是当indexes里没有id为0，1，2中我点击的那个
      if (value && !this.indexes.includes(index)) {
        let newIndexes = [...this.indexes]
        newIndexes.push(index)
        this.indexes = newIndexes
      } // 先判断value是true，而且idnex未在idnexs数组里，就是开启了开关，按钮编号未在idnexs里
      
      if (!value && this.indexes.includes(index)) {
        //当value为false，也就是关闭按钮并且包含这个关闭按钮在indexes里，移出
        let newIndexes = [...this.indexes]
        newIndexes.splice(this.indexes.indexOf(index), 1)
        this.indexes = newIndexes //然后再重新赋值给列表
      }
      //当indexs里有三个值，那就把第一个值移出
      if (this.indexes.length ===3) {
        let newIndexes = [...this.indexes]
        newIndexes.splice(0, 1)
        this.indexes = newIndexes
      }
      //初始化 checked值，如果this.indexes[0]是有值的话，即是编号按钮,讲checked对应的位置设置为true
      //下面的[1]是同样的检测方式
      let checked = [false, false, false]

      if (typeof this.indexes[0] !== 'undefined') {
        checked[this.indexes[0]] = true
      }
      if (typeof this.indexes[1] !== 'undefined') {
        checked[this.indexes[1]] = true
      }

      this.checked=checked
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
}
body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
  padding: 0;
}
</style>
