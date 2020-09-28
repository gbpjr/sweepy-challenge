<template>
    <a href="#" class="btn"><i class="fas fa-trash-alt"></i></a>
</template>

<script>
export default {
    name: "DeleteButton",
    props: {
    },
}
</script>

<style lang="scss" scoped>
    .btn {
        display: flex;
        justify-content: center;
        align-items: center;
        background: rgb(251,63,63);
        background: linear-gradient(circle, rgba(251,63,63,1) 0%, rgba(252,70,107,1) 100%);
        position:fixed;
        width:60px;
        height:60px;
        bottom:40px;
        right:40px;
        color:#FFF;
        border-radius:50px;
        box-shadow: 2px 2px 3px #999;
    }
</style>