<script setup>
import ApiFotos from './Api-fotos.vue';
</script>

<template>
    <div >
        <h4>Inspire-se</h4>
    </div>

    <div><ApiFotos/></div>

</template>

<style scoped lang="scss">
     div>h4 {
        text-align: left;
        margin-left: 150px;
        font-weight: normal;
        color: #333;
        font-size: 2.5rem;
    }

    @media (max-width: 768px) {
        div>h4 {
            margin-left: 20px;
            font-size: 2rem;
        }
    }

    @media (max-width: 1280px) {
        div>h4 {
            margin-left: 30px;
            font-size: 2rem;
        }
    }

</style>