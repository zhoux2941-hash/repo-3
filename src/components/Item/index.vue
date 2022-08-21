<template>
    <li @mouseenter="mouseHandler(true)" @mouseleave="mouseHandler(false)"
        :style="{ backgroundColor: bgColor, color: myColor }">
        <label>
            <input type="checkbox" v-model="isComptete">
            <span>{{ todo.title }}</span>
        </label>
        <button class="btn btn-danger" style="display:none" v-show="isshow" @click="delTodo">删除</button>
    </li>
</template>

<script lang="ts">
import Todo from '@/types/todo'
import { computed, defineComponent, ref } from 'vue'

export default defineComponent({
    name: 'Item',
    props: {
        todo: {
            type: Object as () => Todo,
            required: true
        },
        deleteTodo: {
            type: Function,
            required: true
        },
        index: {
            type: Number,
            required: true
        },
        updateTodo: {
            type: Function,
            required: true
        }
    },
    setup(props) {
        const bgColor = ref('white')
        const myColor = ref('block')
        const isshow = ref(false)

        const mouseHandler = (flag: boolean) => {
            if (flag) {
                //鼠标移入的时候
                bgColor.value = 'pink',
                    myColor.value = 'green',
                    isshow.value = true

            } else {
                //当鼠标移除的时候
                bgColor.value = 'white',
                    myColor.value = 'block'
                isshow.value = false

            }
        }


        const delTodo = () => {
            if (props.todo.isCompleted) {
                if (window.confirm('确定要删除吗')) {
                    props.deleteTodo(props.index)
                }
            }else{
                alert('你的任务还没有完成不能删除')
            }

        }

        const isComptete = computed({
            get() {
                return props.todo.isCompleted
            },
            set(val) {
                props.updateTodo(props.todo, val)
            }
        })

        return {
            delTodo,
            mouseHandler,
            bgColor,
            myColor,
            isshow,
            isComptete
        }
    },
})
</script>


<style scoped>
li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
}

li label {
    float: left;
    cursor: pointer;
}

li label input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
}

li button {
    float: right;
    /* display: none; */
    margin-top: 3px;
}

li:before {
    content: initial;
}

li:last-child {
    border-bottom: none;
}
</style>