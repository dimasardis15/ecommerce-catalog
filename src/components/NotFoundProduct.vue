<script setup>
import noProductImg from "@/assets/error-face.png";
// import { defineEmits } from "vue";

const emit = defineEmits("nextProduct");
</script>

<template>
  <section
    class="not-found"
    :style="{ backgroundImage: `url(${noProductImg})` }"
  >
    <div class="not-found-info">
      <p>This product is unavailable to show</p>
      <button @click="emit('next-product')">Next Product</button>
    </div>
  </section>
</template>

<style scoped>
.not-found {
  width: 75%;
  height: 700px;
  padding: 1rem;
  display: flex;
  justify-content: center;
  background: var(--pure-white);
  box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.6);
  border-radius: 16px;
  margin: 0 auto;
  position: relative;
  background-repeat: no-repeat;
  background-size: cover;
}

.not-found-info {
  align-self: center;
  text-align: center;
  font-size: 1.5rem;
}

button {
  width: 100%;
  padding: 0.25rem 0;
  margin-top: 0.5rem;
  font-size: 1.25rem;
  background: none;
  transition: all 0.1s linear;
}

button:hover {
  background: var(--light-gray);
}
</style>
