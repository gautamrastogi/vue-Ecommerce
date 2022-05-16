<template>
  <div class="column is-3">
    <div class="box widget">
      <figure class="image mb-4 widgetImage animation">
        <router-link v-bind:to="product.get_absolute_url"
          ><img :src="product.get_thumbnail"
        /></router-link>
      </figure>
      <div class="widgetContent animation">
        <router-link v-bind:to="product.get_absolute_url"
          ><h3 class="is-size-4">{{ product.name }}</h3></router-link
        >
        <br />
        <p class="is-size-6 has-text-grey-darker">${{ product.price }}</p>
        <router-link
          v-bind:to="product.get_absolute_url"
          class="button is-dark mt-4"
        >
          View Details</router-link>
          <br>
          <form action="{url 'like_post' product.id}" method="POST">
            <br>
            <button class="button is-success" type="submit" name="product_id" value="{{ product.id }}">
              <span class="icon">
                <i class="fas fa-check-square"></i>
              </span>
              <span>Like</span>
            </button>
          </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ProductBox",
  props: {
    product: Object,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {

  },
   methods: {
     like() {
      axios
        .post("/api/v1/products/like/", { url: this.url })
        .then((response) => {
          this.products = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },

};
</script>



<style scoped>
@import url(https://fonts.googleapis.com/css?family=Arvo:400,700,400italic,700italic);

.animation {
  -webkit-transition: all 0.2s;
  -moz-transition: all 0.2s;
  -ms-transition: all 0.2s;
  -o-transition: all 0.2s;
  transition: all 0.2s;
}

.widget {
  position: relative;
  display: inline-block;
  width: 260px;
  height: 320px;
  margin: 10px;
  background: #fff;
  overflow: hidden;
  box-shadow: 0 0 5px 0 rgba(0, 0, 0, 0.15);
  cursor: pointer;
}

.widgetImage {
  position: absolute;
  top: 0;
  left: 50%;
  width: 260px;
  height: 260px;
  margin-left: -50%;
}

.widgetImage img {
  width: 100%;
  height: auto;
}

.widget:hover .widgetImage {
  top: -130px;
  left: 0;
  width: 520px;
  height: 520px;
  transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
  -webkit-filter: grayscale(1);
}

.widgetContent {
  position: absolute;
  top: 255px;
  width: 240px;
  height: 300px;
  padding: 10px;
  font-size: 12px;
  line-height: 16px;
  color: #666;
  background: #fff;
}

.widget:hover .widgetContent {
  top: 100px;
}

.widgetTitle {
  margin-bottom: 5px;
  font-size: 20px;
  font-weight: 700;
  line-height: 1.2em;
  color: #000;
}

.widgetSubTitle {
  margin-bottom: 20px;
  font-size: 17px;
  line-height: 1.2em;
  color: #000;
}
</style>
