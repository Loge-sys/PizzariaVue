<template>
    <div id="main-banner">
        <h1>Loge's Pizzeria</h1>
    </div>
</template>

<script>
export default {
    name: 'Banner'
}
</script>

<style scoped>
    #main-banner{
        background-image: url('../../public/img/pizzaria.jpg');
        background-position: 0 -300px;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }
    #main-banner h1 {
        color: #fff;
        text-align: center;
        font-size: 60px;
        margin-left: 20px;
    }
</style>