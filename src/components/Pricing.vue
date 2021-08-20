<template>
    <section class="section">
        <nav class="level padded">
            <div class="level-item has-text-centered">
                <div>
                    <p class="heading">Group Session</p>
                    <p class="title is-1">${{ group }}/hour</p>
                </div>
            </div>
            <div class="level-item has-text-centered">
                <div>
                    <p class="heading">1-on-1 Tutoring</p>
                    <p class="title is-1">${{ indiv }}/hour</p>
                </div>
            </div>
        </nav>
    </section>
</template>

<script scoped>
export default {
    name: 'Pricing',
    props: {
        group: Number,
        indiv: Number
    }
}
</script>

<style>
</style>
