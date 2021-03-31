<template>
    <div class ="container">
        <button ><b>{{ value }}</b></button>
    </div>
</template>

<script>
    export default {
        props: {
            value: String,
        },
    }
</script>

<style scoped>

    button{
        background: #444;
        color: white;
        border: 0px;
        padding: 5px;
        border-radius: 5px;
        cursor: pointer;  
        display: inline-block;
        margin-right:40px;
        transition-duration: 0.3s;
        letter-spacing: 5px;
    }
    button:hover {
        background: white;
        color:  #444;
    }
    .container {
        display: inline-block;
        background: #444;
    }

</style>