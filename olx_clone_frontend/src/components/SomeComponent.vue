<template>
    <div>
      <h1>Lista ogłoszeń</h1>
      <ul>
        <li v-for="ad in ads" :key="ad.id">{{ ad.title }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  import api from '../services/api';  // Importuj konfigurację axios
  
  export default {
    data() {
      return {
        ads: [],  // Będziemy przechowywać ogłoszenia w tej zmiennej
      };
    },
    mounted() {
      this.fetchAds();
    },
    methods: {
      // Metoda do pobierania danych z backendu
      fetchAds() {
        api.get('ads/')  // Wysyłamy zapytanie GET do `/api/ads/` w backendzie
          .then(response => {
            this.ads = response.data;  // Przypisujemy dane do zmiennej `ads`
          })
          .catch(error => {
            console.error('Błąd pobierania ogłoszeń:', error);
          });
      },
    },
  };
  </script>
  