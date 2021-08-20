<template>
    <div class="total">
        <nav class="navbar is-primary" role="navigation" aria-label="main navigation">
            <div class="navbar-brand">
                <a class="navbar-item">
                    <figure class="image">
                        <img class="is-rounded" src="./assets/binky.png">
                    </figure>
                </a>
                <p class="navbar-item">
                    <b>Sean Spiegl</b>
                </p>
                <div v-if="pdf" class="navbar-item">
                    Sean.Spiegl@outlook.com
                </div>
            </div>
            <div class="navbar-menu is-active">
                <div class="navbar-end">
                    <div v-if="!pdf" class="navbar-item">
                        <div class="field is-grouped">
                            <p class="control">
                                <a class="button is-link" href="https://discordapp.com/users/74115767930466304" target="_blank" rel="noopener noreferrer">
                                    <span class="icon">
                                        <i class="fab fa-discord"></i>
                                    </span>
                                    <span>
                                        Discord
                                    </span>
                                </a>
                            </p>
                            <p class="control">
                                <a @click="showEmail=true" class="button is-link is-light">
                                    <span class="icon">
                                        <i class="fas fa-envelope"></i>
                                    </span>
                                    <span>
                                        Email
                                    </span>
                                </a>
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </nav>

        <EmailInfo @close="showEmail=false" :isActive="showEmail"/>

        <section class="section">
            <h2 class="subtitle" v-html="slogan"></h2>
            <h2 class="title">{{unitTitle}} Help!</h2>
        </section>

        <section class="section list left-centered">
            <ul style="list-style-type:circle;">
                <li>Are your labs taking way too long to finish?</li>
                <li>Do you get stuck on errors for hours at a time?</li>
                <li>Does it feel like you have no idea what you are doing?</li>
            </ul>
        </section>

        <section class="section left-centered">
            <Vim :lines="aboutMe" :comment="commentStyle"/>
        </section>

        <section class="section">
            <nav class="level padded">
                <div class="level-item has-text-centered">
                    <div>
                        <p class="heading">Group Session (4 People Max)</p>
                        <p class="title is-1">${{groupPrice}}/hour</p>
                    </div>
                </div>
                <div class="level-item has-text-centered">
                    <div>
                        <p class="heading">1-on-1 Tutoring</p>
                        <p class="title is-1">${{indivPrice}}/hour</p>
                    </div>
                </div>
            </nav>
        </section>

        <section class="section">
            <p>Flexible times. Price negotiable. Recurring or once-off sessions.</p>
            <p v-if="pdf">Book a Session at <b>tutor.dinkydie.me</b> or use the QR code:</p>
            <p><br/></p>
            <div v-if="!pdf" class="field">
                <div class="control">
                    <a class="button is-large is-primary" href="https://forms.gle/nuHU6Y9BQFBscS8z6">Book Session</a>
                </div>     
            </div>
            <div v-else>
                <img :src="`/img/code-${unit}.png`">
            </div>
        </section>
    </div>
    
    <footer class="disclaimer has-text-grey has-background-light">
        <p>I am not affiliated with Curtin University.</p>
        <p>This {{ !pdf ? 'website' : 'poster'}} was created by me and is fully open source. See the <a href="https://github.com/DinkyDieDingus/personalpage" target="blank">source code</a></p>
    </footer>
</template>

<script scoped>
import EmailInfo from './components/EmailInfo.vue'
import Vim from './components/Vim.vue'
export default {
    name: 'App',
    data() {
        return {
            showEmail: false,
            pdf: true,
            groupPrice: 15,
            indivPrice: 25,
            unit: null,
            unitTitle: null,
            commentStyle: null,
            unitFull: null,
            slogan: null,
        }
    },
    components: {
        Vim,
        EmailInfo
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
        switch (this.unit) {
            case 'ucp':
                this.unitTitle = "UCP";
                this.commentStyle = "//";
                this.unitFull = "Unix & C Programming";
                this.slogan = "Does <i>UCP</i> make you want to UC-<i>flee</i> your computing <i>degree</i>?";
                break;
            case 'other':
            default:
                this.unit = 'other';
                this.unitTitle = "Computing Study";
                this.commentStyle = "#";
                this.unitFull = "PDI, UCP, DSA, FOP";
                this.slogan = "Does <i>PDI</i> make you want to PD-<i>die</i>?<br/>Has studying <i>FOP</i> been a complete <i>flop</i>?<br/>Does <i>DSA</i> just ruin your <i>day</i>?<br/>Does <i>UCP</i> make you want to UC-<i>flee</i> your computing <i>degree</i>?";
                break;
                
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
