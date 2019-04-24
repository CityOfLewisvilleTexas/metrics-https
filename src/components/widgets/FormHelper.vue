<template>
    <div>
        <slot name="title"></slot>
        <h1>I am the form helper</h1>
        <slot name="text"></slot>
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>
h1 {
    text-transform: uppercase;
    color: #dedede;
    text-shadow: 3px 3px 10px #999;
}
div {
    border: #999 solid 1px;
    border-block-end-width: thick;
    border-radius: 5px;
}
</style>
