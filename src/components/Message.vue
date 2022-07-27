<template>
    <div class="message-container">
        <p>{{msg}}</p>
    </div>
</template>

<script>
export default {
    name: 'Message',
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container{
        color: #2C6F1D;
        background-color: #B1FCA0;
        border: 2px solid #98E786;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
    }

</style>