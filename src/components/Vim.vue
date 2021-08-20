<template>
    <section class="section left-centered">
        <div class="vim padded shadowed">
            <div class="lines">
                <slot></slot>
            </div>
            <div class="grey">
            ~<br/>
            <p class="end">0,0-1&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;All</p>
            </div>
        </div>
    </section>
</template>

<script scoped>
export default {
name: 'Vim',
}
</script>

<style scoped>

.cyan {
    color: cyan;
}

.grey {
    color: gray;
}
.vim {
    font-family: monospace;
    background: black;
    color: lightgray;
    font-size: 1em;
    line-height: 130%;
    color: white;
}

.lines {
    display: grid;
}

.line-num {
    grid-column-start: 1;
    color: yellow;
}

.line {
    grid-column-start: 2;
}

.end {
    text-align: right;
    color: gray;
}

.padded {
    padding: 1em 1.5em;
}
</style>
