<template>
  <div v-if="isLoading" class="preloader">
    <div class="loader">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

let isLoading = ref(null);

const showLoader = () => {
  isLoading.value = true;
  document.body.style.overflowY = "hidden"; // 禁用滾動
};

const hideLoader = () => {
  isLoading.value = false;
  document.body.style.overflowY = "auto"; // 恢復滾動
};

// 在組件掛載時可以設置是否需要顯示加載指示器
onMounted(() => {
  showLoader();
  window.onload = () => {
    hideLoader();
  };
});
</script>

<style scoped>
.preloader {
  position: fixed;
  bottom: 0;
  top: 0;
  left: 0;
  right: 0;
  background-color: #584e4a;
  z-index: 999;
}

.loader {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 80px;
  height: 80px;
  transform: translate(-50%, -50%) rotate(45deg) translate3d(0, 0, 0);
  animation: loader 1.2s infinite ease-in-out;

  span {
    position: absolute;
    display: block;
    width: 40px;
    height: 40px;
    background-color: #ee4040;
    animation: loaderBlock 1.2s infinite ease-in-out both;

    &:nth-child(1) {
      top: 0;
      left: 0;
    }
    &:nth-child(2) {
      top: 0;
      right: 0;
      animation: loaderBlockInverse 1.2s infinite ease-in-out both;
    }
    &:nth-child(3) {
      bottom: 0;
      left: 0;
      animation: loaderBlockInverse 1.2s infinite ease-in-out both;
    }
    &:nth-child(4) {
      bottom: 0;
      right: 0;
    }
  }
}

@keyframes loader {
  0%,
  10%,
  100% {
    width: 80px;
    height: 80px;
  }
  65% {
    width: 150px;
    height: 150px;
  }
}
@keyframes loaderBlock {
  0%,
  30% {
    transform: rotate(0);
  }
  55% {
    background-color: #f37272;
  }
  100% {
    transform: rotate(90deg);
  }
}
@keyframes loaderBlockInverse {
  0%,
  20% {
    transform: rotate(0);
  }
  55% {
    background-color: #f37272;
  }
  100% {
    transform: rotate(-90deg);
  }
}
</style>
