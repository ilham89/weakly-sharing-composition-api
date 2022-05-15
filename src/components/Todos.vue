<template>
    <div class="hello">
        <ul>
            <li v-for="(todo, index) in todos" :key="index" class="list">
                <div v-if="!todo.isDone">{{ todo.name }} -</div>
                <s v-else> {{ todo.name }} - </s>
                <button @click="isDone(index)" class="button">
                    {{ todo.isDone ? "undone" : "done" }}
                </button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "Todos",
    props: {
        todos: Array,
    },
    methods: {
        isDone(index) {
            this.$emit("isDone", index);
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list {
    display: flex;
    align-items: center;
}
.button {
    margin-left: 8px;
}
</style>
