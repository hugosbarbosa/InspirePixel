
<script setup>
import { Icon } from "@iconify/vue";
import logo from "../assets/logo.png"

</script>

<template>

<header>
    <img :src="logo" alt="Imagem da logo marca">

    <nav>
        <ul>
            <li>
                <a href="#" class="search-icon">  <Icon icon="material-symbols:search"/>
                    <!---->
            
                </a>
            </li>
            <li>
                <a href="#"> Início
                </a>
            </li>
            <li>
                <a href="#"> Galeria </a>
            </li>
            <li>
                <a href="#"> Favoritos</a>
            </li>
            <li>
                <a href="#" class="person-icon"> <Icon icon="material-symbols:person-outline"/>  </a>
            </li>
        </ul>
    </nav>

</header>


</template>

<style scoped lang="scss">

header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    margin: 2rem;
}
ul{
    list-style: none;
    display: flex;
    gap: 1.5rem;
}

.search-icon, .person-icon {
    font-size: 1.5rem;
    justify-content: center;
}

ul > li > a {
    text-decoration: none;
    color: black;
    align-items: center;
    
}



</style>

