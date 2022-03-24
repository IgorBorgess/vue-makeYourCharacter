<template>
    <div id="main-banner"></div>
</template>

<script>
export default {
    name: "Banner"
}
</script>

<style scoped>
    #main-banner {
        /* background-image: url("/public/img/cover2.jpg"); */
        background-repeat: no-repeat;
        background-position: 0 -250px;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-banner h1 {
        color: #FFF;
        text-align: center;
        font-size: 60px;
        background-color: #222;
    }
</style>