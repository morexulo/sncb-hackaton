<!-- src/components/TicketHeader.vue -->
<template>
  <header class="relative overflow-hidden bg-gradient-to-r from-blue-800 to-blue-600 py-12 pb-20 px-4 md:px-8 text-white font-raleway">
    <!-- Contenido principal -->
    <div class="relative z-30 max-w-4xl mx-auto text-center space-y-4">
      <svg xmlns="http://www.w3.org/2000/svg" class="mx-auto w-12 h-12 text-white" fill="currentColor" viewBox="0 0 24 24">
        <path d="M5 16h14v2H5zm2-6h10v4H7zM4 4h16v8H4zm2 2v4h12V6z"/>
      </svg>
      <h1 class="text-5xl font-extrabold tracking-tight">
        Plan your group trip
      </h1>
      <p class="text-xl opacity-90">
        Select origin, destination, date and number of passengers to begin.
      </p>
    </div>

    <!-- Vías superiores -->
    <div class="absolute inset-x-0 top-2 h-8 rails-container z-10"></div>
    <!-- Tren moviéndose izquierda→derecha sobre vías superiores -->
    <div class="absolute inset-x-0 top-0 h-8 flex items-center overflow-hidden pointer-events-none z-20">
      <div class="train-wrapper-top">
        <img src="/train3.png" alt="train" class="h-16 drop-shadow-xl" />
      </div>
    </div>

    <!-- Vías inferiores -->
    <div class="absolute inset-x-0 bottom-0 h-10 rails-container z-10"></div>
    <!-- Tren moviéndose derecha→izquierda sobre vías inferiores -->
    <div class="absolute inset-x-0 bottom-0 h-14 flex items-center overflow-hidden pointer-events-none z-20">
      <div class="train-wrapper-bottom">
        <img src="/train4.png" alt="train" class="h-16 drop-shadow-xl" />
      </div>
    </div>
  </header>
</template>

<script setup>
// componente estático, sin props
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@400;700&display=swap');
.font-raleway { font-family: 'Raleway', sans-serif; }

/* Patrón de rieles común para ambas capas */
.rails-container {
  background:
    linear-gradient(to bottom, transparent 44%, white 44%, white 47%, transparent 47%),
    linear-gradient(to bottom, transparent 53%, white 53%, white 56%, transparent 56%);
}

/* Animación tren izquierda→derecha */
@keyframes trainMoveForward {
  0%   { transform: translateX(-25%); }
  100% { transform: translateX(125%); }
}
.train-wrapper-top {
  display: flex;
  width: 150%;
  animation: trainMoveForward 30s linear infinite;
}

/* Animación tren derecha→izquierda */
@keyframes trainMoveBackward {
  0%   { transform: translateX(125%); }
  100% { transform: translateX(-25%); }
}
.train-wrapper-bottom {
  display: flex;
  width: 150%;
  animation: trainMoveBackward 30s linear infinite;
}
</style>
