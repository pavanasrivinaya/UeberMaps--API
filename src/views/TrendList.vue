<template>
  <div class="all">
    <div class="aligns mt-5">
      <v-flex xs6 class="justify-center ml-5">
        <v-autocomplete
          v-model="searchterm"
          :items="post"
          auto-select-first
          clearable
          dense
          filled
          solo
          solo-inverted
          label="Search for trends"
          item-text="title"
          item-value="title"
          class="ml-5 aligns"
        ></v-autocomplete
      ></v-flex>
    </div>
    <v-container v-if="loading" class="progress">
      <div class="text-xs-right">
        <v-progress-circular
          indeterminate
          :size="150"
          :width="8"
          color="white"
          right
        >
        </v-progress-circular>
      </div>
    </v-container>
    <v-container v-else>
      <h1 class="heading">Trends in the UeberMaps API</h1>
      <v-container v-for="list in filterednames" :key="list.id" mb3>
        <v-card class="mx-auto" max-width="650">
          <v-card-title class="orange--text">{{ list.title }}</v-card-title>
          <v-img
            class="white--text align-end"
            height="300px"
            src="https://p21chong.files.wordpress.com/2011/08/incredible_skypark_in_640_06.jpg"
            v-if="!list.picture_url"
            alt="No image to show"
          ></v-img>
          <v-img
            v-else
            class="white--text align-end"
            height="300px"
            :src="list.picture_url"
          >
          </v-img>
          <v-card-subtitle class="pb-2">
            Created_date :{{ list.created_at }}
          </v-card-subtitle>
          <v-card-text class="text--primary">
            <p>Created By : {{ list.user.name }}</p>
            <p v-if="!list.description">No description</p>
            <p v-else>Description: {{ list.description }}</p>
          </v-card-text>
        </v-card>
      </v-container>
    </v-container>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      loading: false,
      post: [],
      error: "",
      searchterm: [],
      desc: []
    };
  },
  created: function() {
    this.loading = true;
    axios
      .get("https://uebermaps.com/api/v2/trends/latest")
      .then(res => {
        this.loading = false;
        this.post = res.data.data;
        this.desc = res.data.data.description;
        console.log(this.post);
      })
      .catch(err => {
        this.loading = false;
        this.error = err;
      });
  },
  computed: {
    filterednames: function() {
      return this.post.filter(list => {
        return list.title.match(this.searchterm);
      });
    }
  }
};
</script>

<style scoped>
.aligns {
  margin-left: 400px;
}
.progress {
  margin-top: 50px;
  margin-left: 550px;
}
.heading {
  text-align: center;
}
a {
  text-decoration: none;
}
</style>
