<template>
<!-- 
  단축키
  주석 :  Ctrl + / 
  들여쓰기 : Ctrl + K,F
  프로젝트창 여닫기 : Ctrl + B
-->

<!-- 모달창 컴포넌트화 -->
<transition name="fade">
  <Modal :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" 
  @closeModal="모달창열렸니=false"/>  
</transition>

<!-- v-for="(a,i) in 작명" :key="i" -->
<div class="menu">
  <a v-for="(a,i) in  메뉴들" :key="i">{{ a }}</a>
</div>

  <!-- component & props -->
  <!-- props 보낼때는 다양한 자료형을 보낼수있음 -->
  <!-- ex)컴포넌트명 : 데이터명="[1,2,3]" -->
<Discount v-if="showDiscount == true" :할인률="할인률"/>
<button @click="priceSort">가격순정렬</button>
<button @click="priceSort2">가격역순정렬</button>
<button @click="sortBack">되돌리기</button>
<button @click="nameSort">이름순정렬</button>
<button @click="nameSort2">이름역순정렬</button>
<Card @openModal="모달창열렸니=true; 누른거 = $event" :원룸="원룸들[i]" v-for="(a,i) in 원룸들" :key="i"/>
  
</template>
 
<script>
// import는 컴포넌트를 만들때 또는 다른파일에서 export한것을 가져올때 사용
// import를 여러개 할때는 import {데이터1,데이터2} from '위치'도 사용가능.
import data from './assets/oneroom.js';
import Discount from './DiscountView.vue';
import Modal from './ModalView.vue';
import Card from './CardView.vue';


export default {
  name: 'App',
  data() {
    // 데이터바인딩 할것 등록
    return{
      할인률 : 3,
      showDiscount : true,
      // array,object 데이터의 각각 별개의 사본을 만들때 사용 [...array자료]
      원룸들오리지널 : [...data],
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      메뉴들 : ['Home','Shop','About'],
      products : ['천호동원룸', '역삼동원룸', '마포구원룸'],
      price : [60,70,80]
    }
  },
  methods : {
    // function을 쓸때는 this.가 무조건들어간다.
    priceSort() {
      // this.원룸들.sort()는 가나다순 정렬 ->문자정렬
      this.원룸들.sort(function(a,b) {
        return a.price - b.price;
        //  a-b 가 음수면 왼쪽으로 가라고 sort()함수가 내부적으로 실행
      })
    },
    priceSort2() {
      this.원룸들.sort(function(a,b) {
        return b.price - a.price;
      })
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    },
    nameSort() {
      this.원룸들.sort(function(a,b) {
        if(a.title > b.title) return 1;
        if(b.title > a.title) return -1;
        return 0;
      });
    },
    nameSort2() {
      this.원룸들.sort(function(a,b) {
        if(a.title > b.title) return -1;
        if(b.title > a.title) return 1;
        return 0;
      });
    }
  },
  // lifecycle Hook
  // beforeCreate(), created(),beforeMount(),mounted(),beforeUpdate(),update()등등
  mounted() {
    let interval = setInterval(() => {
        this.할인률 --;
        if(this.할인률==0) {
          clearInterval(interval);
        }
    }, 1000);

  
  },

  components: {
    // 컴포넌트를 만들때 등록
   Discount : Discount,
   Modal : Modal,
   Card : Card,
  }
}
</script>

<style>
  /* opacity : 투명도 */
  /* transition : 속성이 변할때 @초에 걸쳐 변하게 하는것 */

  /* 퇴장 애니메이션 */
 /* 시작 스타일 */
 .fade-leave-from{
    opacity: 1;
  } 
  /* 애니메이션 */
  .fade-leave-active{
    transition: all 1s;
  }

  /* 끝날시 스타일 */
  .fade-leave-to{
    opacity: 0;
  }

  /* 등장 애니메이션 */
  /* 시작 스타일 */
  .fade-enter-from{
    opacity: 0;
  } 
  /* 애니메이션 */
  .fade-enter-active{
    transition: all 1s;
  }

  /* 끝날시 스타일 */
  .fade-enter-to{
    opacity: 1;
  }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.body {
  margin: 0;
}
.menu {
  background-color: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.roomimg {
  width: 100%;
  margin-top: 40px;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 4px;
  padding: 20px;
}
.discount {
  background-color: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

</style>
