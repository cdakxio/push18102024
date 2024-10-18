<template>
  <Layout>
    <Head title="Dashboard" />

   
    <!-- Objectif Mensuel et Année en Cours -->
    <div class="grid grid-cols-2 gap-4 mb-8">
      <div class="p-6 bg-blue-100 rounded-lg shadow-md">
        <h3 class="text-lg font-semibold">Objectif Mensuel</h3>
        <div class="relative w-full h-4 bg-gray-200 rounded-full mt-3">
          <div class="absolute top-0 h-4 bg-blue-500 rounded-full" style="width: 50%;"></div>
        </div>
        <p class="mt-2 text-gray-600">5000 € / 10000 €</p>
      </div>
      <div class="p-6 bg-green-100 rounded-lg shadow-md">
        <h3 class="text-lg font-semibold">Année En Cours</h3>
        <p class="mt-2 text-gray-600">Marge : 8000 €</p>
      </div>
    </div>

    <!-- Statistiques -->
    <div class="mb-8">
      <h3 class="text-xl font-semibold mb-4">Statistiques</h3>
      <table class="min-w-full bg-white border border-gray-200 shadow-md rounded-lg">
        <thead>
          <tr class="bg-gray-100 border-b border-gray-300">
            <th class="py-2 px-4">Mois</th>
            <th class="py-2 px-4" v-for="month in months" :key="month">{{ month }}</th>
          </tr>
        </thead>
        <tbody>
          <tr class="border-b">
            <td class="py-2 px-4">Marge</td>
            <td class="py-2 px-4" v-for="month in months" :key="month">0</td>
          </tr>
          <tr class="border-b">
            <td class="py-2 px-4">Comm</td>
            <td class="py-2 px-4" v-for="month in months" :key="month">0</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Filtres de recherche et filtres de vente -->
    <div class="mb-4">
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Recherche par client..."
        class="w-full px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring focus:border-blue-300 mb-4"
      />

      <select v-model="filterStatus" class="px-4 py-2 border rounded-lg mb-4">
        <option value="">Tous les statuts</option>
        <option value="Payé">Payé</option>
        <option value="Non payé">Non payé</option>
      </select>

     
    </div>

    <!-- Dernières ventes -->
    <div class="mb-8">
      <h3 class="text-xl font-semibold mb-4">Dernières ventes</h3>
      <table class="min-w-full bg-white border border-gray-200 shadow-md rounded-lg">
        <thead class="bg-gray-100 border-b border-gray-300">
          <tr>
            <th class="py-2 px-4">N°</th>
            <th class="py-2 px-4">Date</th>
            <th class="py-2 px-4">Client</th>
            <th class="py-2 px-4">TVA</th>
            <th class="py-2 px-4">BQE</th>
            <th class="py-2 px-4">PV.BR</th>
            <th class="py-2 px-4">TOPUP</th>
            <th class="py-2 px-4">PV.NET</th>
            <th class="py-2 px-4">NB MOIS</th>
            <th class="py-2 px-4">Marge</th>
            <th class="py-2 px-4">Statut</th>
            <th class="py-2 px-4">Date L</th>
            <th class="py-2 px-4">Comm</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="sale in filteredSales" :key="sale.id" class="border-b hover:bg-gray-100">
            <td class="py-2 px-4">{{ sale.id }}</td>
            <td class="py-2 px-4">{{ sale.date }}</td>
            <td class="py-2 px-4">{{ sale.client }}</td>
            <td class="py-2 px-4">{{ sale.tva }}</td>
            <td class="py-2 px-4">{{ sale.bqe }}</td>
            <td class="py-2 px-4">{{ sale.pvbr }}</td>
            <td class="py-2 px-4">{{ sale.topup }}</td>
            <td class="py-2 px-4">{{ sale.pvnet }}</td>
            <td class="py-2 px-4">{{ sale.nbMois }}</td>
            <td class="py-2 px-4">{{ sale.marge }}</td>
            <td class="py-2 px-4">{{ sale.statut }}</td>
            <td class="py-2 px-4">{{ sale.dateL }}</td>
            <td class="py-2 px-4">{{ sale.comm }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </Layout>
</template>

<script>
import { Head } from '@inertiajs/vue3'
import Layout from '@/Shared/Layout.vue'

export default {
  components: {
    Head,
  },
  layout: Layout,

  data() {
    return {
      searchQuery: '',
      filterStatus: '',
      filterMonth: '',
      filterYear: '',
      months: ["Janvier", "Février", "Mars", "Avril", "Mai", "Juin", "Juillet", "Août", "Septembre", "Octobre", "Novembre", "Décembre"],
      availableYears: ["2022", "2023", "2024"],
      sales: [
        { id: 1, date: "2024-01-01", client: "Client 1", tva: "20%", bqe: "XYZ", pvbr: "1000", topup: "200", pvnet: "800", nbMois: 12, marge: "200", statut: "Payé", dateL: "2024-01-15", comm: "10%" },
        { id: 2, date: "2024-02-15", client: "Client 2", tva: "21%", bqe: "ABC", pvbr: "1500", topup: "300", pvnet: "1200", nbMois: 10, marge: "250", statut: "Non payé", dateL: "2024-02-25", comm: "15%" },
        // Ajoutez plus de données ici
      ],
    };
  },
  computed: {
    filteredSales() {
      return this.sales.filter(sale => {
        
        return (
          (!this.filterStatus || sale.statut === this.filterStatus) &&
          (!this.filterMonth || saleMonth === this.filterMonth) &&
          (!this.filterYear || saleYear === this.filterYear) &&
          (!this.searchQuery || sale.client.toLowerCase().includes(this.searchQuery.toLowerCase()))
        );
      });
    }
  }
}
</script>

<style scoped>
/* Styles spécifiques au Dashboard */
</style>
