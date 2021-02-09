案例：TodoList

1.传统的prop传值用法
2.emit的另一种用法
3.发布与订阅
  下载：npm install pubsub-js --save
  引入：import Pubsub from 'pubsub-js'
  使用：谁订阅谁处理
  发布：Pubsub.publish('delTodo',this.index)
  订阅:Pubsub.subscribe('delTodo',(msg,index)=>{

  })
4.slot 