<template>
  <div class="black-bg" v-if="modal===true">
    <div class="white-bg">
      <img :src="oneRooms[pickedModal].image" class="room-img"/>
      <h4 >{{ oneRooms[pickedModal].title }}</h4>
      <p>{{ oneRooms[pickedModal].content }}</p>
      <input v-model="month"
             @input="$event.target.value = $event.target.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');"/>
      <input v-model="month" type="range" min="1" max="12"/>
      <h3> {{ month }} 개월 , 가격 : {{ oneRooms[pickedModal].price * month }} </h3>
      <DiscountComponent v-if="modalShow"/>
      <div v-if="modalSecondsWord">
        <p>할인문구는 {{ modalSeconds }}초 후 닫힙니다.</p>
      </div>

      <button @click="$.emit('closeModal')">닫기</button>
      <button @click="showMe">d</button>
    </div>
  </div>
</template>

<script>
import DiscountComponent from "@/components/DiscountComponent";

export default {
  name: "EstateModal",
  props: {
    pickedModal: Number,
    oneRooms: Array,
    modal: Boolean
  },
  methods: {
    showMe() {
      console.log(this.modalShow);
    }
  },
  components: {DiscountComponent},
  data() {
    return {
      month: 1,
      modalShow: true,
      modalSeconds: 3,
      modalSecondsWord: true
    }
  },

  //Life Cycle Hooks
  mounted() {
    let intavary=setInterval(() => {
      this.modalSeconds--
      console.log(this.modalShow);
      if (this.modalSeconds < 0) {
        this.modalShow = false;
        this.modalSecondsWord=false;
        clearInterval(intavary);
      }
    }, 1000);
  },
  beforeUpdate(){
  this.month==2 ? alert('2개월은 불가입니다.') : console.log('else')
  },

  watch: {
    month(e) {
      if (e >= 13) {
        alert('12개일 이하만 가능합니다.');
      }
    }
  }
}
</script>

<style scoped>

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
  top: 1px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 50%;
  margin-top: 5%;
}
</style>