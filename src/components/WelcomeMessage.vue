<script setup>
const props = defineProps({
  userName: {
    type: String,
    default: 'X'
  }
})
</script>

<template>
  <section class="max-w-4xl mx-auto bg-white overflow-hidden">
    <!-- Hero image recortada -->
    <div class="h-64 overflow-hidden">
      <img
        src="/welcome.png"
        alt="Train hero"
        class="w-full h-full object-cover object-center"
      />
    </div>

    <!-- Texto de bienvenida -->
    <div class="px-6 py-4 text-gray-800">
      <p class="text-base leading-relaxed">
        Beste {{ userName }}, bedankt voor het reserveren van je groepsreis!  
        We kijken ernaar uit om jou en je groep een onvergetelijke treinreis te bezorgen.  
        Hieronder vind je een aantal tips om je reis vlot te laten verlopen.  
        Alvast een fijne treinreis gewenst. Tot binnenkort in de trein.
      </p>
    </div>
  </section>
</template>
