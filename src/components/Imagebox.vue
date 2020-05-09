<template>
  <div id="container">
    <div id="imagebox">
      <div id="images">
        <img :src="`${fileUploadPath}${image}`" />
      </div>
    </div>
    <div id="buttonbox">
      <input
        @change="fileInput"
        ref="fileInput"
        style="display:none"
        type="file"
      />
      <button @click="back" style="margin-right:20px;" class="btn btn-primary">
        Back
      </button>
      <button
        style="margin-right:20px;"
        @click="$refs.fileInput.click()"
        class="btn btn-primary"
      >
        Pick file
      </button>
      <button @click="forward" class="btn btn-primary">Forward</button>
    </div>
    <div id="textinputbox"><input type="text" class="form-control" /></div>
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
  name: "imagebox",
  data() {
    return {
      counter: 0,
      image: "",
      images: [],
      fileUpload: "",
      publicPath: process.env.BASE_URL + "flowers/",
      fileUploadPath: "http://localhost:5000/",
    };
    // return { image: require("@/assets/logo.png") };
  },
  methods: {
    back() {
      if (this.counter >= 1) {
        this.counter--;
        this.image = this.images[this.counter];
      }
      console.log("back");
    },
    fetchImages() {
      axios
        .get("https://restbackenddemo.herokuapp.com/products/productslist")
        .then((res) => {
          // console.log(res.data);
          res.data.map((product) => {
            if (product.fileName != null) {
              this.images.push(product.fileName);
              console.log(this.images);
              this.image = this.images[this.counter];
            }
          });
        });
    },
    fileInput(event) {
      //this.image = require("@/assets/image.gif");
      this.image = "logo.png";
      this.fileUpload = event.target.files[0];
      console.log(this.fileUpload.name);
      const fd = new FormData();
      if (this.fileUpload.name != null) {
        fd.append("fileName", this.fileUpload, this.fileUpload.name);
        axios
          .post("https://restbackenddemo.herokuapp.com/products/add", fd)
          .then((res) => {
            this.fetchImages();
            this.image = this.images[this.counter];
          });
      }
      this.image = this.images[this.counter];
    },
    forward() {
      if (this.counter < this.images.length - 1) {
        this.counter++;
        this.image = this.images[this.counter];
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
<style scoped></style>
