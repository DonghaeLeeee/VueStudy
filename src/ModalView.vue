<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" alt="" style="width: 100%;">
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <input v-model="month">
      <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalView',
  data() {
    return {
      month: 1,
    }
  },
  watch: {
    month(a) {
      if (12 < a) {
        alert('할부는 12까지만가능');
        this.month = 1;
      }

      if (isNaN(a) == true) {
        alert('숫자만 입력 가능');
        this.month = 1;
      }

    }
  },

  props: {
    원룸들: Array,
    누른거: Number,
    모달창열렸니: Boolean
  }

}
</script>

<style></style>