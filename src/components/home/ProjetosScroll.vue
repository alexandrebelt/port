<template>
    <div class="projects-wrapper">
        <ul class="projects-list">
            <div class="li-wrapper">
                <li class="projeto-item" v-for="proj in projetos" :key="proj.id">
                    <router-link
                        :to="{ name: 'Projeto', params: { projetoNome: proj.name.replace(/\s+/g, '-').toLowerCase() } }">
                        <img class="projeto-thumb" :src="proj.image" :alt="proj.name">
                    </router-link>
                    <div class="hovertext" id="dialog-label">
                        <p>{{ proj.name }}</p>
                    </div>
                </li>
            </div>
        </ul>
    </div>
</template>

<script>
import axios from 'axios'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/dist/ScrollTrigger'
import $ from 'jquery'
gsap.registerPlugin(ScrollTrigger);

export default {

    data() {
        return {
            projetos: []
        }
    },
    mounted() {
        $(".li-wrapper").mousemove(function (e) {

            // Select hovertext element within gallery cell

            this.$popup = $(this).find(".hovertext").first();

            // Get offset from top
            var eTop = $(this).offset().top;
            var eLeft = $(this).offset().left;

            var x = e.pageX + 20;
            var y = e.pageY + 20;

            // Set CSS
            $(this).find(".hovertext").css({ top: y - eTop, left: x - eLeft });

        });
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
.hovertext {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 100;
    overflow: hidden;
    white-space: nowrap;
}

.projeto-item .hovertext {
    visibility: hidden;
}

.projeto-item:hover .hovertext {
    visibility: visible;
}

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
        position: relative;
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
    position: relative;
    display: flex;
    padding: 0 4vw;
}

#dialog-label {
    position: fixed;
    background-color: var(--branco) !important;
    padding: 1vw;
    border: 1px solid var(--preto);

    p {
        font-size: max(15px, 1vw) !important;
        text-transform: uppercase;
        letter-spacing: 0.1vw
    }
}

@media (max-width: 800px) {
    .submit-form {
        transform: translatey(19px);
    }
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

    .projeto-info {
        flex-direction: column-reverse !important;
        flex-basis: 100% !important;
        row-gap: 3vw;

        .col-projeto {
            width: 100%;
        }
    }

}
</style>