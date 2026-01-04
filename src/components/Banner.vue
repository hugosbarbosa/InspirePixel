<script setup>
import fotografo from "../assets/fotografo.png";


</script>

<template>

    <section class="banner">

        <div class="text">
            <h1>
                Onde a paisagem <br> vira <span>inspiração</span> .
            </h1>
            <p>
                Explore paisagens, cores e luzes que inspiram novas histórias <br> através da fotografia.
            </p>
        </div>
        <img :src="fotografo" alt="Fotógrafo com câmera" />
    

    </section>

</template>

<style scoped lang="scss">
.banner {
    display: flex;
    justify-content: space-between;
    
    align-items: center; 

    margin: 2rem auto; 
    
    max-width: 1400px; 
    
    padding: 0 5%; 

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

        max-width: 482.84px; 
        height: 398.18px;
        object-fit: cover;
        border-radius: 60px 60px 60px 0; 
    }

}

@media (max-width: 768px) {
    .banner {
        // Inverte a ordem: Imagem vai pro topo, texto pro fundo
        flex-direction: column-reverse; 
        text-align: center; // Centraliza o texto
        margin: 2rem 1rem; // Margens menores para celular
        padding: 0; // Remove padding lateral excessivo

        .text {
            max-width: 100%; // Texto ocupa toda a largura
            padding-right: 0; // Remove o espaço lateral que tinha no desktop
            margin-top: 1.5rem; // Espaço entre a imagem e o texto
            
            h1 {
                font-size: 2rem; // Diminui um pouco a fonte
                
                span {
                    font-size: 3rem; // Ajusta proporcionalmente
                }
            }

            p{  
                font-size: 0.7rem; // Ajusta o tamanho da fonte do parágrafo
            }
        }

        img {
            margin-right: 0; // Remove margem lateral
            width: 100%; // Imagem full width
            max-width: 350px; // Limita para não ficar gigante
            height: auto; // Altura automática
            border-radius: 40px; // Arredondamento igual da referência mobile
        }
    }
}
</style>