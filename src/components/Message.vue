<template>
    <div class="message-conatiner">
        <p>{{msg}}</p>
    </div>
</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String,
    }
}

</script>

<style scoped>
    .message-conatiner{
        color: #2010ff;
        background-color: rgb(184, 241, 241);
        border: 2px solid rgb(135, 216, 216);
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
    }
</style>
