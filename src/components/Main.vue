<template>
    <div id="main">
        <Books></Books>
    </div>
</template>

<script>
    import Books from "@/components/Books/Books";

    export default {
        name: "Main",
        components: {Books}
    }
</script>

<style scoped>
    #main {
        margin: 15px;
        width: 100%;
    }
</style>