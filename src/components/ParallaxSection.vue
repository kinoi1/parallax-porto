<script setup lang="ts">
import { onMounted, nextTick } from "vue";

onMounted(async () => {
  await nextTick();

  const wrapper = document.querySelector("[data-parallax]");
  if (!wrapper) return;

  const items = wrapper.querySelectorAll<HTMLElement>(".parallax-item");

  let ticking = false;

  function update() {
    const scrollY = window.scrollY;

    items.forEach((el) => {
      const speed = parseFloat(el.dataset.speed || "0");
      el.style.transform = `translateY(${scrollY * speed}px)`;
    });

    ticking = false;
  }

  function onScroll() {
    if (!ticking) {
      requestAnimationFrame(update);
      ticking = true;
    }
  }

  window.addEventListener("scroll", onScroll, { passive: true });
  update();
});
</script>

<template>
  <div
    data-parallax
     class="relative h-[200vh] overflow-hidden bg-cover bg-center"
        style="background-image: url('/background.jpg')"
  >
    <!-- SVG 1 -->
    <img
      src="/svg/Nextjs.svg"
      class="parallax-item absolute top-[10%] left-[10%] w-30"
      data-speed="0.2"
    />

    <!-- SVG 2 -->
    <img
      src="/svg/Laravel.svg"
      class="parallax-item absolute top-[20%] left-[50%] w-30"
      data-speed="0.35"
    />

    <!-- SVG 3 -->
    <img
      src="/svg/Nodejs.svg"
      class="parallax-item absolute top-[40%] left-[30%] w-32"
      data-speed="0.5"
    />

    <!-- SVG 4 -->
    <img
      src="/svg/React.svg"
      class="parallax-item absolute top-[60%] left-[60%] w-30"
      data-speed="0.25"
    />

    <!-- SVG 5 -->
    <img
      src="/svg/Vue.svg"
      class="parallax-item absolute top-[35%] right-[15%] w-36"
      data-speed="0.4"
    />
  </div>
</template>
