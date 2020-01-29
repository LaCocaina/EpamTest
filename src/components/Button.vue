<template>
    <div :class="'button ' + type">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: "Button",
        props: ["type"],
        mounted() {
            this.$emit('toggle');
        }
    }
</script>

<style scoped>
    .button {
        padding: 10px 15px;
        margin-left: 10px;
        border-radius: 5px;
        text-align: center;
        cursor: pointer;
        transition: .5s filter ease-in-out;
    }
    .button:hover {
        filter: hue-rotate(-25deg);
    }
    .add {
        background: linear-gradient(36deg, #0052ff, #00ffdc);
        color: #FFF;
    }
    .can {
        background: linear-gradient(36deg, #ff00b4, #ff6000);
        color: #FFF;
    }
    .whi {
        background: #fff;
        color: #000;
        border: 1px solid #ccc;
    }
</style>