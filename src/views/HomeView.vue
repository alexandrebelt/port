<template>
  <ProjetosScroll />
  <div class="lets-work-footer">
    <div class="lwfooter-col">
      <p>Hello! I'm an independent designer and developer enthusiastic about crafting ideas into memorable creations.
      </p>
    </div>
    <div class="lwfooter-col">
      <a @click="scrollBottom()">
        Let's work together?
      </a>
    </div>
  </div>
  <section class="contato">
    <div class="contato-wrapper">
      <div class="horizontal-page">
        <div class="lets-work-letter">
          <h1>
              Let's work together?
          </h1>
        </div>
      </div>
      <div class="horizontal-page">
        <FormComponent />
      </div>
    </div>

  </section>

</template>

<script>

import gsap from 'gsap'
import { defineComponent } from 'vue'
import ScrollTrigger from 'gsap/dist/ScrollTrigger'
import ProjetosScroll from '../components/home/ProjetosScroll.vue'
import FormComponent from '../components/home/FormComponent.vue'

gsap.registerPlugin(ScrollTrigger)

export default defineComponent({
  components: {
    ProjetosScroll,
    FormComponent
  },
  methods: {
    scrollBottom() {
      window.scrollTo(0,document.body.scrollHeight);
    }
  },
  mounted() {
    setTimeout(() => {
    const tl = gsap.timeline();
    gsap.set('#footer', {y:200,})
    gsap.from('.header', {
      y: 0
    })
    tl.to('.header', {
      y: -200,
      ease: 'power1',
      scrollTrigger: {
        trigger: "body",
        start: "top top",
        end: "+=1400",
        scrub: 0.5,
        markers: true,
      }
    })
    gsap.to('.lets-work-footer', {
      y: 200,
      ease: 'power1',
      scrollTrigger: {
        trigger: "body",
        start: "top top",
        end: "+=1400",
        scrub: 0.5,
        invalidateOnRefresh: true
      }
    })

    
      gsap.to('.contato-wrapper', {
        keyframes: {
          "0%": { x: 0 },
          "20%": { x: 0 },
          "100%": { x: '-100vw' }
        },
        ease: 'power1',
        scrollTrigger: {
          trigger: '.contato',
          start: 'center center',
          end: 'center top',
          pin: true,
          scrub: 2,
          invalidateOnRefresh: true
        }
      })
      gsap.to('body', {
        backgroundColor: '#202020',
        ease: 'power1',
        scrollTrigger: {
          trigger: '.contato',
          start: 'top bottom',
          end: 'center top',
          scrub: 2,
          invalidateOnRefresh: true
        }
      })
      gsap.set('#footer', {y:200,})
      gsap.to('#footer', {
        y:0,
        ease: 'power1',
        scrollTrigger: {
          trigger: 'body',
          start: '80% center',
          end: 'bottom bottom',
          scrub: 2,
          invalidateOnRefresh: true
        }
      })
      tl.to('.header', {
        keyframes: {
          "0%":{y:-200,},
          "100%":{y: 0,}
        },
        ease: 'power1',
        scrollTrigger: {
          trigger: 'body',
          start: '80% center',
          end: 'bottom bottom',
          scrub: 2,
          markers:true,
          invalidateOnRefresh: true
        }
      })
    }, 1000);
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
section {
  display: flex;
  height: 100vh;
  align-items: center;
}

.contato {
  color: var(--branco);
  height: 100vh;
  background-color: var(--preto);

  .horizontal-page {
    width: 100vw;
  }

  .contato-wrapper {
    align-self: baseline;
    width: 200vw;
    display: flex;
    justify-content: left;
    height: 100vh;
    align-items: center;
  }

  .lets-work-letter {
    align-items: center;

    h1 {
      transition: .1s;
      cursor: pointer;
      text-align: center;

      &:hover {
        font-weight: 400;

      }
    }
  }
}

.lets-work-footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  align-content: end;

  .lwfooter-col {
    text-align: right !important;
    a{
      font-size: max(13px, 1.2vw);
      
      &:hover{
        cursor:pointer;
      }
    }
    padding: 0 max(20px, 3vw) max(20px, 3vw);
    align-self: end;
    p{
      max-width: max(200px, 18vw);
    }
  }

  p {
    max-width: 16vw;
    text-align: left;
    font-weight: 500;
  }
}

h3 {
  margin: 40px 0 0;
}

a {
  color: var(--preto);
  transition: .3s;
  &:hover{
    color: var(--azul)
  }
}


</style>
