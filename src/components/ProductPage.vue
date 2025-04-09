<script setup>
// import { defineProps, defineEmits } from "vue";
const props = defineProps(["storeData", "switch"]);
const emit = defineEmits("nextProduct");
</script>

<template>
  <section class="product-view">
    <!-- bagian kiri product view yaitu gambar  -->
    <div class="left-side-view">
      <img :src="props.storeData.image" alt="" />
    </div>
    <!-- bagian kanan product view yang berisi detail  -->
    <div class="right-side-view">
      <h2 class="product-name" :class="{ 'product-name-womens': props.switch }">
        {{ props.storeData.title }}
      </h2>
      <div class="product-header">
        <p>{{ props.storeData.category }}</p>
        <p class="rating-container">
          <span class="product-rate">{{ props.storeData.rating.rate }}/5</span>
          <span class="rate-circle">
            <span
              v-for="(_, index) in 5"
              :key="index"
              :class="
                index < Math.ceil(props.storeData.rating.rate)
                  ? props.switch
                    ? 'filled-womens'
                    : 'filled'
                  : 'empty'
              "
              >●</span
            >
          </span>
        </p>
      </div>
      <div class="product-detail">
        <p>{{ props.storeData.description }}</p>
      </div>
      <div class="product-footer">
        <h2
          class="product-footer-mens"
          :class="{ 'product-footer-womens': props.switch }"
        >
          ${{ props.storeData.price }}
        </h2>
        <div class="btns">
          <button
            class="btn-primary-mens"
            :class="{ 'btn-primary-womens': props.switch }"
          >
            Add to cart
          </button>
          <button
            @click="emit('nextProduct')"
            class="btn-secondary-mens"
            :class="{ 'btn-secondary-womens': props.switch }"
          >
            Next product
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.filled {
  color: var(--mens-1);
}

.filled-womens {
  color: var(--womens-2);
}

.product-view {
  width: 75%;
  min-height: 700px;
  padding: 1rem;
  display: flex;
  column-gap: 1rem;
  background: var(--pure-white);
  box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.6);
  border-radius: 16px;
  margin: 0 auto;
}

.left-side-view {
  flex-basis: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-right: 2px solid var(--light-gray);
}

.right-side-view {
  flex-basis: 50%;
}

.left-side-view img {
  max-width: 100%;
  height: 500px;
  object-fit: cover;
}

.product-name {
  font-size: 1.6rem;
  color: var(--mens-1);
  margin-top: 1rem;
}

.product-name-womens {
  color: var(--womens-2);
}

.product-header {
  display: flex;
  justify-content: space-between;
  align-items: end;
  width: 100%;
  border-bottom: 1px solid var(--light-gray);
}

.product-header p {
  margin-bottom: 0.5rem;
  text-transform: capitalize;
}

.rating-container {
  display: flex;
  justify-content: center;
  align-self: center;
  gap: 0.5rem;
}

.product-rate {
  align-self: center;
  margin-top: 1rem;
}

.empty {
  color: #ddd;
}

.rate-circle {
  display: flex;
}

.rate-circle span {
  font-size: 2.5rem;
  margin-top: 0.5rem;
}

.product-detail {
  height: 65%;
  font-size: 1.3rem;
  border-bottom: 1px solid var(--light-gray);
  padding: 0.75rem 0;
}

.product-footer {
  padding: 1rem 0;
}

.product-footer-mens {
  color: var(--mens-1);
}

.product-footer-womens {
  color: var(--womens-2);
}

.btns {
  display: flex;
  width: 100%;
  gap: 0.5rem 1rem;
}

.btn-primary-mens {
  flex-basis: 40%;
  justify-self: start;
  padding: 0.5rem;
  background: var(--mens-1);
  color: var(--pure-white);
  border: none;
}

.btn-primary-womens {
  background: var(--womens-2);
}

.btn-secondary-mens {
  flex-basis: 40%;
  justify-self: start;
  padding: 0.5rem;
  border: 1.5px solid var(--mens-1);
  color: var(--mens-1);
  background: var(--pure-white);
}

.btn-secondary-womens {
  color: var(--womens-2);
  border: 1.5px solid var(--womens-2);
}

button {
  margin: 0.25rem 0;
  font-size: 1.2rem;
}
</style>
