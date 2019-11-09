<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="page-group">
      <div class="page page-current">
        <!-- html代码 -->
        <!-- ---------------------Here is Tab code---------------------- -->
        <Tab @changetext="changetext"></Tab>

        <!-- -------------------Here is container code----------------- -->
        <Container @changeflagdel="changeflag" :todos="newTodos" @userchangedone="userchangedone"></Container>

        <!-- -------------------Here is foornav code------------------------ -->
        <Footnav :tabs="tabs" :type="type" @userchoose="userchoose"></Footnav>

        <!-- -------------------Here is usertext code------------------------ -->
        <Usertext :textflag='textflag' @changetext2="changetext" @userwrite="userwrite"></Usertext>

        <!-- -------------------Here is usercheck code------------------------ -->
        <Usercheck :flag='flag' @changeflagdel2="changeflag" @deltask="deltask"></Usercheck>
      </div>
  </div>
  </div>
</template>

<script>
import Vue from 'vue'
let bus = new Vue()
// import HelloWorld from './components/HelloWorld.vue'
import Tab from './components/Tab.vue'
import Container from './components/Container.vue'
import Footnav from './components/Footnav.vue'
import Usertext from './components/Usertext.vue'
import Usercheck from './components/Usercheck.vue'

export default {
  
  components: {
    // HelloWorld
    Tab,
    Container,
    Footnav,
    Usertext,
    Usercheck
  },
  data () {
    return {
      todos: [{
      id: 1,
      task: '今天早上8点起床！',
      done: true,
      times: '10:20:30'
    } ],
    tabs: [{
      choose: 'All',
      num: 0,
      class: 'tab-item external'
    },
    {
      choose: 'UnDone',
      num: 0,
      class: 'tab-item external'
    },
    {
      choose: 'Finished',
      num: 0,
      class: 'tab-item external'
    }
    ],
    flag: false,
    textflag: false,
    index: 0,
    type: 'All',
    }
  },
  methods: {
    changetext() {
      this.textflag = !this.textflag
      getnum(this.todos, this.tabs)

    },
    changeflag(index) {
      this.flag = !this.flag
      this.index = index
      getnum(this.todos, this.tabs)
    },
    userwrite(val) {
      var a = getTimerr()

      this.todos.push({
        id: sort(this.todos)[0].id + 1,
        task: val,
        done: false,
        times: a
      })
      getnum(this.todos, this.tabs)

    },
    userchangedone(index) {
      this.todos[index].done = !this.todos[index].done
      getnum(this.todos, this.tabs)

    },
    deltask() {
      if (this.todos[this.index].done) {
          this.todos.splice(this.index, 1)
      } else {
          alert('请先完成您的任务哦！')
      }
      getnum(this.todos, this.tabs)

    },
    userchoose(choose) {
      this.type = choose
      getnum(this.todos, this.tabs)

    }

  },
  computed: {
    newTodos() {
      switch (this.type) {
        case 'All':
          return this.todos
          break;
        case 'UnDone':
          return this.todos.filter(item => !item.done)
          break;
        default :
          return this.todos.filter(item => item.done)
          
        
      }
    }
    },
    created() {
      getnum(this.todos, this.tabs)
      // this.tabs[0].num = this.todos.length
      // this.tabs[1].num = this.todos.filter(item => !item.done).length
      // this.tabs[2].num = this.todos.filter(item => item.done).length
    }

}

//自定义函数  排序
function sort(arr) {
    return arr.sort(function(a, b) {
        return b.id - a.id
    })
}
// 得到数据条数
function getnum(arr, b) {
    b[0].num = arr.length
    b[1].num = arr.filter(item => !item.done).length
    b[2].num = arr.filter(item => item.done).length
}
//发送时间
function getTimerr(t) {
    var time = new Date();
    var hour = time.getHours();
    hour = hour < 10 ? '0' + hour : hour;
    var minute = time.getMinutes();
    minute = minute < 10 ? '0' + minute : minute;
    var second = time.getSeconds();
    second = second < 10 ? '0' + second : second;
    return hour + ':' + minute + ':' + second;
}
</script>

<style lang="stylus">
  @import './assets/todolist.css';
</style>
