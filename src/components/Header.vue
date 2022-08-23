<template>
    <div class="MyHeader">
        <div>
            <h1>ACG Falls Flow</h1>
        </div>
    </div>
</template>

<script type="text/javascript">
export default {
    name: "MyHeader"
}
</script>

<style lang='less' scoped>
.MyHeader {
    z-index: 999;
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
    box-shadow: 0 0 3px #ccc;
    height: 80px;
    background-color: rgba(36, 33, 33, 0.95);
}
</style>