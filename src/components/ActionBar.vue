<template lang="pug">
    .top-bar
        img.logo(src="./../assets/logo.svg")
        button(
            type="button" 
            @click="$emit('addNew')") Add New
</template>

<script>
export default {
    name: 'ActionBar'
}
</script>

<style lang="scss" scoped>
@import '../scss/vars';

.top-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 50px;
    padding: 0 26px;
    height: 100px;
    background: $clr-main;
    border-bottom-right-radius: 20px;
    border-bottom-left-radius: 20px;
    box-shadow: 0 1px 80px rgba(0, 0, 0, .06);

    .logo {
        width: auto;
        height: 40px;
    }

    button {
        position: relative;
        margin-top: 10px;
        padding-right: 45px;
        color: $white;
        line-height: 30px;
        font-size: 20px;
        font-family: $font-main;
        font-weight: 500;
        background: transparent;
        border: none;
        outline: 0;
        cursor: pointer;

        &::before {
            content: '+';
            position: absolute;
            top: -2px;
            right: 0;
            width: 30px;
            height: 30px;
            line-height: 30px;
            color: $white;
            font-size: 26px;
            font-weight: 600;
            background-color: transparent;
            transition: all .3s ease-in-out;
            border: 2px solid $white;
            border-radius: 50%;
        }

        &:hover {

            &::before {
                color: $clr-main;
                background-color: $white;
            }
        }
    }
}
</style>
