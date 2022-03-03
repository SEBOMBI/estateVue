<template>
  <div class="menu">
    <a v-for="(menus,id) in menu" :key="id">{{ menus }}</a>
  </div>

<!--  <div v-for="(real,id) in (estates)" :key="id">
    <div class="black-bg"  v-if="real.modal==true" >
      <div class="white-bg">
        <h4>상세페이지</h4>
        <p>상세페이지내용임</p>
        <button @click="real.modal=false">닫기</button>
      </div>
    </div>
      <img src="../assets/estates/room1.jpg" class="room-img"/>
      <h4 :style="h4Style" @click="real.modal=true">{{ real.name }}</h4>
      <p>{{ price[id] }} 천만원</p>
      <button @click="increase(id)">허위매물신고</button>
      <span>신고수 : {{ real.report }}</span>
  </div>-->

    <!--MODAL-->
    <div class="black-bg"  v-if="modal===true" >
      <div class="white-bg">
        <img :src="oneRooms[pickedModal].image" class="room-img"/>
        <h4>{{oneRooms[pickedModal].title}}</h4>
        <p>{{ oneRooms[pickedModal].content }}</p>
        <h3> 가격 : {{oneRooms[pickedModal].price}} </h3>
        <DiscountComponent/>
        <button @click="modal=false">닫기</button>
      </div>
    </div>

  <div v-for="(estate,id) in (oneRooms)" :key="id">
    <img :src="estate.image" class="room-img"/>
    <h4 :style="h4Style" @click="modal=true; pickedModal=id; ">{{ estate.title }}</h4>
  </div>

</template>


<script>

import oneRoomData from '../assets/oneRoomData/oneRooms';
import DiscountComponent from "@/components/DiscountComponent";

export default {
  name: 'HelloWorld',
  components: {DiscountComponent},
  props: {
    msg: String
  },
  data() {
    return {
      DiscountComponent,
      pickedModal : 0,
      modal : false,
      oneRooms : oneRoomData,
      price: [3, 2, 4],
      h4Style: 'color : blue',
      estates: [
        {name: '역삼동원룸', report: 0, modal: false},
        {name: '천호동원룸', report: 0, modal: false},
        {name: '마포구원룸', report: 0, modal: false}],
      menu: ['HOME', 'PRODUCT', 'ABOUT']
    }
  },
  methods: {
    increase(id) {
      this.estates[id].report++
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

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

.room-img{
  width: 50%;
  margin-top: 5%;
}
</style>
