<template>
  <div :class="product.category == 'women\'s clothing' ? 'bg-women' : (product.category == 'men\'s clothing' ? 'bg-men' : 'bg-empty')">
    <div class="product-page" v-if="product.category == 'men\'s clothing' || product.category == 'women\'s clothing'">
      <div class="img-container">
        <img :src="product.image" :alt="product.title" />
      </div>
      <div class="desc-container">
        <p class="product-title" >{{ product.title }}</p>
        <div class="product-rating">
          <p>{{ product.category }}</p>
          <p>{{ product.rating.rate }}/5</p>
        </div>
        <p class="product-desc">{{ product.description }}</p>
        <div>
          <p class="product-price">${{ product.price }}</p>
          <div>
            <button type="submit" :class="product.category == 'women\'s clothing' ? 'btn-buy-women' : (product.category == 'men\'s clothing' ? 'btn-buy-men' : 'btn-buy-empty')">Buy now </button>
            <button type="submit" :class="product.category == 'women\'s clothing' ? 'btn-next-women' : (product.category == 'men\'s clothing' ? 'btn-next-men' : 'btn-next-empty')">Next Product</button>
          </div>
        </div>
      </div>
    </div>

    <div class="bg-empty" v-else>
      <div class="empty-page">
        <!-- <img src="../" alt="" srcset=""> -->
        This product is unavailable to show
        <button @click="fetchProduct">Next product</button>
      </div>
    </div>
    <button @click="fetchProduct">Next</button>
  </div>
</template>
  
<script>
  export default {
    data() {
      return {
        product: {},
        index: 1
      };
    },
    methods: {
      async fetchProduct() {
        const response = await fetch(`https://fakestoreapi.com/products/${ this.index <= 20 ? this.index++ : this.index = 1 }`);
        const data = await response.json();
        this.product = data;
        console.log(data)
      },
    },
    mounted() {
      this.fetchProduct();
    },
  };
</script>

<style src="../../assets/style/page.css"></style>