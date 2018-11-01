<template lang="pug">
    .todo-item(:class="{done: done}" @click="isDone")
        p.item-text {{todo.text}}
        button.item-remove(@click.stop="getId")
        .item-check
</template>

<script>
export default {
    name: 'TodoItem',
    props: {
        todo: {}
    },
    data() {
        return {
            done: false
        }
    },
    methods: {
        isDone() { this.done = !this.done },
        getId () {
            this.$emit('remove-item', this.todo.id)
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../scss/vars';

.todo-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px 30px 30px 40px;
    background: transparent;
    transition: all .2s ease-in-out;

    // Text content
    .item-text {
        position: relative;
        color: $black;
        font-size: 20px;
        font-family: $font-main;
        letter-spacing: .02rem;
        word-spacing: .02rem;

        &::before {
            content: '';
            display: block;
            position: absolute;
            top: 50%;
            left: 0;
            width: 0;
            height: 2px;
            background-color: rgba($clr-main, .4);
            transition: width .4s;
        }
    }

    // Check Todo button
    .item-check {
        position: relative;
        display: block;
        margin: 0;
        padding: 0;
        width: 20px;
        height: 20px;
        border: 2px solid $gray;
        border-radius: 50%;
        overflow: hidden;
        cursor: pointer;

        &::before {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            background: $clr-main;
            transition: all .2s;
            box-shadow: inset 0 0 0 10px $white;
            border-radius: 50%;
        }
    }

    // Remove Todo button
    .item-remove {
        visibility: hidden;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 20px 0 auto;
        width: 20px;
        height: 20px;
        opacity: 0;
        transform: rotate(0deg);
        transform-origin: center center;
        transition: all .5s ease-in-out;
        background: transparent;
        border: 3px solid transparent;
        border-radius: 50%;
        outline: 0;
        overflow: hidden;
        cursor: pointer;

        &::before {
            @extend %cross;
            transform: rotate(45deg);
        }

        &::after {
            @extend %cross;
            transform: rotate(-45deg);
        }
    }

    // Mark Todo done
    &.done {
        background: rgba($clr-light, .5);

        &:hover {

            .item-remove {
                visibility: visible;
                opacity: .7;
                transform: rotate(180deg);
                transition: all .3s ease-in-out;

                &:hover {

                    &::before,
                    &::after { background: $clr-main; }
                }
            }
        }

        .item-text {
            color: rgba($black, .3);

            &::before {
                width: 100%;
            }
        }

        .item-check {

            &::before {
                box-shadow: inset 0 0 0 3px $white;
            }
        }
    }

    // cross btn partial
    %cross {
        content: '';
        position: absolute;
        display: block;
        width: 30px;
        height: 2px;
        background: $black;
    }
}
</style>
