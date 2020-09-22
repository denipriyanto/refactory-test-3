<template>
  <div class="main">
    <div class="main-title">{{ msg }}</div>
    <div class="user-count">
      <div class="count">{{ count }}</div>
      Users
    </div>
    <div class="wrapper">
      <div v-for="user in users" :key="user.name" class="card">
        <div class="body-card">
          <div class="title">Name</div>
          <div class="name"><h3 v-html="user.name"></h3></div>
          <div class="wrapper-card">
            <div>
              <div class="title">Email</div>
              <div class="email"><h4>{{ user.email }}</h4></div>
            </div>
            <div>
              <div class="title">Phone</div>
              <div class="phone"><h4>{{ user.phone }}</h4></div>
            </div>
            <div>
              <div class="title">Website</div>
              <div class="website"><h4>{{ user.website }}</h4></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { mapState } from "vuex";

export default {
  name: "Users",
  props: {
    msg: String,
  },
  computed: {
    ...mapState({
      list : state => state.lists
    }),
    users() {
      return this.$store.getters.getData;
    },
    count() {
      return this.$store.getters.getCountData;
    },
  },
  mounted() {
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then((response) => {
        this.setData(response.data);
      })
      .catch((error) => (this.msg = error));
  },
  methods: {
    setData(data) {
      this.$store.dispatch("setDatas", data);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main {
  background-color: #f5f7fa;
  padding: 10px;
}

.main-title {
  font-size: 32px;
  font-weight: bold;
  padding-top: 20px;
}

.count {
  color: #83dd8b;
  font-weight: 800;
  margin-right: 10px;
}
.user-count {
  border-bottom: 1px solid #e1e1e7;
  color: #646464;
  display: flex;
}
.wrapper {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.card {
  width: 50%;
}
.body-card {
  margin: 6px;
  padding: 15px;
  background-color: #fff;
  border-radius: 4px;
}

.body-card .title {
  font-size: 0.825rem;
  font-weight: bold;
  color: #ccc;
  padding-bottom: 4px;
}

.body-card h3, .body-card h4 {
  margin-top: 0;
  margin-bottom: 12px;
  color: #646464;
}

.wrapper-card {
  display: flex;
  justify-content: space-between;
}

.body-card .wrapper-card .website h4 {
  color: #83dd8b;
}

@media screen and (max-width: 1023.98px) {
  .card {
    width: 100%;
  }
}

</style>
