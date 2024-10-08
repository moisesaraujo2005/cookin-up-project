<template>
 
    <header class="banner">
     <div class="aprensetacao">
       <img src="../assets/imagens/logo.svg" alt="logo cookin" class="logo">
   
       <p class="cabecalho-lg frase-cabelhaco">
         <span class="texto-verde">A feast of ideas for</span>
         awaken the chef in you!
       </p>
   
       <p class="subtitulo-lg">
        Explore new recipes every day with ingredients at your fingertips
       </p>
     </div>
     <img src="../assets/imagens/foto-banner.png" alt="" class="foto-banner">
    </header>
       
   </template>
   
   <script >
   
   export default {
     name: 'App',
     components: {
   
     }
   }
   </script>
   
   <style scoped>
   .banner {
     padding: 4rem 7.5rem;
     color: var(--creme);
   
     display: flex;
     justify-content: space-between;
     align-items: center;
     column-gap: 3.25rem;
   }
   
   .logo {
     height: 4.5rem;
     margin-bottom: 3rem;
   }
   
   .frase-cabecalho {
     margin-bottom: 2rem;
   }
   
   .texto-verde {
     color: var(--verde-medio, #3D6D4A);
   }
   
   .foto-banner {
     width: 35rem;
   }
   
   @media only screen and (max-width: 1300px) {
     .banner {
       padding: 4rem 3.75rem;
       flex-direction: column;
       align-items: center;
       gap: 1rem;
     }
   
     .logo {
       display: block;
       margin-left: auto;
       margin-right: auto;
     }
   }
   
   @media only screen and (max-width: 767px) {
     .banner {
       padding: 4rem 1.5rem;
     }
   
     .foto-banner {
       width: min(100%, 21.25rem);
     }
   }
   </style>
   