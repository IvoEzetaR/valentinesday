<script setup>
import {computed, ref} from "vue";
import {GIFS, ACCEPTED_GIF} from "@/util/valentineConstants.js";
import Confetti from 'vue-confetti/src/confetti';

const confetti = new Confetti({});

const paramNames = "Natalia Amor de mi vida";
const title = ref(`${paramNames}, ¿Quieres ser mi San Valentín?`)
const actualGif = ref(GIFS[0]);

const isYesButtonClicked = ref(false);
const yesButtonClickCount = ref(0);

const fontSize = computed(() => {
  return yesButtonClickCount.value===0 ? 22 : Math.max(16, 20 + yesButtonClickCount.value * 6);
});

const onNoButtonClick = () => {
  const randomIndex = Math.floor(Math.random() * GIFS.length);
  actualGif.value = GIFS[randomIndex];
  yesButtonClickCount.value++;
};

const onYesButtonClick = () => {
  isYesButtonClicked.value = true;
  actualGif.value = ACCEPTED_GIF;
  title.value = `¡SABÍA QUE DIRÍAS QUE SÍ! Te amo con toda mi vida, Natalia 😍`;

  confetti.start({
    particles: [
      {
        type: 'heart',
      }
    ],
    defaultSize: 30,
    defaultColors: [
      '#ff4d6d',
      '#ff758f',
      '#c9184a',
      '#ffb3c1',
    ],
  });

  setTimeout(() => {
    confetti.stop();
  }, 10000);
}
</script>

<template>
  <section class="p-8 w-full h-full min-h-dvh items-center justify-center flex flex-col gap-8 md:p-16">
    <div class="glass-card p-10 flex flex-col items-center gap-10 max-w-4xl w-full border-pink-200">
      <h1 class="text-center font-bold text-[clamp(28px,6vw,48px)] text-[#590d22] leading-tight">
        {{title}}
      </h1>
      
      <div class="h-[300px] md:h-[400px] flex justify-center items-center rounded-2xl overflow-hidden shadow-lg bg-white/30 p-4 border border-white/50 float-animation">
        <img
            :src="actualGif.img"
            alt="gif"
            class="w-full h-full object-contain"
        />
      </div>

      <div class="flex justify-center items-center flex-wrap w-full gap-6" v-if="!isYesButtonClicked">
        <Button
          type="button"
          label="¡SÍ! ❤️"
          class="min-w-fit sm:min-w-64 min-h-20 w-full sm:w-fit p-button-success shadow-xl"
          :style="{ fontSize: fontSize + 'px' }"
          @click="onYesButtonClick"
        />
        <Button
          type="button"
          :label="actualGif.description"
          class="min-w-fit text-xl sm:min-w-64 min-h-20 w-full sm:w-fit p-button-danger shadow-md"
          @click="onNoButtonClick"
        />
      </div>
      
      <div v-if="isYesButtonClicked" class=" romantic-text text-3xl text-pink-600 mt-4 animate-bounce">
         Eres lo mejor que me ha pasado ✨
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Background handled in global style.css */
</style>