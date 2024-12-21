<template>
    <form id="feedback" @submit.prevent="submitFeedback">
      <h2>Feedback</h2>
      <input v-model="name" placeholder="Nama" />
      <input v-model="email" placeholder="Email" />
      <textarea v-model="message" placeholder="Pesan"></textarea>
      <button type="submit">Kirim</button>
    </form>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        name: '',
        email: '',
        message: '',
      };
    },
    methods: {
      async submitFeedback() {
        const feedback = {
          name: this.name,
          email: this.email,
          message: this.message,
        };
        await axios.post(`${import.meta.env.VITE_API_URL}/feedback`, feedback);
        alert('Feedback berhasil dikirim!');
      },
    },
  };
  </script>
  