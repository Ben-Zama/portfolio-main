<template>
  <section id="services" ref="sectionRef">
    <div class="intro">
      <h2>Crafting Digital Experiences</h2>
    </div>

    <div class="sticky-wrapper" ref="stickyWrapperRef">
      <div class="sticky-content">
        <div class="sticky-header">
          <h2 ref="headerRef">Services I offer</h2>
        </div>

        <div class="card-container" ref="cardContainerRef">
          <div class="card card-1">
            <div class="card-inner">
              <div class="front">
                <img src="/split1.webp" alt="Web Development" loading="lazy" />
              </div>
              <div class="back">
                <PhGlobe weight="bold" />
                <h3>Web Development</h3>
                <p>
                  I build fast, responsive websites using modern technologies
                  (HTML5, CSS3, JavaScript, VueJS) to deliver engaging user
                  experiences.
                </p>
              </div>
            </div>
          </div>

          <div class="card card-2">
            <div class="card-inner">
              <div class="front">
                <img src="/split2.webp" alt="Mobile App" loading="lazy" />
              </div>
              <div class="back">
                <PhDeviceMobile weight="bold" />
                <h3>App Development</h3>
                <p>
                  I develop cross‑platform mobile apps with Quasar framework,
                  ensuring smooth performance and native‑like UX.
                </p>
              </div>
            </div>
          </div>

          <div class="card card-3">
            <div class="card-inner">
              <div class="front">
                <img src="/split3.webp" alt="Maintenance" loading="lazy" />
              </div>
              <div class="back">
                <PhGear weight="bold" />
                <h3>Web Maintenance</h3>
                <p>
                  I provide ongoing support—updates, security patches, backups,
                  and performance tweaks—to keep your site running smoothly.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="outro">
      <h2>Let’s Build Something Remarkable</h2>
      <CTA name="Contact me" link="#contact" />
    </div>
  </section>
</template>

<script setup>
import { PhDeviceMobile, PhGear, PhGlobe } from "@phosphor-icons/vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ref, onMounted, onUnmounted } from "vue";
import CTA from "./ctaButton.vue";

gsap.registerPlugin(ScrollTrigger);

const sectionRef = ref(null);
const stickyWrapperRef = ref(null);
const headerRef = ref(null);
const cardContainerRef = ref(null);

let ctx;

onMounted(() => {
  ctx = gsap.context(() => {
    const mm = gsap.matchMedia();

    // --- MOBILE & TABLET ANIMATIONS (< 1024px) ---
    mm.add("(max-width: 1023px)", () => {
      // Simple stagger fade-in for mobile (Content is already visible via CSS)
      gsap.from(".card", {
        scrollTrigger: {
          trigger: ".card-container",
          start: "top 80%",
          toggleActions: "play none none reverse",
        },
        y: 60,
        opacity: 0,
        duration: 0.6,
        stagger: 0.2,
        ease: "power2.out",
      });
    });

    // --- DESKTOP ANIMATIONS (>= 1024px) ---
    mm.add("(min-width: 1024px)", () => {
      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: stickyWrapperRef.value,
          start: "top top",
          end: "+=300%",
          scrub: 1,
          pin: true,
          anticipatePin: 1,
        },
      });

      // 1. Header fades in and slides down
      tl.to(headerRef.value, {
        y: 0,
        opacity: 1,
        duration: 1,
        ease: "power2.out",
      });

      // 2. Container shrinks width
      tl.fromTo(
        cardContainerRef.value,
        { width: "75%" },
        { width: "65%", duration: 2, ease: "none" },
        "<"
      );

      // 3. Separate Cards (Gap) & Round Corners
      tl.to(
        cardContainerRef.value,
        {
          gap: "15px",
          duration: 1,
          ease: "power1.inOut",
        },
        ">-0.5"
      );

      tl.to(".card-1", { borderRadius: "16px", duration: 0.5 }, "<");
      tl.to(".card-2", { borderRadius: "16px", duration: 0.5 }, "<");
      tl.to(".card-3", { borderRadius: "16px", duration: 0.5 }, "<");

      // 4. Flip Cards & Fan Out
      tl.to(".card-inner", {
        rotationY: 180,
        duration: 3,
        stagger: 0.15,
        ease: "power2.inOut",
      });

      // Fan effect
      tl.to(".card-1", { y: 50, rotation: -15, duration: 3 }, "<");
      tl.to(".card-2", { y: 10, duration: 3 }, "<");
      tl.to(".card-3", { y: 50, rotation: 15, duration: 3 }, "<");

      // Buffer
      tl.to({}, { duration: 0.5 });
    });
  }, sectionRef.value);
});

