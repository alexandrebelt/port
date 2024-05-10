<template>
    <div id='#contato'>

        <form ref="form" id="contact-form" @submit.prevent="sendEmail">
            <div v-if="formActive" class="form-content">
                <input required class="form-field" type="text" name="from_name" placeholder="Your name" />
                <hr class="form-hr">
                <input required class="form-field" type="email" name="reply_to" placeholder="Your E-mail " />
                <hr class="form-hr">
                <textarea required class="form-field" name="message"
                    placeholder="Tell me more about your project."></textarea>
                <hr>
                <button type="submit" class="submit-form">
                    <div class="loading-icon" v-if="isLoading">
                        <img src="#" alt="enviar" />
                    </div>
                    <div class="enviar-label" v-else>
                        <img src="#" alt="send" />
                    </div>
                </button>
            </div>
            <div v-if="mensagemSucesso">
                <h3><span>Obrigado!</span> I´ll be in touch as soon as possible! :)</h3>
            </div>
            <div v-if="mensagemErro">
                <h3><span>Ops! </span>Something went wrong, try again later :(</h3>
            </div>
        </form>
    </div>
</template>
<script lang="js">
import { defineComponent } from 'vue'
import emailjs from '@emailjs/browser'


export default defineComponent({
    data() {
        return {
            isLoading: false,
            formActive: true,
            mensagemErro: false,
            mensagemSucesso: false,

        }
    },
    methods: {
        sendEmail() {
            if (this.$refs.form === null) return;
            this.isLoading = true;

            emailjs.sendForm('service_g9jobfd', 'template_8bn97wn', this.$refs.form, {
                publicKey: 'MSPIUEWF69QcjnYel'
            })

                .then(
                    () => {
                        this.mensagemSucesso = true;
                        console.log('SUCCESS!');
                        this.formActive = false;
                        this.isLoading = false;
                    },
                    (error) => {
                        this.mensagemErro = true;
                        console.log('FAILED...', error.text);
                        this.isLoading = false;
                        this.formActive = false;
                    },
                );
        }

    }
})
</script>

<style lang="scss">
.form-field {
    background: none;
    border: none;
    font-family: var(--cotford);
    font-size: max(20px, 3vw);
    font-weight: 200;
    resize: none
}

.form-field::placeholder {
    font-weight: 300;
    opacity: 1;
    color: var(--branco);
}

.form-field:focus-visible {
    outline: none;
}


button {
    background: var(--branco);
    border: 1px solid var(--branco);
    height: max(40px, 5vw);
    width: max(40px, 5vw);
    border-radius: 50%;
    position: absolute;
    right: -1vw;
    bottom: 0;
    transform: translatey(2.4vw);
    cursor: pointer;

    &:hover {
        background: var(--preto);

        img {
            filter: invert(100%);
        }
    }

    img {
        //width: 0.5vw;
        transition: 1s;
        display: flex;
        margin: 0 auto;
    }

    .loading-icon {
        img {
            width: 2vw;
            animation-name: spin;
            animation-duration: 500ms;
            animation-iteration-count: infinite;
            animation-timing-function: linear;
            animation-direction: reverse;
        }
    }
}


@keyframes spin {
    from {
        transform: rotate(0deg);
    }

    to {
        transform: rotate(360deg);
    }
}


.form-hr {
    width: 3vw;
    margin: 0.4vw 0 1.2vw;
    opacity: 0.3;
}

textarea {
    padding-bottom: 2vw;
}



#contact-form {
    width: 66vw;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    max-width: 70vw;

    h3 {
        text-align: center !important;

        span {
            font-weight: 500;
        }
    }

    .form-content {
        position: relative;

        .enviar-label {
            display: flex;
            justify-content: center;
        }

        .form-field {
            width: 100%;
            color: var(--branco);
        }

        textarea {
            width: 100%;
        }

        hr:nth-of-type(3) {
            width: 100%;
            margin: 0;
        }
    }
}
</style>