<template>
    <div class="projects-wrapper">
        <ul class="projects-list">
            <div class="li-wrapper">
                <li v-for="proj in projetos" :key="proj.id">
                    <router-link
                        :to="{ name: 'Projeto', params: { projetoNome: proj.name.replace(/\s+/g, '-').toLowerCase() } }">
                        <img :src="proj.image" :alt="proj.name">
                    </router-link>
                </li>
            </div>
        </ul>
    </div>
</template>

<script>
import axios from 'axios'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/dist/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger);

export default {

    data() {
        return {
            projetos: []
        }
    },
    mounted() {
        axios.get("https://rickandmortyapi.com/api/character").
            then((response) => {
                this.projetos = response.data.results.slice(0, 7)
            }).catch((error) => {
                console.log(error)
            })
        setTimeout(() => {
            const projs = document.querySelector('.projects-list');
            function getScrollAmount() {
                let projsWidth = projs.scrollWidth;
                return -(projsWidth - window.innerWidth)
            }

            const tween = gsap.to(projs, {
                x: getScrollAmount,
                duration: 3,
                ease: "none",
            })

            ScrollTrigger.create({
                trigger: ".projects-wrapper",
                start: "center center",
                end: () => `+=${getScrollAmount() * -2}`,
                pin: true,
                animation: tween,
                scrub: 1,
                invalidateOnRefresh: true
            })
        }, 100);
    },
}
</script>

<style lang="scss">
.projects-wrapper {
    position: fixed !important;
    top: 50% !important;
    right: 50% !important;
    transform: translatey(-50%) !important;
    padding: 2vw;

}

.projects-list {
    display: flex;
    flex-wrap: no-wrap;
    width: fit-content;
    list-style-type: none;
    padding: 0;


    li {
        display: inline-block;
        list-style: none;
        margin: 0 10px;
        width: 35vw;
        max-width: unset;

        img {
            width: 100%;
            aspect-ratio: 10/6;
            object-fit: cover;
            border-radius: 10px;
        }
    }

}

.li-wrapper {
    display: flex;
    padding: 0 4vw;
}

@media (max-width: 700px) {
    
  .projects-wrapper {
      height: 50vh !important;
      max-height: 100vh !important;
    }
    
    .li-wrapper {
        li {
            width: 50vw !important;
            height: 50vh !important;
            
            img {
                height: 100% !important;
      }
    }
  }
}
</style>