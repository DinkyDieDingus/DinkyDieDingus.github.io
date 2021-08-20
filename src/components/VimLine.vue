<template>
    <div :style="{'grid-row': row}" class="line-num">{{ row }}&#160;</div> 
    <div :style="{'grid-row': row}" class="line">
        <span v-if="comment" class="cyan">{{`${comment} `}} </span>
        <span :class="{ cyan: comment }"><slot></slot></span>
    </div>
</template>

<script scoped>
export default {
name: 'Vim',
    props: {
        row: Number,
        comment: String
    }
}
</script>

<style scoped>

.cyan {
    color: cyan;
}

.line-num {
    grid-column-start: 1;
    color: yellow;
}

.line {
    grid-column-start: 2;
}

</style>
