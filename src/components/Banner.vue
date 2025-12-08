<script setup>
import fotografo from "../assets/fotografo.png";


</script>

<template>

    <section class="banner">

        <div class="text">
            <h1>
                Onde a paisagem vira <span>inspiração</span> .
            </h1>
            <p>
                Explore paisagens, cores e luzes que inspiram novas histórias através da fotografia.
            </p>
        </div>
        <img :src="fotografo" alt="Fotógrafo com câmera" />
    

    </section>

</template>

<style scoped lang="scss">

.banner {
    display: flex;
    justify-content: space-between;
    margin: 2rem;

    h1 {
        font-size: 3rem;
        margin-bottom: 1rem;

        span {
            font-size: 4.5rem;
            color: #E1306C;
        }
    }

   .text {
        max-width: 50%;
    }

    img {
        margin-right: 2rem;
        max-width: 482.84px; 
        height: 398.18px;
        object-fit: cover;
    }

}



</style>