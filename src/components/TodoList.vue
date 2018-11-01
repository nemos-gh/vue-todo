<template lang="pug">
    ul
        li(
            v-for="todo in todos" 
            :key="todo.id") 
                TodoItem(
                    :todo="todo"
                    @remove-item="removeItem")
</template>

<script>
import TodoItem from './TodoItem'

export default {
    name: 'TodoList',
    components: {
        TodoItem
    },
    props: {
        todos: Array
    },
    methods: {
        removeItem(id) {
            this.$emit('remove-todo', id)
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../scss/vars';

ul {
    margin: 0;
    padding: 0;
    box-shadow: 0 0 80px rgba($black, .04);
    counter-reset: todo-order;

    li {
        position: relative;
        background-color: $white;
        border-bottom: 1px solid rgba($gray, .4);
        overflow: hidden;

        &::before {
            counter-increment: todo-order;
            content: counter(todo-order);
            position: absolute;
            top: 5px;
            left: 15px;
            color: rgba($gray, .25);
            font-size: 80px;
            font-family: $font-main;
            font-weight: 700;
            letter-spacing: -10px;
        }

        &:last-child {
            border: 0;
        }
    }
}
</style>