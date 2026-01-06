<template>
  <main>
    <Hero />
    <Sliders />
    <About />
    <Services />
    <workProcess />
    <Skills />
    <Footer />
  </main>
</template>

<script setup>
import Hero from "./components/hero.vue";
import Sliders from "./components/sliders.vue";
import About from "./components/about.vue";
import Services from "./components/services.vue";
import workProcess from "./components/workProcess.vue";
import Skills from "./components/skils.vue";
import Footer from "./components/footer.vue";

import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import Lenis from "lenis";
import { onMounted } from "vue";
gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  const lenis = new Lenis();
  lenis.on("scroll", ScrollTrigger.update);
  gsap.ticker.add((time) => {
    lenis.raf(time * 1000);
  });
  gsap.ticker.lagSmoothing(0);
});
</script>