<template>
<div class="home">
  <div class="main-photo">
    <img src="@/assets/kiss.jpg">
  </div>
  <div class="card-deck">
<div class="card">
<img class="card-img-top" src="@/assets/pex_cam.jpg" alt="Card image cap">
<div class="card-body">
  <router-link class="dropdown-item" to="/gallery">
  <h5 class="card-title">Gallery</h5>
  </router-link>
  <p class="card-text">A gallery of the couple, aren't they cute?</p>
</div>
</div>

<div class="card">
<img class="card-img-top" src="@/assets/pex_book.jpg" alt="Card image cap">
<div class="card-body">
  <router-link class="dropdown-item" to="/notes">
  <h5 class="card-title">Kind Notes</h5>
  </router-link>
  <p class="card-text">Take a second to write a kind note to the couple, whether it be a word of advice, or just a friendly note reminding them how awesome they are. </p>
</div>
</div>
<div class="card">
<img class="card-img-top" src="@/assets/pex_key.jpg" alt="Card image cap">
<div class="card-body">
  <router-link class="dropdown-item" to="/dashboard">
  <h5 class="card-title">Login</h5>
  </router-link>
  <p class="card-text">To do anything on this site, you'll have to create an account, please remeber to fill in every space!</p>
</div>
</div>
</div>
<div class="space">

</div>
</div>
</template>


<script>
export default {
  name: 'Home',
  components: {
  },
  data() {
    return {

    }
  },
  created() {

  },
  methods: {

  }

}
</script>

<style scoped>
img {
  border: 0;
  margin: 0;
  padding:0;
  width: 100%;
}
.dividing-bar {
  padding: 0;
  margin:0;
  border:0;
  transform: translate(0px, -30px);
  height: 30px;
  background-color: #bbb;
}
.router-link {
  padding: 0;
  margin: 0;
  text-align: left;
}

.space {
  padding: 20px;
}

.card-title {
  text-align: center;
}
.card {
  border: 0;
}
.card-deck {
  margin: 10px;
  margin-top: 25px;
}


</style>
