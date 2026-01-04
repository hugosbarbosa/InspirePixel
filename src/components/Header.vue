<script setup>
import { ref } from 'vue';
import { Icon } from "@iconify/vue";
import logo from "../assets/logo.png"

const menuAberto = ref(false);

const toggleMenu = () => {
    menuAberto.value = !menuAberto.value;
}
</script>

<template>
<header>
    <img :src="logo" alt="Imagem da logo marca" class="logo">

    <div class="mobile-controls">
        <a href="#" class="search-icon-mobile"> 
            <Icon icon="line-md:search" class="icon-size-control"/>
        </a>
        
        <button class="hamburger-btn" @click="toggleMenu">
            <Icon 
                :icon="menuAberto ? 'line-md:close' : 'line-md:menu-fold-left'" 
                :key="menuAberto"
                class="menu-icon icon-size-control"
            />
        </button>
    </div>

    <nav :class="{ 'active': menuAberto }">
        <ul>
            <li class="desktop-only">
                <a href="#" class="search-icon"> 
                    <Icon icon="line-md:search" class="icon-size-control"/> 
                </a>
            </li>
            
            <li><a href="#">Início</a></li>
            <li><a href="#">Galeria</a></li>
            <li><a href="#">Favoritos</a></li>
            
            <li>
                <a href="#" class="conta-link"> 
                    <Icon icon="line-md:account" class="icon-desktop icon-size-control"/> 
                    
                    <span class="text-mobile">Conta</span>
                </a>
            </li>

        </ul>
    </nav>

</header>
</template>

<style scoped lang="scss">

/* --- AQUI ESTÁ A CORREÇÃO --- */
:deep(.icon-size-control) {
    font-size: 2.2rem;
    color: #e1306c; /* Adicionei a cor rosa aqui para forçar */
}

/* Controle da grossura (finura) */
:deep(.icon-size-control path),
:deep(.icon-size-control line),
:deep(.icon-size-control circle),
:deep(.icon-size-control rect) {
    stroke-width: 1.2 !important;
}
/* --------------------------- */

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 2rem 5%; 
    position: relative;
    z-index: 50; 

    .logo {
        max-width: 40px; 
    }
}

.mobile-controls {
    display: none; 
    align-items: center;
    gap: 15px;

    .search-icon-mobile {
        display: flex;
        text-decoration: none; 
    }

    .hamburger-btn {
        background: none;
        border: none;
        cursor: pointer;
        display: flex;
    }
}

nav {
    ul {
        list-style: none;
        display: flex;
        gap: 2rem;
        align-items: center;

        li a {
            text-decoration: none;
            color: black;
            font-weight: 500;
            display: flex;
            align-items: center;
            font-size: 1.1rem;
            transition: color 0.3s;

            &:hover { color: #e1306c; }
        }

        .search-icon {
            display: flex;
        }

        .conta-link {
            .text-mobile {
                display: none; 
            }
            .icon-desktop {
                display: block;
            }
        }
    }
}

// --- MEDIA QUERY (CELULAR) ---
@media (max-width: 768px) {
    
    .mobile-controls {
        display: flex; 
    }

    .desktop-only {
        display: none;
    }

    nav {
        position: absolute;
        top: 60px; 
        right: 0;
        background: white;
        width: 200px; 
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        
        opacity: 0;
        visibility: hidden;
        transform: translateY(-20px); 
        transition: all 0.3s ease;

        &.active {
            opacity: 1;
            visibility: visible;
            transform: translateY(0);
        }

        ul {
            flex-direction: column; 
            align-items: flex-start; 
            gap: 1.5rem;

            .conta-link {
                .icon-desktop {
                    display: none; 
                }
                .text-mobile {
                    display: block; 
                }
            }
        }
    }
}
</style>