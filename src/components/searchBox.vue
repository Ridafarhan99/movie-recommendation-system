<template>
  <div>
    <v-row style="margin-left: 30%; margin-right: 30%; margin-top: 60px">
      <v-text-field
        filled
        rounded
        solo
        label="Search Movies"
        placeholder="Start typing to search"
        style="width: 40%; height: 55px; background-color: whitesmoke"
        v-on:keydown="getData"
        v-model="movieName"
      >
      </v-text-field>

      <v-btn
        class="ma-2"
        color="red"
        dark
        v-on:click="
          expand = false;
          option = true;
          recom = false;
        "
        style="height: 40px; margin-left: 10px"
      >
        CLEAR
        <v-icon dark right> mdi-cancel </v-icon>
      </v-btn>
    </v-row>
    <p></p>

    <v-btn
      v-for="item in lists"
      v-bind:key="item.id"
      width="400px"
      height="50px"
      style="margin-left: 33%; margin-top: 5px; width: 35%"
      class="flex-row"
      color="light-green lighten-3"
      elevation="7"
      @click="onSuggestion(item)"
      v-show="option"
    >
      <v-card-title v-if="item.title !== undefined">
        {{ item.title }}
        <!-- {{item.id}} -->
      </v-card-title>
    </v-btn>

    <v-expand-transition>
      <v-card
        v-show="expand"
        width="1000"
        class="mx-auto my-12"
        style="margin-top: 30px"
        min-height="600px"
      >
        <v-img
          height="350"
          v-bind:src="'http://image.tmdb.org/t/p/w500' + moviedata.poster_path"
        ></v-img>
        <v-card-title>
          {{ moviedata.title }}
        </v-card-title>
        <v-rating
          :value="(moviedata.vote_average * 5) / 10"
          length="5"
          color="amber"
          dense
          half-increments
          readonly
          size="20"
          style="margin-left: 10px"
        ></v-rating>
        <div class="grey--text ms-4">
          IMDB rating: {{ moviedata.vote_average }}
        </div>
        <br />

        <v-divider class="mx-4"></v-divider>

        <br />
        <div style="margin-left: 20px; margin-right: 20px">
          <div>
            <strong> Release Date: </strong>{{ moviedata.release_date }}
          </div>
          <div><strong> Overview: </strong>{{ moviedata.overview }}</div>
          <br />
          <div>
            <strong> Media Type: </strong>
            <v-chip color="blue">
              {{ moviedata.media_type }}
            </v-chip>
          </div>
        </div>
        <br />
        <!-- <v-card-title>{{item.title}}</v-card-title> -->
      </v-card>
    </v-expand-transition>

    <br />
    <div v-show="recom" style="background-color: #c5e1a5; padding-bottom: 20px">
      <h1
        elevation="12"
        style="text-align: center; margin-top: 80px"
        class="header"
      >
        Recommended Movies
      </h1>

      <v-row v-if="recommmovie.length == 5" style="margin-left: 0%">
        <v-col v-for="index in recommmovie.length" :key="index">
          <v-card color="aquamarine" min-height="300" width="230">
            <v-img
              max-height="150"
              :src="
                'http://image.tmdb.org/t/p/w500' +
                recommmovie[index - 1].poster_path
              "
            >
            </v-img>
            <br />
            <v-divider class="mx-4"></v-divider>

            <v-card-title>
              <!-- {{moviedata.title}} :  -->
              {{ recommmovie[index - 1].title }}
              <!-- {{recommmovie[0].title}} -->
              <!-- {{index}} -->
              <!-- {{test}} -->
            </v-card-title>

            <div class="grey--text ms-4">
              IMDB rating: {{ recommmovie[index - 1].vote_average }}
            </div>

            <br />
            <!-- <v-btn
              style="margin-left:35%; color: ;"
            >open</v-btn> -->
          </v-card>
        </v-col>
      </v-row>
    </div>

    <!-- {{moviedata.title}} -->
    <!-- {{moviedata.title}} -->
  </div>
</template>

<script>
import jsonFile from "../assets/data.json";

export default {
  name: "searchBox",
  data() {
    return {
      movieName: "",
      API_URL:
        "https://api.themoviedb.org/3/search/multi?api_key=b37b3c7ebd44dd331b6f888c817d23f8&query=",
      list: undefined,
      lists: {},
      expand: false,
      option: true,
      moviedata: {},
      recom: false,
      jsondata: jsonFile,
      showing: true,
      recommmovie: [],
    };
  },
  methods: {
    getData() {
      fetch(this.API_URL + this.movieName)
        .then((res) => res.json())
        .then((res) => {
          const { page, results } = res;
          this.page = page;
          this.results = results;
          console.log(results);
          // console.log(this.movieName)
          // console.log(res)
          this.lists = [];
          for (let i = 0; i < 15; i++) {
            if (
              results[i].title != undefined &&
              this.jsondata[results[i].title] !== undefined
            ) {
              this.lists.push(results[i]);
            }
          }
          // console.log('Title: '+results[0].title)
          this.list = results;
          // console.log("Lists: "+this.lists[0])
          // console.log('Recommended Movies: '+this.jsondata.Avatar)
          // console.log(this.jsondata[this.moviedata.title])
          // console.log("moviedata : "+ this.moviedata.title)
        })
        .catch((err) => {
          console.log(err);
          // console.log(this.API_URL+this.movieName)
        });
    },
    onSuggestion(item) {
      this.expand = !this.expand;
      this.option = !this.option;
      this.moviedata = item;
      this.recom = true;
      this.recData();
      // console.log(this.jsondata[this.moviedata.title][0]);

      // console.log(this.moviedata);
    },
    recData() {
      this.recommmovie = [];
      for (let i = 0; i < 5; i++) {
        fetch(this.API_URL + this.jsondata[this.moviedata.title][i])
          .then((res) => res.json())
          .then((res) => {
            // console.log(this.jsondata[this.moviedata.title][i])
            const { page, results } = res;
            this.page = page;
            this.results = results;
            // console.log(results)
            // console.log(this.jsondata[this.moviedata.title][index])
            this.recommmovie.push(results[0]);
            // console.log(index)
            // console.log(this.recommmovie[0].poster_path)
            // console.log(results[0])
            // console.log(this.test);
            // console.log(index)
          });
      }
      console.log(this.recommmovie);
    },
  },
};
</script>

<style>
* {
  text-transform: none !important;
}
</style>