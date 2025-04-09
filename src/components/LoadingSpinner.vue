<template>
  <div class="loader"></div>
</template>

<style scoped>
.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid var(--mens-1); /* Blue */
  border-radius: 50%;
  width: 150px;
  height: 150px;
  animation: spin 2s linear infinite;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
