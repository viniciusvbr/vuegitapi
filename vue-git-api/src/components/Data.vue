<template>
  <div class="row justify-content-center">
    <div class="col-lg-6">
      <div class="card bg-light shadow-sm mb-3 rounded" style="margin-top: 2%">
        <div class="card-body">
          <h5 class="card-title">Enter Details</h5>

          <form>
            <div class="form-group">
              <input
                type="text"
                class="form-control form-control-sm"
                v-model="username"
                id="username"
                placeholder="Your username"
              />
            </div>

            <div class="form-group">
              <input
                type="text"
                class="form-control form-control-sm"
                v-model="repository"
                list="repos"
                id="repository"
                placeholder="Repository name"
                v-on:keyup.enter="sendReq"
              />
            </div>
          </form>

          <button class="btn btn-outline-dark" v-on:click="sendReq">
            Submit
          </button>
        </div>
      </div>
    </div>
    <div class="col-lg-6">
      <h5 v-if="grandTotal && success" style="margin-bottom: 3%;">
        Total Downloads: {{ grandTotal.toLocaleString() }}
      </h5>
      <Card
        v-for="(release, index) in releases"
        :key="index"
        v-bind:release="release"
        v-bind:index="index"
        :success="success"
      ></Card>
      <h5 v-if="!success" style="margin: 2%;">
        No repository found
      </h5>
      <h5 v-if="empty" style="margin: 2%;">
        No Releases
      </h5>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Card from './Card.vue'

export default {
  name: "Data",
  components: {
    Card
  },
  data() {
    return {
      username: "",
      repository: "",
      releases: [],
      grandTotal: 0,
      success: true,
      successs: true,
      empty: false,
      url: "https://api.github.com",
    };
  },
  methods: {
    sendReq: function() {
      var that = this;
      this.empty = false;
      axios
        .get(`${this.url}/repos/${this.username}/${this.repository}/releases`)
        .then(function(response) {
          var data = response.data;
          that.grandTotal = 0;
          for (let i = 0; i < data.length; i++) {
            var total = 0;
            data[i].total = 0;
            for (let j = 0; j < data[i].assets.length; j++) {
              total += parseInt(data[i].assets[j].download_count);
            }
            data[i].total = total;
            that.grandTotal += total;
          }
          that.releases = data;
          that.success = true;
          if (response.data.length === 0) {
            that.empty = true;
          }
        })
        .catch(function() {
          that.success = false;
          that.empty = false;
        });
    },
  },
};
</script>

<style scoped></style>
