<template> 
    <h2 class="font-mono font-bold mt-4 p-8 pl-12 text-4xl flex text-center ml-12 mx-12 mb-8">
        Pesquise dados atuais de covid-19 em todos os países
    </h2>
    <main v-if="!loading">
        <DataTitle  :text="title" :dataDate="dataDate" class="font-bold" />
        <DataBoxes :stats="status" />
        <CountrySelect @get-country="getCountryData" :countries="countries" />
        <button
            v-if="status.Country"
            @click="clearCountryData"
            class="
            bg-green-700 text-white rounded-full p-3
            mt-10 focus:outline-none hover:bg-red-400
            font-poppins text-lg
            "
            >
            Limpar busca
        </button>
    </main>
    <main v-else class="flex flex-col align-center justify-center text-center">
        <div class="text-gray-500 text-3xl mt-10 mb-6">
            Buscando dados
        </div>
        <img :src="require('../assets/time.gif')" class="w-24 m-auto" alt="logo de carregamento" />
    </main>
</template>

<script>
import CountrySelect from '@/components/CountrySelect';
import DataBoxes from '@/components/DataBoxes';
import DataTitle from '@/components/DataTitle';
import { ref } from 'vue';
export default {
    name: 'Home',
    components: {
        DataTitle,
        DataBoxes,
        CountrySelect
    },
    setup () {
        const loading = ref(true);
        const title = ref('Global');
        const dataDate = ref('');
        const status = ref({});
        const countries = ref([]);
        const fetchCovidData = async () => {
            const res = await fetch('https://api.covid19api.com/summary');
            return await res.json();
        };
        const getCountryData = (country) => {
            status.value = country;
            title.value = country.Country;
        };
        const clearCountryData = async () => {
            loading.value = true;
            const data = await fetchCovidData();
            title.value = 'Global';
            status.value = data.Global;
            loading.value = false;
        };
        const baseSetup = async () => {
            const data = await fetchCovidData();
            dataDate.value = data.Date;
            status.value = data.Global;
            countries.value = data.Countries;
            loading.value = false;
        };
        baseSetup();
        return {
            loading,
            title,
            dataDate,
            status,
            countries,
            getCountryData,
            clearCountryData
        };
    }
};
</script>

