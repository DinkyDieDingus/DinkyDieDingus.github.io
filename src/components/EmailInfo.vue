<template>
    <div class="modal" :class="{'is-active': isActive}">
        <div @click="close" class="modal-background"></div>
        <div class="modal-content message">
            <div class="message-header">
                <p>Email Me!</p>
            </div>
            <div class="message-body">
                <div class="field is-grouped">
                    <div class="control">
                        <input class="input" type="email" value="Sean.Spiegl@outlook.com" readonly/>
                    </div>
                    <div class="control">
                        <button v-if="!copied" @click="copy" class="button">
                            <i class="fas fa-clipboard"></i>
                        </button>
                        <button v-else @click="copy" class="button is-success is-inverted is-focused">
                            <i class="fas fa-check"></i>
                        </button>
                    </div>
                    
                </div>
            </div>
        </div>
        <button @click="close" class="modal-close is-large" aria-label="close"></button>
    </div>
</template>

<script scoped>
export default {
    name: 'EmailInfo',
    props: {
        isActive: Boolean,
    },
    data() {
        return{ 
            copied: false
        }
    },
    emits: [ 'close' ],
    methods: {
        copy() {
            navigator.clipboard.writeText('Sean.Spiegl@outlook.com');
            this.copied = true;
        },
        close() {
            this.copied = false;
            this.$emit('close');
        }
    }
}
</script>

<style scoped>

</style>
