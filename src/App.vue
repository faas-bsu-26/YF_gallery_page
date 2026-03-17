<template>
  <div class="gallery-wrapper">
    <header>
      <h1>{{ galleryData.galleryName }}</h1>
    </header>

    <div class="grid-container">
      <div v-for="item in galleryData.items" :key="item.id" class="gallery-card">
        <div class="image-box">
          <img :src="`/images/${item.image}`" :alt="item.name" />
        </div>
        <div class="info">
          <h3>{{ item.name }}</h3>
          <span>{{ item.category }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const galleryData = ref({ galleryName: '', items: [] });

onMounted(async () => {
  try {
    // Fetching from the public folder
    const response = await fetch('/data.json');
    galleryData.value = await response.json();
  } catch (error) {
    console.error("Error loading gallery data:", error);
  }
});
</script>

<style scoped>
.gallery-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Inter', sans-serif;
}

header h1 {
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 3rem;
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 2rem;
}

.gallery-card {
  background: #fff;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
}

.gallery-card:hover {
  transform: translateY(-5px);
}

.image-box {
  width: 100%;
  aspect-ratio: 4 / 3;
  background: #eee;
}

.image-box img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.info {
  padding: 1.5rem;
}

.info h3 {
  margin: 0;
  font-size: 1.2rem;
  color: #1a1a1a;
}

.info span {
  font-size: 0.8rem;
  color: #666;
  text-transform: uppercase;
}
</style>