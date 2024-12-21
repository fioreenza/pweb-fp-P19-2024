<template>
  <div>
    <h1>Edit Crowdfund</h1>
    <form @submit.prevent="submitEdit">
      <label>
        Name:
        <input type="text" v-model="name" required />
      </label>
      <label>
        Target Donation:
        <input type="number" v-model="targetDonation" required />
      </label>
      <label>
        Status:
        <select v-model="status">
          <option value="open">Open</option>
          <option value="close">Close</option>
        </select>
      </label>
      <button type="submit">Save Changes</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import api from "../services/api";

export default defineComponent({
  data() {
    return {
      name: "",
      targetDonation: 0,
      status: "open",
    };
  },
  methods: {
    async fetchCrowdfund() {
      const id = this.$route.params.id;
      try {
        const response = await api.get(`/admin/${id}`);
        const data = response.data;
        this.name = data.name;
        this.targetDonation = data.targetDonation;
        this.status = data.status;
      } catch (error) {
        console.error(error);
        alert("Failed to load crowdfund details.");
      }
    },
    async submitEdit() {
      const id = this.$route.params.id;
      try {
        await api.put(`/admin/${id}/edit`, {
          name: this.name,
          targetDonation: this.targetDonation,
          status: this.status,
        });
        alert("Crowdfund updated successfully.");
        this.$router.push("/admin");
      } catch (error) {
        console.error(error);
        alert("Failed to update crowdfund.");
      }
    },
  },
  mounted() {
    this.fetchCrowdfund();
  },
});
</script>
