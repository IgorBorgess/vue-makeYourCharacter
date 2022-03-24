<template>
    <footer id="footer">
        <p>Make Your Character &copy; 2021</p>
    </footer>
</template>

<script>
export default {
    name: "Footer"
}
</script>

<style>
    #footer {
        height: 200px;
        background-color: #222;
        border-top: 4px solid #111;
        color: red;
        display: flex;
        align-items: center;
        justify-content: center;
        /* position: absolute; */
        bottom: 0;
        width: 100%;
    }
</style>