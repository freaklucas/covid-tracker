<template>
  <header class="text-center bg-blue-900 text-white p-4 mb-10">
    <div class="text-3xl md:text-5xl font-bold mb-3"><i class="fa fa-viruses mr-2"></i>Covid-19 Rastreador</div>
    <p>
      API by 
      <a class="text-red-400" href="https://covid19api.com" target="_blank"
        > covid19api.com</a
      >
    </p>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    msg: String,
  },
};
</script>