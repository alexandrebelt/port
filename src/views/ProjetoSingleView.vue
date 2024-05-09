<template>
    <div class="projeto-single-container">
        <div class="projeto-info">
            <div class="col-projeto">
                <h4>
                    {{ infos.name }}
                </h4>
                <p>
                    {{ descricao }}
                </p>
                <a :href=link>View site</a>
            </div>
            <div class="col-projeto">
                <img :src="infos.image" />
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import ScrollTrigger from 'gsap/dist/ScrollTrigger';

export default {
    props: ['projetoNome'],
    data() {
        return {
            descricao: "bla bla bal balbalbal bla balbalbal blabalbalbal blabalbalbal blabalbalbal bla balbalbal bla balbalbal blabalbalbal bla",
            link: '#',
            infos: []
        }
    },
    mounted() {
        axios.get(`https://rickandmortyapi.com/api/character?name=${this.projetoNome.replace(/-/g, ' ')}`)
            .then((response) => {
                this.infos = response.data.results[0]
                console.log(this.infos)
            }).catch((error) => {
                console.log(error)
            })

        ScrollTrigger.killAll()
    },
    beforeRouteEnter() {

    }
}
</script>

<style lang="scss">
.projeto-single-container {

    padding: 12vw 3vw 0vw;

    .projeto-info {
        display: flex;
        flex-direction: row;
        column-gap: max(20px, 3vw);
        .col-projeto {
            display:flex;
            flex-direction: column;
            align-self:start;
            text-align: left;
            row-gap: max(20px, 3vw);
            h4{
                font-weight: 500;
                margin: 0;
                line-height: .6em;
            }
            p{
                margin: 0;
            }
            img {
                width: 100%;
                aspect-ratio: 3/2;
                object-fit: cover;
            }
            a{
                font-weight: 500;
                text-transform: uppercase;
                text-decoration: underline;
                color: var(--preto);
                font-size: max(13px, 1.2vw);
            }
        }

        :nth-of-type(1) {
            flex-basis: 40%;
        }

        :nth-of-type(2) {
            flex-basis: 60%;
        }
    }
}
</style>