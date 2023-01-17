<template>
  <div class="loading"></div>
</template>

<script>

export default {

}
</script>

<style lang="less" scoped>
    .loading{
        width: 80px;
        height: 80px;
        border-radius: 50%;
        border: 3px solid @light-yellow;
        border-top: @yellow;
        animation: spin 1s linear infinite;
    }

    @keyframes spin{
        to{
            transform: rotate(360deg);
        }
    }
</style>