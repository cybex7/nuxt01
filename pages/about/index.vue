<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <span>
      {{ slides }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      message: 'Hello, Nuxt.js with Tailwind CSS!',
      slides: [], // Initialize slides
    };
  },
  async created() {
    try {
      const response = await fetch(`${this.$config.apiBaseUrl}list-news?limit=9&sortBy=created_at&sortOrder=desc`, {
        method: "GET",
        headers: {
          accept: "application/json",
          "api-key": this.$config.apiKey,
        },
      });

      if (!response.ok) {
        throw new Error("Failed to fetch data");
      }
      const result = await response.json();
      this.slides = result;
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  },
};
</script>
