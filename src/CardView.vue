<template>
   <div>
    <img :src="원룸.image" alt="" class="roomimg">
    <h4 @click="함수">{{ 원룸.title }}</h4>
    <p>{{ 원룸.price }}원</p>
    
  </div>
</template>

<script>
export default {
    name : 'CardView',

    props : {
        // props로 가져올 object명 : object타입
        // 부모쪽에서 보낸 props는 데이터 수정이 안된다.
        원룸 : Object,
       
    },
    methods : {
        함수() {
        this.$emit('openModal',this.원룸.id)
        }
    }
}
</script>

<style>

</style>