<template>
  <md-card class="md-card-profile">
    <div class="md-card-avatar">
      <img class="img" :src="cardUserImage" />
    </div>

    <md-card-content>
      <div v-for="user in users" v-bind:key="user.id">
        <h6 class="category text-gray">Janitor</h6>
        <h4 class="card-title">{{ user.name }}</h4>
        <p class="card-description">
          Don't be scared of the truth because we need to restart the human
          foundation in truth And I love you like Kanye loves Kanye I love Rick
          Owens’ bed design but the back is...
        </p>
        <p class="card-title">
            {{ user.telp_no }}
        </p>
      </div>
      <md-button class="md-round md-success">Call</md-button>
    </md-card-content>
    <router-link to="/users"> Back </router-link>
  </md-card>
</template>
<script>
export default {
  name: "detail",
  props: {
    cardUserImage: {
      type: String,
      default: require("@/assets/img/faces/marc.jpg")
    }
  },
  data() {
    return {
      errorMessage : "",
      successMessage : "",
      users: []
    };
  },
  mounted: function () {
    console.log("Test getUser");
    this.getUser();
  },
  methods: {
    getUser: function(){
      let currentObj = this;

      let config = {
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/x-www-form-urlencoded'
        },
      }

      this.axios.get("http://api.inoprex.com/include/users.php?action=view&id="+this.$route.params.id, config)
      .then(function(response){
        console.log(response.data.users);
        if (response.data.error) {
          currentObj.errorMessage = response.data.message;
        }else{
          currentObj.users = response.data.users;
        }
      });
    }
  }
};
</script>
<style></style>
