<template>
    <div class="vim padded shadowed">
        <div class="lines">
            <template v-for="(line, i) in lines" :key="i">
                <div :style="{'grid-row': i + 2}" class="line-num">{{i + 1}}&#160;</div> 
                <div :style="{'grid-row': i + 2}" class="line">
                    <span v-if="line.comment" class="cyan">{{`${comment} `}} </span>
                    <span :class="{ cyan: line.comment }">{{line.content}}</span>
                </div>
            </template>
        </div>
        <div class="grey">
        ~<br/>
        <p class="end">0,0-1&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;All</p>
        </div>
    </div>
</template>

<script scoped>
export default {
name: 'Vim',
    props: {
        lines: Array,
        comment: String
    }
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
