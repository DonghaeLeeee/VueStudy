<template>
    <div class="discount">
        <h4>지금결제하면 {{할인률}}%할인</h4>
    </div>
</template>

<script>
export default {
    name: 'DiscountView',
    props: {
        할인률 : Number
    }
}
</script>

<style>

</style>

