<template>
    <nav class="navbar is-primary" role="navigation" aria-label="main navigation">
        <div class="navbar-brand">
            <a class="navbar-item">
                <figure class="image">
                    <img class="is-rounded" src="../assets/binky.png">
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
                            <a class="button is-link" :href="discordLink" target="_blank" rel="noopener noreferrer">
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
</template>

<script scoped>
import EmailInfo from '../components/EmailInfo.vue'
export default {
    name: 'Navbar',
    props: {
        discordLink: String,
        pdf: Boolean
    },
    data() {
        return {
            showEmail: false,
        }
    },
    components: {
        EmailInfo
    }
}
</script>

<style>
</style>
