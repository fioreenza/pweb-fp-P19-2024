<template>
    <div class="min-h-screen bg-gray-50 flex">
      <!-- Sidebar -->
      <aside class="w-64 bg-blue-900 text-white p-8 shadow-lg">
        <h2 class="text-2xl font-semibold mb-8">Dashboard</h2>
        <ul class="space-y-6">
          <li>
            <NuxtLink to="/crowdfund" class="text-lg hover:text-blue-300 transition duration-300">See All Crowdfund</NuxtLink>
          </li>
          <li>
            <NuxtLink to="/crowdfund/favorite" class="text-lg hover:text-blue-300 transition duration-300">My Favorite Crowdfund</NuxtLink>
          </li>
        </ul>
      </aside>
  
      <!-- Main Content -->
      <main class="flex-1 p-8 bg-gray-50">
        <div class="bg-white shadow-lg rounded-xl p-6">
          <h1 class="text-3xl font-bold text-gray-800 mb-8">My Favorite Crowdfund</h1>
          
          <!-- Favorite Crowdfund List -->
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
            <div
              v-for="crowdfund in favoriteCrowdfunds"
              :key="crowdfund.id"
              class="bg-white border border-gray-200 rounded-xl shadow-md hover:shadow-xl transition-shadow duration-300 p-6"
            >
              <h3 class="text-xl font-semibold text-gray-800">{{ crowdfund.name }}</h3>
              <p class="text-gray-600 mt-2">Target: <span class="font-semibold text-green-600">${{ crowdfund.target }}</span></p>
              <p class="text-gray-600 mt-2">Current Donation: <span class="font-semibold text-blue-600">${{ crowdfund.current_donation }}</span></p>
              <NuxtLink :to="`/crowdfund/${crowdfund.id}`" class="text-blue-500 hover:text-blue-700 mt-4 inline-block font-medium">See Details</NuxtLink>
            </div>
          </div>
        </div>
      </main>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        favoriteCrowdfunds: [
          { id: 1, name: "Crowdfund 1", target: "1000000", current_donation: 500000 },
          { id: 2, name: "Crowdfund 2", target: "500000", current_donation: 250000 },
        ]
      };
    }
  };
  </script>
  
  <style scoped>
  /* Optional: Custom styling if needed */
  </style>
  