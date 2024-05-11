<template>
  <div id="footer">
    <div>
      <div class="footer-col">
        <a v-for="social in socials" :key="social.id" target="_blank" :href="social.link">
          {{ social.nome }}
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      socials: []
    }
  },
  mounted() {

      axios.get('socials.json')
        .then((response) => {
          this.socials = response.data;
          console.log(this.socials)
        })
  }
}
</script>

<style lang="scss">
#footer {
  position: fixed;
  width: 100vw;
  bottom: 0;

  .footer-col {
    a {
      margin: max(20px, 3vw);
    }

    width: 100%;
    display: flex;
    justify-content: space-between;

    a {
      mix-blend-mode: exclusion;
      filter: contrast(0) brightness(100);
      font-size: max(13px, 1.2vw);
      text-transform: uppercase;
    }
  }
}
</style>