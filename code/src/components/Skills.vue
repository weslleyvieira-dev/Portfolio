<script setup>
import { ref } from "vue";

const skills = ref([
  {
    name: "Vue.js",
    xp: "1.5 anos de experiência",
  },
  {
    name: "HTML",
    xp: "1.5 anos de experiência",
  },
  {
    name: "CSS",
    xp: "1.5 anos de experiência",
  },
  {
    name: "JavaScript",
    xp: "1 ano de experiência",
  },
  {
    name: "PostgreSQL",
    xp: "6 meses de experiência",
  },
  {
    name: "Java",
    xp: "6 meses de experiência",
  },
]);
</script>

<template>
  <div class="skills-container">
    <div v-for="item in skills" class="skill-group">
      <h2 class="skill-name text-heading-l">{{ item.name }}</h2>
      <p class="skill-xp text-body">{{ item.xp }}</p>
    </div>
  </div>
</template>

<style scoped>
.skills-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3.75rem 0;
  margin: 4.5rem 0 8.75rem;
}

.skill-group {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

@media (max-width: 1024px) {
  .skills-container {
    grid-template-columns: repeat(2, 1fr);
    gap: 3rem 0;
    margin: 3rem 0 6rem;
  }
}

@media (max-width: 767px) {
  .skills-container {
    grid-template-columns: repeat(1, 1fr);
    gap: 1.5rem 0;
    margin: 2.5rem 0 5rem;
    padding-bottom: 2.5rem;
    border-bottom: 1px solid white;
  }

  .skill-group {
    align-items: center;
  }
}
</style>
