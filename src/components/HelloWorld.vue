<template>
  <div class="menu">
    <a v-for="(menus,id) in menu" :key="id">{{ menus }}</a>
  </div>

  <select @change="selectModify">
    <option selected disabled>선택</option>
    <option value="lowPrice">낮은가격순</option>
    <option value="highPrice">높은가격순</option>
    <option value="ganadaSun">가나다순</option>
  </select>
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
  <!--    <div class="black-bg"  v-if="modal===true" >
        <div class="white-bg">
          <img :src="oneRooms[pickedModal].image" class="room-img"/>
          <h4>{{oneRooms[pickedModal].title}}</h4>
          <p>{{ oneRooms[pickedModal].content }}</p>
          <h3> 가격 : {{oneRooms[pickedModal].price}} </h3>
          <DiscountComponent/>
          <button @click="modal=false">닫기</button>
        </div>
      </div>-->

  <!-- Modal -->
  <transition name="modals">
    <EstateModal :modal="modal" :pickedModal="pickedModal" :oneRooms="oneRooms"
                 @closeModal="modal=false"/>
  </transition>

  <EstateCard :oneRooms="oneRooms" :modal="modal" :pickedModal="pickedModal"
              @openModal="modal=true; pickedModal=$event"/>

  <!--  <div v-for="(estate,id) in (oneRooms)" :key="id">
      <img :src="estate.image" class="room-img"/>
      <h4 :style="h4Style" @click="modal=true; pickedModal=id; ">{{ estate.title }}</h4>
    </div>-->

</template>


<script>

import oneRoomData from '../assets/oneRoomData/oneRooms';
import EstateCard from "@/components/EstateCard";
import EstateModal from "@/components/EstateModal";


export default {
  name: 'HelloWorld',
  components: {EstateCard, EstateModal},
  props: {
    msg: String
  },
  data() {
    return {
      pickedModal: 0,
      modal: false,
      oneRooms: [...oneRoomData],
      oneRoomsCopy: [...oneRoomData],
      price: [3, 2, 4],
      h4Style: 'color : blue',
      estates: [
        {name: '역삼동원룸', report: 0, modal: false},
        {name: '천호동원룸', report: 0, modal: false},
        {name: '마포구원룸', report: 0, modal: false}],
      menu: ['HOME', 'PRODUCT', 'ABOUT']
    }
  },
  created() {
    console.log(this.oneRoomsCopy);
  },
  methods: {
    selectModify(e) {
      switch (e.target.value) {
        case 'lowPrice' :
          this.oneRoomsCopy.sort((a, b) => {
            console.log(a.price - b.price);
            return (
                a.price - b.price
            )
          });
          console.log(this.oneRoomsCopy);
          this.oneRooms = [...this.oneRoomsCopy];
          break;
        case 'highPrice' :
          this.oneRoomsCopy.sort((a, b) => {
            console.log(b.price + a.price);
            return b.price - a.price
          });
          console.log(this.oneRoomsCopy);
          this.oneRooms = [...this.oneRoomsCopy];
          break;
        case 'ganadaSun' :
          this.oneRoomsCopy.sort(function(a, b) {
            const nameA = a.title.toUpperCase(); // ignore upper and lowercase
            const nameB = b.title.toUpperCase(); // ignore upper and lowercase
            if (nameA < nameB) {
              return -1;
            }
            if (nameA > nameB) {
              return 1;
            }
            // 이름이 같을 경우
            return 0;
          });
          this.oneRooms = [...this.oneRoomsCopy];
          console.log(this.oneRoomsCopy);
          break;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.menu {
  background: darkslateblue;
  padding: 15px;
  top : auto;
  border-radius: 5px;
  margin-bottom: 3%;
}

.menu a {
  color: white;
  padding: 10px;
}

div {
  box-sizing: border-box;
}

.modals-enter-from {
  opacity: 0
}

.modals-enter-active {
  transition: all 1s;
}

.modals-enter-to {
  opacity: 1
}

.modals-leave-from {
  opacity: 1
}

.modals-leave-active {
  transition: all 1s;
}

.modals-leave-to {
  opacity: 0
}
</style>
