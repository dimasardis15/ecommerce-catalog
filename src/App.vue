<script setup>
import { computed, onBeforeMount, ref } from "vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";
import NotFoundProduct from "./components/NotFoundProduct.vue";
import ProductPage from "./components/ProductPage.vue";

// storeData untuk menyimpan data per index
const storeData = ref(null);
// is Loading untuk menampilkan spinner jika data belum dimuat
const isLoading = ref(true);
// current index
const productIndex = ref(1);

//fetch api function mulai dari index 1 saat di load
async function fetchApi(index = 1) {
  try {
    isLoading.value = true;
    const response = await fetch(`https://fakestoreapi.com/products/${index}`);
    const data = await response.json();
    if (!response.ok) throw new Error("Product not found...");
    console.log(data);
    //hanya akan mengambil data yang categorynya men or womens
    if (
      data.category !== "men's clothing" &&
      data.category !== "women's clothing"
    ) {
      storeData.value = null;
      return;
    }
    storeData.value = data;
  } catch (err) {
    console.error(err.message);
  } finally {
    isLoading.value = false;
  }
}

onBeforeMount(async () => {
  await fetchApi();
  console.log("berhasil render");
});

async function handleClickProduct() {
  isLoading.value = true;
  //akan increment index setiap di klik next product btn
  productIndex.value++;
  //akan reset ke-index 1 jika index > 20
  if (productIndex.value > 20) productIndex.value = 1;
  //fetch data baru sesuai indexnya
  await fetchApi(productIndex.value);
  //console.log disini untuk mengetahui current index dan mencari bug jika ada
  console.log(`data baru berhasil di fetch di index ${productIndex.value}`);
}

const switchCategory = computed(
  () => storeData.value?.category === "women's clothing"
);
</script>

<template>
  <main :class="{ womens: switchCategory }">
    <!-- jika masih loading dan data belum berhasil dimuat  -->
    <LoadingSpinner v-if="isLoading && !storeData" />
    <!-- jika sudah selesai loading tapi data tidak ditemukan  -->
    <NotFoundProduct
      v-else-if="!isLoading && !storeData"
      @next-product="handleClickProduct"
    />
    <!-- jika sudah selesai loading dan data berhasil didapat  -->
    <ProductPage
      v-else-if="!isLoading && storeData"
      :store-data="storeData"
      @next-product="handleClickProduct"
      :switch="switchCategory"
    />
  </main>
</template>

<style scoped>
main {
  background: linear-gradient(to bottom, var(--mens-2) 65%, white 35%);
  height: 100vh;
  margin: 0;
  display: flex;
  align-items: center;
}
.womens {
  background: linear-gradient(to bottom, var(--womens-1) 65%, white 35%);
}
</style>
