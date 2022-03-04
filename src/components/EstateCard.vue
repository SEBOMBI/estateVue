<template>

  <!--Card-->
  <div v-for="(estate,id) in (oneRooms)" :key="id">
    <img :src="estate.image" class="room-img"/>
        <h4 :style="h4Style" @click="$.emit('openModal',id);" :modal="modal" >{{ estate.title }}</h4>
  </div>

</template>

<script>

export default {
  props: {
    oneRooms: Object,
    modal: Boolean,
    pickedModal: Number
  },
  data() {
    return {
      h4Style: 'color : blue'
    }
  }
}

</script>

<style scoped>

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

.room-img {
  width: 50%;
  margin-top: 5%;
}
</style>