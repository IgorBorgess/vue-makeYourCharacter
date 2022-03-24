<template>
    <div id="nav">
        <router-link to="/" id="logo-url">
            <img v-bind:src="logo" v-bind:alt="alt" id="logo">
        </router-link>
        <router-link to="/"><p>Home</p></router-link> 
        <router-link to="/orders"><p>Sheets</p></router-link>
        <router-link to="/summary"><p>Summary</p></router-link>
    </div>
</template>

<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"]
}
</script>

<style>
    #nav {
        background-color: #222;
        border-bottom: 4px solid #111;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-content: center;
    }

    #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }

    #logo {
        width: 40px;
        height: 40px;
    }

    #nav a {
        color: red;
        text-decoration: none;
        margin: 12px;
        transition: .5;
    }

    #nav a:hover {
        color: #FFF;
    }
</style>