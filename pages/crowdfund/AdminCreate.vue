<template>
  <div>
    <h1>Create Crowdfund</h1>
    <form @submit.prevent="submitCrowdfund">
      <label>
        Name:
        <input type="text" v-model="name" required />
      </label>
      <label>
        Target Donation:
        <input type="number" v-model="targetDonation" required />
      </label>
      <button type="submit">Create</button>
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
    };
  },
  methods: {
    async submitCrowdfund() {
      try {
        await api.post("/admin/create", {
          name: this.name,
          targetDonation: this.targetDonation,
          createdBy: "Admin",
        });
        alert("Crowdfund created successfully.");
        this.$router.push("/admin");
      } catch (error) {
        console.error(error);
        alert("Failed to create crowdfund.");
      }
    },
  },
});
</script>
