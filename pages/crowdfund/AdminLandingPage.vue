<template>
  <div>
    <h1>Admin Dashboard</h1>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Target Donation</th>
          <th>Status</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="crowdfund in crowdfunds" :key="crowdfund._id">
          <td>{{ crowdfund._id }}</td>
          <td>{{ crowdfund.name }}</td>
          <td>{{ crowdfund.targetDonation }}</td>
          <td>{{ crowdfund.status }}</td>
          <td>
            <button @click="goToDetail(crowdfund._id)">Detail</button>
            <button @click="goToEdit(crowdfund._id)">Edit</button>
            <button @click="deleteCrowdfund(crowdfund._id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
    <button @click="goToCreate">Create New Crowdfund</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useRouter } from "vue-router";
import api from "../services/api";

export default defineComponent({
  data() {
    return {
      crowdfunds: [] as Array<{
        _id: string;
        name: string;
        targetDonation: number;
        status: string;
      }>,
    };
  },
  methods: {
    async fetchCrowdfunds() {
      try {
        const response = await api.get("/admin");
        this.crowdfunds = response.data;
      } catch (error) {
        console.error(error);
        alert("Failed to load crowdfunds.");
      }
    },
    goToDetail(id: string) {
      this.$router.push(`/admin/${id}`);
    },
    goToEdit(id: string) {
      this.$router.push(`/admin/${id}/edit`);
    },
    async deleteCrowdfund(id: string) {
      try {
        await api.delete(`/admin/${id}`);
        alert("Crowdfund deleted successfully.");
        this.fetchCrowdfunds();
      } catch (error) {
        console.error(error);
        alert("Failed to delete crowdfund.");
      }
    },
    goToCreate() {
      this.$router.push("/admin/create");
    },
  },
  mounted() {
    this.fetchCrowdfunds();
  },
});
</script>
