<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="isCheck" />
    </label>
    <span>
      <span>已完成{{finishedCount}}件</span> / 总计{{toDolist.length}}件
    </span>
    <button @click="clearAllFinished" class="btn btn-warning">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "Footer",
  data () {
    return {
      // isCheck: false
    }
  },
  props: {
    toDolist: Array,
    allFinishedOr: Function,
    clearAllFinished: Function
  },
  computed: {
    finishedCount () {
      return this.toDolist.reduce((total, item) => total + (item.isDo ? 1 : 0), 0);
    },
    isCheck: {
      get () {
        return this.toDolist.length === this.finishedCount;
      },
      set (val) {
        console.log(val);
        this.allFinishedOr(val);
      }
    }

  }
}
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>