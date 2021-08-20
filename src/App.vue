<template>
    <div class="total">
        <Navbar :pdf="pdf" :discordLink="links.discord"/>

        <section class="section">
            <h2 class="subtitle" v-html="slogan"></h2>
            <h2 class="title">{{unitTitle}} Help!</h2>
        </section>

        <section class="section list left-centered">
            <ul>
                <li>Are your labs taking way too long to finish?</li>
                <li>Do you get stuck on errors for hours at a time?</li>
                <li>Does it feel like you have no idea what you are doing?</li>
            </ul>
        </section>

        <Vim>
            <VimLine :row="1" :comment="commentStyle">Hi! My name is Sean and I worked in the Curtin Computing Deparment for 2 years as a Lab Tutor</VimLine>
            <VimLine :row="2">I love coding and I love teaching students to code!</VimLine>
            <VimLine :row="3">I offer private tutoring for {{ unitFull }} and other first year computing units</VimLine>
        </Vim>

        <Pricing :group="price.group" :indiv="price.indiv"/>

        <section class="section">
            <p>Flexible times. Price negotiable. Recurring or once-off sessions.</p>
            <p v-if="pdf">Book a Session at <b>tutor.dinkydie.me</b> or use the QR code:</p>
            <p><br/></p>
            <div v-if="!pdf" class="field">
                <div class="control">
                    <a class="button is-large is-primary" :href="links.form">Book Session</a>
                </div>     
            </div>
            <div v-else>
                <img :src="`/img/code-${unit}.png`">
            </div>
        </section>
    </div>
    
    <footer class="disclaimer has-text-grey has-background-light">
        <p>I am not affiliated with Curtin University.</p>
        <p>This {{ !pdf ? 'website' : 'poster'}} was created by me and is fully open source.
            <span v-if="!pdf">See the <a :href="links.source" target="blank">source code</a>.</span>
        </p>
    </footer>
</template>

<script scoped>
import Navbar from './components/Navbar.vue'
import Pricing from './components/Pricing.vue'
import Vim from './components/Vim.vue'
import VimLine from './components/VimLine.vue';
export default {
    name: 'App',
    data() {
        return {
            pdf: false,
            price: { group: 15, indiv: 25 },
            unit: null,
            unitTitle: null,
            commentStyle: null,
            unitFull: null,
            slogan: null,
            links: {
                source: "https://github.com/DinkyDieDingus/DinkyDieDingus.github.io",
                form: "https://forms.gle/nuHU6Y9BQFBscS8z6",
                discord: "https://discordapp.com/users/74115767930466304"
            }
        }
    },
    components: {
        Vim,
        Navbar,
        Pricing,
        VimLine
    },
    computed: {
        aboutMe() {
            return [
                {content:"Hi! My name is Sean and I worked in the Curtin Computing Deparment for 2 years as a Lab Tutor", comment: true},
                {content:"I love coding and I love teaching students to code!",comment: false},
                {content:`I offer private tutoring for ${this.unitFull} and other first year computing units`, comment: false},
            ]
        }
    },
    mounted() {
        document.title = 'Computing Tutor - Sean Spiegl'
        const urlParams = new URLSearchParams(window.location.search);
        this.unit = urlParams.get('unit');
        if (this.unit === null) {
            this.unit = 'other';
        }
        let data = require('./data/data.json')[this.unit];
        for (let prop of Object.keys(data)) {
            this[prop] = data[prop];
        }
        this.pdf = urlParams.has('pdf');
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  height: 100vh;
}

.navbar {
    margin-bottom: 2em;
}

.disclaimer {
    text-align: left;
    padding: 1em;
    width: 100%;
    font-style: italic;
    font-size: 0.8em;
}

.list {
    font-size: 1.3rem;
    list-style-type:circle;
}

.list > ul {
    list-style-type:circle;
}

.code {
    width: 5em;
    height: 5em;
}

.left-centered {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: left;
}

.padded {
    padding: 0 15% 0 15%;
}
</style>
