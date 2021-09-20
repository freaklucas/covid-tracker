<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- Box 1 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded hover:bg-green-200">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Casos</h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">Novos:</span>
        {{ numberWithCommas(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithCommas(stats.TotalConfirmed) }}
      </div>
    </div>

    <!-- Box 2 -->
    <div class="shadow-md bg-blue-200 p-10 text-center rounded hover:bg-green-200">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Óbitos</h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">Novos:</span>
        {{ numberWithCommas(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithCommas(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DataBoxes',
  props: ['stats'],
  setup () {
    return {
      numberWithCommas (x) {
        return x.toString()
          .replace(/\B(?=(\d{3})+(?!\d))/g, ',');
      }
    };
  }
};
</script>

