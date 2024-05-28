<template>
    <div>
      <h1 class="text-2xl font-bold mb-4">Cryptocurrency Prices</h1>
      <div v-if="loading" class="text-center">Loading...</div>
      <table v-else class="table-auto w-full">
        <thead>
          <tr>
            <th class="px-4 py-2">Name</th>
            <th class="px-4 py-2">Symbol</th>
            <th class="px-4 py-2">Price (USD)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="crypto in cryptos" :key="crypto.id">
            <td class="border px-4 py-2">{{ crypto.name }}</td>
            <td class="border px-4 py-2">{{ crypto.symbol }}</td>
            <td class="border px-4 py-2">{{ crypto.price_usd }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cryptos: [],
        loading: true
      };
    },
    async mounted() {
      try {
        const response = await fetch('https://api.coinlore.net/api/tickers/');
        const data = await response.json();
        this.cryptos = data.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      } finally {
        this.loading = false;
      }
    }
  };
  </script>
  
  <style scoped>
  /* Add any additional styles here */
  </style>
  