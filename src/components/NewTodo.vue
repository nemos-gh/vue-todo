<template lang="pug">
    .new-todo(@click.self="hide")
        input(
            id="new-todo"
            @keyup.enter="sendTodo"
            @keyup.esc="hide"
            placeholder="Type and hit Enter"
            autofocus)
        p.msg-quit Esc to Quit
</template>

<script>
export default {
    name: 'NewTodo',
    mounted() {
        document.getElementById('new-todo').focus();
    },
    methods: {
        sendTodo(el) {
            this.$emit('addTodo', el);
            el.target.value = '';
        },
        hide() {
            this.$emit('hidePanel');
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../scss/vars';

.new-todo {
    display: flex;
    flex-flow: column wrap;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: rgba($black, .85);
    
    input {
        margin: -240px 0 40px;
        padding: 50px 60px;
        width: 700px;
        height: 45px;
        font-size: 30px;
        font-family: $font-main;
        text-align: center;
        border: 0;
        border-radius: 100px;
        outline: 0;
        resize: none;

        &::placeholder {
            color: $gray;
            opacity: 1;
        }
    }

    .msg-quit {
        color: $white;
        font-size: 12px;
        font-family: $font-main;
        text-transform: uppercase;
        text-align: center;
        letter-spacing: 1px;
        word-spacing: 2px;
    }
}
</style>
