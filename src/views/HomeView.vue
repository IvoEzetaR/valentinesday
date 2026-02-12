<script setup>
import {useForm} from "vee-validate";
import {useRouter} from "vue-router";

const router = useRouter();
const {handleSubmit} = useForm();

const onSubmit = handleSubmit(() => {
  router.push({name: 'valentine', params: {names: 'Natalia'}});
});
</script>

<template>
  <section class="p-8 w-full h-full min-h-dvh items-center justify-center flex flex-col gap-8 md:p-16">
    <div class="glass-card p-12 flex flex-col items-center gap-8 max-w-2xl w-full text-center">
      <div class="w-24 h-24 bg-pink-100 rounded-full flex items-center justify-center shadow-inner float-animation">
        <span class="text-5xl">💝</span>
      </div>
      
      <div class="flex flex-col gap-4">
        <h1 class="font-bold text-[clamp(32px,7vw,54px)] text-[#c9184a]">
          Para Natalia...
        </h1>
        <p class="text-xl text-fuchsia-950/80 leading-relaxed font-light">
          El amor de mi vida se merece una sorpresa <br>
          tan hermosa como ella. ❤️
        </p>
      </div>

      <form @submit="onSubmit" class="w-full flex justify-center mt-4">
        <Button
            type="submit"
            label="Ver mi Sorpresa ✨"
            class="p-button-success h-20 px-12 text-2xl rounded-full shadow-2xl hover:brightness-110 active:scale-95 transition-all"
        />
      </form>
      
      <p class="text-sm opacity-60 mt-4 italic">
        Haz clic en el botón, princesa.
      </p>
    </div>
  </section>
</template>

<style scoped>
/* Background handled in global style.css */
</style>