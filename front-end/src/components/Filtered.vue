<template>
<div>
  <div class="main">
    <div class="botton1">
        <h4>Notes for Jake & Stacy</h4>
    <button @click="setCreating" class="pure-button button-xsmall">Add A Note
    </button>
    </div>
    <form class="pure-form" v-if="creating" @submit.prevent="addTicket">
      <fieldset>
       <textarea v-model="comment"></textarea>
       <br />
       <div class="bottons2">
         <button @click="cancelCreating" class="pure-button space-right">Cancel</button>
         <button class="pure-button pure-button-primary" type="submit">Submit</button>
       </div>

      </fieldset>
     </form>

  </div>
  <div class="wrapper">
    <div class="search">
      <form class="pure-form">
        <i class="fas fa-search"></i><input v-model="searchText" />
      </form>
    </div>
  </div>
  <Tickets :tickets="tickets" />
</div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
import Tickets from "../components/Tickets.vue"
export default {
  name: 'Home',
  components: {
    Tickets
  },
  data() {
     return {
       searchText: '',
     }
   },
   computed: {
   tickets() {
     return this.$root.$data.tickets.filter(tickets => ticket.user.firstName.toLowerCase().search(this.searchText.toLowerCase()) >= 0);
   },
   user() {
     return this.$root.$data.user;
   },
  },
  methods: {
    async logout() {
      try {
        await axios.delete("/api/users");
        this.$root.$data.user = null;
      } catch (error) {
        this.$root.$data.user = null;
      }
    },
    async getTickets() {
      try {
        let response = await axios.get("/api/tickets/" + this.$route.params.id);
        this.tickets = response.data.tickets;
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    time(d) {
      return moment(d).format('D MMMM YYYY, h:mm:ss a');
    },
    formatDate(date) {
      if (moment(date).diff(Date.now(), 'days') < 15)
        return moment(date).fromNow();
      else
        return moment(date).format('d MMMM YYYY');
    },
    setCreating() {
      this.creating = true;
    },
    cancelCreating() {
      this.creating = false;
    },
    async addTicket() {
      try {
        await axios.post("/api/tickets/" + this.$route.params.id, {
          comment: this.comment
        });
        this.comment = "";
        this.creating = false;
        this.getTickets();
        return true;
      } catch (error) {
        console.log(error);
      }
    },

  },
}
</script>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

.search {
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 50%;
}

form {
  display: table;
  width: 100%;
}

i {
  display: table-cell;
  padding-left: 10px;
  width: 1px;
}

input {
  display: table-cell;
  font-size: 20px;
  border: none !important;
  box-shadow: none !important;
  width: 100%;
  height: 40px;
}

fieldset {
  margin-left: 10%;
  margin-right: 10%;
  width: 80%;
  text-align: center;
}
textarea {
  width: 100%;
  text-align: center;

}

h3 {
  display: flex;
  font-size: 12px;
  font-weight: normal;
  background-color: #ccc;
  padding: 10px 20px;
  padding-bottom: 0px;
  margin: 0px;
  background-color: #94D9E8;
}

h6 {
  color: #888;
  font-size: 10px;
  font-weight: bold;
  padding: 0px;
  border: 0px;
  margin: 0px;
  padding-left: 20px;
  padding-top: 7px;
  padding-bottom: 4px;
  background-color: #ccc;
    background-color: #94D9E8;

}

h4 {
  text-align: center;
  padding-top: 20px;
  font-size: 16px;
  font-weight: normal;
}


label {
  background-color: #000;
  color: white;
  padding: 5px;
  border-radius: 30px;
  font-size: 12px;
  margin-right: 10px;
}

.problempart2 {
 background-color: #fafafa;
 padding-left: 20px;
 margin-bottom: 10px;
 box-shadow: 0 1px 1px #ccc;
}

h2 {
  padding-top: 50px;
}

.botton1 {
  text-align: center;
  padding: 10px;
}

.bottons2 {
  padding: 10px;
}

.actions {
  text-align: right;
}
.problempart {
  background-color: #94D9E8;
}


</style>
