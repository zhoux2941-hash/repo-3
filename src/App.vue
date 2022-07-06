<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <Header :addTodo="addTodo" />
      <List :todos="todos" :deleteTodo="deleteTodo" :updateTodo="updateTodo" />
      <Footer :todos="todos" :checkAll="checkAll" :clearAllCompletedTodos="clearAllCompletedTodos" />
    </div>
  </div>
</template>

<script lang="ts">
import Header from '@/components/Header/index.vue'
import List from '@/components/List/index.vue'
import Footer from '@/components/Footer/index.vue'
import { defineComponent, onMounted, reactive, toRefs,watch } from 'vue'
import Todo from '@/types/todo'
import {saveTodos,readTodos} from '@/utils/localStorageUtils'

export default defineComponent({
  name: 'App',
  components: {
    Header,
    List,
    Footer
  },
  setup() {
    const state = reactive<{ todos: Todo[] }>({
      todos: [
        // { id: 1, title: '学习', isCompleted: true },
        // { id: 2, title: '吃饭', isCompleted: false },
        // { id: 3, title: '睡觉', isCompleted: false },
      ]
    })

    // 页面加载的时候读取数据
    onMounted(()=>{
      setTimeout(() => {
        state.todos = readTodos()
      }, 1000);
    })


    //添加数据
    const addTodo = (todo: Todo) => {
      state.todos.unshift(todo)
    }

    const deleteTodo = (index: number) => {
      state.todos.splice(index, 1)
    }

    //修改todo的isComplete属性的状态
    const updateTodo = (todo: Todo, isCompleted: boolean) => {
      todo.isCompleted = isCompleted
      console.log(todo.isCompleted)
    }

    //全选或者全部取消
    const checkAll = (isCompleted: boolean) => {
      state.todos.forEach((todo) => {
        todo.isCompleted = isCompleted
      })
    }

    // 清除已经完成的任务
    const  clearAllCompletedTodos = ()=>{

      state.todos = state.todos.filter(todo => !todo.isCompleted)
      console.log(state.todos,1)
    }

    //监视操作：如果todos数组的数据变化了,
    watch(()=> state.todos,(value) =>{
       saveTodos(value)
    },{deep:true})


    return {
      ...toRefs(state),
      addTodo,
      deleteTodo,
      updateTodo,
      checkAll,
      clearAllCompletedTodos
    }
  },
})
</script>

<style scoped>
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
