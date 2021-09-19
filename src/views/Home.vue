<template> 
    <h2 class="font-mono font-bold mt-4 p-8 pl-12 text-4xl flex text-center ml-12 mx-12 mb-8">
        Pesquise dados atuais de covid-19 em todos os países
    </h2>
  <main v-if="!loading">
      <DataTitle  :text="title" :dataDate="dataDate" />
      <DataBoxes :stats="stats"/>
      <CountrySelect @get-country="getCountryData" :countries="countries" />
      <button
          v-if="stats.Country"
          @click="clearCountryData"
          class="
            bg-green-700 text-white rounded-full p-3
            mt-10 focus:outline-none hover:bg-red-800
            font-poppins text-lg
            "
        >
        Limpar busca
      </button>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
      <div class="text-gray-500 text-3xl mt-10 mb-6">
          Buscando dados
      </div>
      <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>

import DataTitle from '@/components/DataTitle';
import DataBoxes from '@/components/DataBoxes';
import CountrySelect from '@/components/CountrySelect';

export default {
    name: 'Home',
    components: { DataTitle, DataBoxes, CountrySelect },
    data() {
        return {
            loading: true,
            title: 'Global',
            dataDate: '',
            stats: {},
            countries: [],
            loadingImage: require('../assets/time.gif')
        }
    },
    methods: {
        async fetchCovidData() {
            const res = await fetch('https://api.covid19api.com/summary') 
            const data = await res.json()

            return data
        },

        getCountryData(country) {
            this.stats = country
            this.title = country.Country
        },

        async clearCountryData() {
            this.loading = true
            const data = this.fetchCovidData()
            this.title = 'Global'
            this.stats =  data.Global
            this.loading = false
        },
    },
    async created() {
        const data = await this.fetchCovidData()
        console.log(data)

        this.dataDate = data.Date
        this.stats = data.Global
        this.countries = data.Countries
        this.loading = false
    }
}
</script>
