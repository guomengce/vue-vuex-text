<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <Header ref="header" :addList="addList" />
      <List :toDolist="toDolist" :delTodo="delTodo" />
      <Footer :toDolist="toDolist" :allFinishedOr="allFinishedOr" :clearAllFinished="clearAllFinished" />
    </div>
  </div>

</template>

<script>
// 引入组件
import Header from './components/Header'
import List from './components/List'
import Footer from './components/Footer'

// 引入工具类
// import {readTodos} from './utils/localStorageUtil'
import Pubsub from 'pubsub-js'
export default {
  name: 'app',
  data () {
    return {
      toDolist: [{
        id: 1, title: 'csdcsgt', isDo: false
      }, {
        id: 2, title: 'cds', isDo: false
      }, {
        id: 3, title: 'yjty', isDo: false
      }, {
        id: 4, title: '12e2r3', isDo: false
      }, {
        id: 5, title: 'fre', isDo: false
      }]
    }
  },

  components: {
    Header,
    List,
    Footer
  },
  mounted () {
    this.$refs.header.$on('addTodo', this.addList)
    Pubsub.subscribe('delTodo', (msg, token) => {
      this.delTodo(token);

    })
  },

  methods: {
    delTodo (index) {
      this.toDolist.splice(index, 1);
    },
    addList (list) {
      console.log(list);
      this.toDolist.unshift(list)
    },

    allFinishedOr (isCheck) {
      this.toDolist.forEach(item => {
        item.isDo = isCheck;
      })
    },
    clearAllFinished () {
      console.log(111);
      this.toDolist = this.toDolist.filter(item => !item.isDo);
    }


  },
  watch: {

  }
}
</script>

<style>
.todo-container {
  width: 600px;
  margin: 0 auto;
}

.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
