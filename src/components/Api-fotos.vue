<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';
import { Icon } from "@iconify/vue";

const fotos = ref([]);
const page = ref(1);
const loading = ref(false);
const sentinela = ref(null);

const fetchFotos = async () => {
    if (loading.value) return; 

    loading.value = true;

    try {
        const response = await axios.get(`https://picsum.photos/v2/list?page=${page.value}&limit=30`);
        const rawData = response.data;

        // --- CORREÇÃO AQUI ---
        const novasFotos = rawData.map(photo => {
            const isTall = photo.id % 2 === 0; 
            const height = isTall ? 900 : 720; 

            return { 
                id: photo.id,
                author: photo.author,
                customUrl: `https://picsum.photos/id/${photo.id}/600/${height}`
            }
        });
        // ---------------------

        fotos.value = [...fotos.value, ...novasFotos];
        page.value++;

    } catch (error) {
        console.error('Erro ao buscar fotos:', error);
    } finally {
        loading.value = false;
    }
}

const toggleLike = (foto) => {
    foto.liked = !foto.liked;
}

onMounted(() => {
    fetchFotos();
    
    const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) fetchFotos();
    }, { rootMargin: '100px' });

    if (sentinela.value) observer.observe(sentinela.value);
});
</script>

<template>
  <div class="masonry-container">
    
    <div v-for="foto in fotos" :key="foto.id" class="pin">
      
      <img :src="foto.customUrl" :alt="foto.author" loading="lazy">
      
      <button class="like-btn" @click.stop="toggleLike(foto)">
        <Icon 
            :icon="foto.liked ? 'material-symbols:favorite' : 'material-symbols:favorite-outline'" 
            :class="{ 'liked': foto.liked }"
        />
      </button>

      <div class="author-info">
        <p>{{ foto.author }}</p>
      </div>

    </div>

  </div>

  <div ref="sentinela" class="loading-trigger">
    <p v-if="loading">Carregando mais inspirações...</p>
  </div>
</template>

<style scoped lang="scss">
.masonry-container {
  
  column-count: 4; 
  column-gap: 24px; // Espaço entre as colunas
  padding: 20px;
  max-width: 1280px;
  margin: 0 auto;

  // Responsividade (muda colunas conforme a tela diminui)
  @media (max-width: 1200px) { column-count: 4; }
  @media (max-width: 900px) { column-count: 3; }
  @media (max-width: 600px) { column-count: 2; }
}

.pin {
  break-inside: avoid; 
  margin-bottom: 24px; // Espaço vertical entre os pins
  border-radius: 16px;
  overflow: hidden; // Para o zoom não sair da borda
  background-color: #d2d1d1; // Cor de fundo enquanto carrega
  position: relative;
  cursor: zoom-in;
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-4px); // Leve subida ao passar o mouse
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
    
    // Mostra o autor apenas quando passa o mouse
    .author-info {
      opacity: 1; 
    }
  }

 

  img {
    width: 100%; // Ocupa toda a largura da coluna
    display: block; // Remove espaços extras
    border-radius: 24px;
  }

  .author-info {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    background: linear-gradient(transparent, rgba(0,0,0,0.8));
    color: white;
    padding: 20px 10px 10px;
    opacity: 0; // Começa invisível
    transition: opacity 0.3s ease;
    
    p {
      margin: 0;
      font-size: 0.9rem;
      font-weight: 600;
    }
  }
}


.loading-trigger {
  text-align: center;
  padding: 20px;
  width: 100%;
  clear: both; // Garante que fique abaixo do grid
  color: #666;
  font-weight: bold;
}

.like-btn {
    position: absolute;
    top: 15px;    // Distância do topo
    right: 15px;  // Distância da direita
    
    background: transparent; // Fundo transparente
    border: none;
    cursor: pointer;
    z-index: 10; // Garante que fique em cima da imagem
    
    // Tamanho do ícone
    font-size: 1.8rem; 
    color: white; // Cor padrão (borda branca)
    
    // Sombra para garantir que dê para ver o coração branco mesmo se a foto for clara
    filter: drop-shadow(0 2px 4px rgba(0,0,0,0.3));
    
    transition: transform 0.2s;

    &:hover {
      transform: scale(1.2); // Aumenta um pouco ao passar o mouse
    }

    // Quando o coração está ativo (classe que colocamos no template)
    .liked {
      color: #E1306C; // Rosa/Vermelho do Instagram/Pinterest
      // Remove a sombra preta para ficar "brilhante" ou mantém, gosto pessoal
      filter: drop-shadow(0 2px 4px rgba(225, 48, 108, 0.3));
    }
  }

    
</style>