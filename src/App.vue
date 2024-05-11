<template>
  <HeaderComponent />
  <router-view v-slot="{ Component }">
    <transition name="fade">
      <component :is="Component" />
    </transition>
    <FooterComponent/>
  </router-view>
</template>
<script>
import LocomotiveScroll from 'locomotive-scroll'
import HeaderComponent from './components/HeaderComponent.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  components: {
    HeaderComponent,
    FooterComponent
  },
  
  mounted() {
    /* eslint-disable */
    const locomotiveScroll = new LocomotiveScroll();
    /* eslint-enable */
  },
}
</script>
<style lang="scss">
@font-face {
  font-family: 'Cotford Var', serif;
  src: url('./assets/fonts/CotfordVar/CotfordVar.ttf') format('truetype');
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Thin.otf') format('opentype');
  font-weight: 100;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-ExtLt.otf') format('opentype');
  font-weight: 200
}
/*teste */

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Light.otf') format('opentype');
  font-weight: 300;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-SemLt.otf') format('opentype');
  font-weight: 400;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Reg.otf') format('opentype');
  font-weight: 500;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Medium.otf') format('opentype');
  font-weight: 600;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Bold.otf') format('opentype');
  font-weight: 700;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Black.otf') format('opentype');
  font-weight: 800;
}


:root {
  --azul: #485CC7;
  --preto: #202020;
  --branco: #f5f5f5;

  --cotford: 'Cotford Var', serif;
  --neue: 'Neue Haas Grotesk Display', sans-serif;
}

* {
  margin: 0;
  padding: 0;
}
html,body{
  overflow-x: hidden;
}
body {
  background-color: var(--branco);
  font-weight: 500;
  overflow-x: hidden;


  a {
    text-decoration: none;

  }
}
p{
  font-size: max(13px, 1.2vw);
}
#app {
  font-family: var(--neue);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: var(--preto);
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: var(--cotford);
}

h1 {
  font-size: max(1.5em, 7vw);
  margin-top: 1vw;
  margin-bottom: 3vw;
  font-weight: 300;
}

h3 {
  font-size: max(1.5em, 6vw);
  margin-top: 1vw;
  margin-bottom: 3vw;
  font-weight: 200;

  strong {
    font-weight: 500 !important;
  }
}

h4 {
  font-size: max(1.2em, 4vw);
  margin-top: 1vw;
  margin-bottom: 3vw;
  font-weight: 200;
}
</style>
