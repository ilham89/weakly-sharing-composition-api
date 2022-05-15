<template>
    <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- 
    <div>Ini state dari option API: {{ count }}</div>
    <button @click="addCount">tambah option</button>

    <div>Ini state dari Composition API: {{ counter }}</div>
    <button @click="addCounter">tambah Composition</button> -->
    <h4>
        <b>Todo List</b>
    </h4>
    <div class="container">
        <div>
            <input
                v-model="inputOption"
                placeholder="Tambah dengan option API"
            />
            <button @click="addTodos">tambah option</button>

            <Todos :todos="todos" @isDone="updateTodo" />
        </div>
        <div>
            <input
                v-model="inputComposition"
                placeholder="Tambah dengan composition API"
                v-on:keyup.enter="addTodoList"
            />
            <button @click="addTodoList">tambah composition</button>
            <Todos
                :todos="todosComposition.list"
                @isDone="updateTodoComposition"
            />
        </div>
    </div>
</template>

<script>
import { reactive, ref } from "@vue/reactivity";
// import HelloWorld from './components/HelloWorld.vue'
import Todos from "./components/Todos.vue";

export default {
    name: "App",
    components: {
        // HelloWorld
        Todos,
    },
    // Option API
    data() {
        return {
            count: 0,
            inputOption: "",
            todos: [],
        };
    },
    methods: {
        addCount() {
            this.count++;
        },

        addTodos() {
            this.todos.push({
                id: this.todos.length + 1,
                name: this.inputOption,
                isDone: false,
            });
        },

        updateTodo(index) {
            this.todos[index].isDone = !this.todos[index].isDone;
        },
    },

    // Composition API
    setup() {
        const counter = ref(0);
        const inputComposition = ref("");
        const todosComposition = reactive({
            list: [],
        });

        const addCounter = () => {
            counter.value++;
        };

        const addTodoList = () => {
            todosComposition.list.push({
                id: todosComposition.list.length + 1,
                name: inputComposition.value,
                isDone: false,
            });
        };

        const updateTodoComposition = (index) => {
            todosComposition.list[index].isDone =
                !todosComposition.list[index].isDone;
        };

        return {
            counter,
            addCounter,
            inputComposition,
            addTodoList,
            todosComposition,
            updateTodoComposition,
        };
    },
};
</script>

<style>
.constainer {
    display: flex;
}
</style>
