<template>
  <div class="min-h-screen bg-gray-100 flex">
    <!-- Navbar and Feedback Form -->
    <div class="flex-1">
      <Navbar />
      <FeedbackForm />
    </div>
        <!-- Home -->
        <main class="flex-1 p-6">
            <div class="bg-white shadow-md rounded-lg p-6">
                <h1 class="text-3xl font-bold mb-4">Home</h1>
                <p class="text-gray-600">Welcome to the home page!</p>
            </div>
        </main>
    </div>
</template>
<script>
import Navbar from '@/components/Navbar.vue';
import FeedbackForm from '@/components/FeedbackForm.vue';

export default {
  components: {
    Navbar,
    FeedbackForm,
  },
};
</script>