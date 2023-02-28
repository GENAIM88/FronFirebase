<template>

    <div class="fondo">

        <v-row class="renglon" >
        <nuxt />
    </v-row>

    </div>
    
</template>

<style scoped>
    .renglon{
        width: 100vw;
        height: 100vh;
        flex-direction: row;
        align-content: center;
        justify-content: center;
        align-items: center;
    }

    .fondo{
        background-image: url('../assets/images/fondo.jpg');
        background-repeat: no-repeat;
        background-size: cover;
        height: 102vh;
    }
</style>