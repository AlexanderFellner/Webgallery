<template>
  <div id="container">
    <div id="imagebox">
      <div id="images">
        <img :src="image" />
      </div>
    </div>
    <div id="pricetitlebox">
      <span style="color:red;margin-right:20px;">Title: {{ title }}</span
      ><span style="color:red">Price:{{ price }}</span>
    </div>
    <div id="buttonbox">
      <button @click="back" style="margin-right:20px;" class="btn btn-primary">
        Back
      </button>
      <button @click="forward" class="btn btn-primary">Forward</button>
    </div>
    <div id="textinputbox">
      <input v-model="searchtext" type="text" class="form-control" />
    </div>
    <div id="bottombuttonbox">
      <button @click="search" class="btn btn-primary">
        Search
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "webgallery",
  data() {
    return {
      counter: 0,
      image: "",
      price: "",
      title: "",
      images: [],
      prices: [],
      titles: [],
      publicPath: process.env.BASE_URL + "flowers/",
      searchtext: "",
    };
  },
  methods: {
    back() {
      if (this.counter >= 1) {
        this.counter--;
        if (this.images[this.counter].length >= 1) {
          this.image = this.images[this.counter];
          this.price = this.prices[this.counter];
          this.title = this.titles[this.counter];
        }
      }
      console.log("back");
    },
    fetchImages() {
      const webgallery = {
        webgallerysearch: this.searchtext,
      };

      axios
        .post("https://restbackenddemo.herokuapp.com/search", webgallery)
        .then((res) => {
          //console.log(res.data);
          this.images = res.data.images;
          this.image = this.images[2];

          console.log(this.images);
          this.titles = res.data.titles;
          this.prices = res.data.prices;
          this.price = this.prices[2];
          this.title = this.titles[2];
        });
    },

    forward() {
      if (this.counter < this.images.length - 1) {
        this.counter++;
        if (this.images[this.counter].length >= 1) {
          this.image = this.images[this.counter];
          this.price = this.prices[this.counter];
          this.title = this.titles[this.counter];
        }
      }

      console.log("forward");
    },
    search() {
      console.log("search");
    },
  },
  created() {
    console.log("App created");
    this.fetchImages();
  },
};
</script>

<style>
* {
  color: black;
}
</style>
