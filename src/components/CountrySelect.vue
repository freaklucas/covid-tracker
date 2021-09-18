<template>
    <div>
        <select  
            @change="onChange()" 
            v-model="selected" 
            class="text-xl font-poppins p-2"
        >
            <option velue="0" 
            class="
                form-select block w-full border p-6 rounded-full mt-10
                bg-gray-400 font-poppins text-xl
                "
            >
                Selecione a cidade
            </option>
            <option v-for="country in countries" :key="country" :value="country.ID"
                class="text-xl"
            >
                {{ country.Country }}
            </option>
        </select>
    </div>
</template>

<script>
    export default {
        name: 'CountrySelect',
        props: ['countries'],
        data() {
            return {
                selected: 0
            }
        },
        methods: {
            onChange() {
                const country = this.countries.find((item) => item.ID === this.selected)
                console.log(country)

                this.$emit('get-country')
                }
        }
        
    }
</script>
