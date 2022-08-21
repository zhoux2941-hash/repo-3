<template>
    <ul class="todo-main">
        <Item v-for="(todo, index) in todos" :todo="todo" :deleteTodo="deleteTodo" :updateTodo="updateTodo" :index="index"/>
    </ul>
</template>

<script lang="ts">
import Item from '@/components/Item/index.vue'
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'List',
    props: ['todos','deleteTodo',"updateTodo"],
    components: {
        Item
    },
    setup() {

    },
})
</script>


<style scoped>
.todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-color: 2px;
    padding: 0px;
}

.todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
}
</style>