onUnmounted(() => {
  if (ctx) ctx.revert();
});
</script>

<style lang="scss" scoped>
#services {
  background: var(--primary);
  color: var(--secondary);
  width: 100%;
  overflow: hidden;
}

/* --- SHARED LAYOUT --- */
.intro,
.outro {
  min-height: 50vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 40px 20px;
  text-align: center;
  gap: 75px;

  h2 {
    font-family: var(--alternate-font);
    font-size: clamp(40px, 8vw, 100px);
    line-height: 1.1;
  }

  .button {
    margin-top: -50px;
    background: var(--secondary);
    color: var(--primary);
    :deep(.button__icon-wrapper) {
      background: var(--primary);
      color: var(--secondary);
    }
    &:hover {
      background: var(--accent);
      color: var(--secondary);
      :deep(.button__icon-wrapper) {
        background: var(--secondary);
        color: var(--accent);
      }
    }
  }
}

/* --- STICKY SECTION WRAPPER --- */
.sticky-wrapper {
  position: relative;
  width: 100%;
  padding: 0 20px;
}

.sticky-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 25px;
}

.sticky-header {
  h2 {
    font-family: var(--header-font);
    font-size: clamp(32px, 5vw, 50px);
    text-align: center;
    opacity: 1;
    transform: none;
  }
}

/* --- CARD CONTAINER --- */
.card-container {
  width: 100%;
  max-width: 500px;
  display: flex;
  flex-direction: column;
  gap: 30px;
  position: relative;
}

/* --- CARD STYLING (Mobile Default) --- */
.card {
  width: 100%;
  /* Mobile: Auto height to fit text, minimum height for consistency */
  min-height: 300px;
  position: relative;
  perspective: 1000px;
}

.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 16px;
  transform-style: preserve-3d;
  transform: none;
}
.front {
  display: none; /* Hide image on mobile */
}

.back {
  position: relative; /* Flow naturally on mobile */
  width: 100%;
  height: 100%;
  min-height: 300px;
  border-radius: inherit;
  overflow: hidden;
  padding: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
  text-align: center;
  transform: none;
  backface-visibility: visible;

  svg {
    font-size: 48px;
  }
  h3 {
    font-family: var(--header-font);
    font-size: 24px;
    font-weight: bold;
  }
  p {
    font-family: var(--body-font);
  }
}

.card-1 .back {
  background: var(--secondary);
  color: var(--text);
}
.card-2 .back {
  background: var(--accent);
}
.card-3 .back {
  background: var(--text);
  color: var(--secondary);
}

@media (min-width: 600px) and (max-width: 1023px) {
  .outro {
    gap: 100px;
  }
  .sticky-wrapper {
    padding: 0 40px;
  }

  .card-container {
    max-width: 600px;
    .card .card-inner .back h3 {
      font-size: 30px;
    }
  }
}

@media (min-width: 1024px) {
  .intro,
  .outro {
    height: 100vh;
    padding: 0 100px;
    gap: 100px;
  }

  .sticky-wrapper {
    height: 100vh;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: visible;
  }

  .sticky-content {
    width: 100%;
    height: 100%;
    position: relative;
    justify-content: center;
    gap: 0;
  }

  .sticky-header {
    position: absolute;
    top: 5%;
    left: 50%;
    transform: translateX(-50%);
    width: 100%;
    z-index: 10;

    h2 {
      opacity: 0;
      transform: translateY(50px);
    }
  }

  .card-container {
    max-width: none;
    width: 75%;
    max-width: 800px;
    flex-direction: row;
    gap: 0;
    align-items: stretch;
    justify-content: center;
    border-radius: 16px;
  }

  /* Restore 3D settings for Desktop */
  .card {
    flex: 1;
    border-radius: 0;
    aspect-ratio: 5/7; /* Enforce ratio only on desktop */
    min-height: auto;
  }

  .card-inner {
    transform-style: preserve-3d;
  }

  /* Restore Front Image */
  .front {
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: inherit;
    backface-visibility: hidden;
    overflow: hidden;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }
  }

  /* Restore Back Logic (Rotated away) */
  .back {
    position: absolute;
    top: 0;
    left: 0;
    transform: rotateY(180deg);
    backface-visibility: hidden;
  }

  /* The "Merged" Initial Look logic */
  .card-1 {
    border-radius: 16px 0 0 16px;
    .card-inner {
      border-radius: inherit;
    }
  }
  .card-2 {
    border-radius: 0;
    .card-inner {
      border-radius: inherit;
    }
  }
  .card-3 {
    border-radius: 0 16px 16px 0;
    .card-inner {
      border-radius: inherit;
    }
  }
}
</style>