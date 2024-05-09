<template>
    <div class="header">
        <div class="header-col">
            <h3>A<strong>B</strong></h3>
        </div>
        <div class="header-col">
            <nav>
                <router-link to="/">Home</router-link>
                <router-link to="/about">Contact</router-link>
            </nav>
        </div>

    </div>
</template>

<script>
import gsap from 'gsap'
import ScrollTrigger from 'gsap/dist/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger)

export default {
    mounted() {

    }
}
</script>

<style lang="scss">
.header {
    z-index: 10;
    position: fixed;
    display: flex;
    justify-content: space-between;
    top: 0;
    color:var(--branco);
    width: 100%;
    flex-direction: row;
    align-content: end;
    mix-blend-mode: difference;


    .header-col {
        align-self: end;
        padding: max(20px, 3vw) max(20px, 3vw);
    }

    h3 {
        line-height: 0.9em;
    }

    nav {
        display: flex;
        margin-top: 1vw;
        margin-bottom: 3vw;
        gap: max(20px, 4vw);



        a {
            font-weight: bold;
            color: var(--branco);
            text-transform: uppercase;
            font-weight: 500 !important;
            font-size: max(13px, 1.2vw);
            mix-blend-mode: difference;


            &.router-link-exact-active {

            }
        }
    }
}
</style>