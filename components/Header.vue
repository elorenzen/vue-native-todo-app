<template>
    <view class="header">
        <text class="title">{{ title }}</text>
    </view>
</template>
<script>
export default {
    props: ['title']
}
</script>
<style scoped>
.header {
    height: 60px;
    background-color: #171717;
    justify-content: center;
    align-items: center
}
.title {
    color: #f3f3f3;
    font-size: 28px;
    font-weight: 700;
    text-transform: uppercase;
}
</style>