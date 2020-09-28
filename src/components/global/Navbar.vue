<template>
    <div class="navbar">
        <h1>Sweepy's Challenge</h1>
    </div>
</template>

<script>
    export default {
        name: "Navbar"
    }
</script>

<style lang="scss" scoped>
    .navbar {
        background: rgb(131,58,180);
        background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%);

        display: flex;
        justify-content: flex-start;
        box-shadow: 2px 2px 5px #e1e2e3;
    }

    .navbar h1 {
        padding: 0 15px;
        color: #fff;
        font-family: 'Roboto', sans-serif;
        font-weight: 900;
        font-style: italic;
    }
</style>
