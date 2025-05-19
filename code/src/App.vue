<script setup>
import Header from "./components/Header.vue";
import Skills from "./components/Skills.vue";
import Projects from "./components/Projects.vue";
import Contact from "./components/Contact.vue";
import BackgroundPattern from "./components/BackgroundPattern.vue";
</script>

<template>
  <BackgroundPattern />
  <Header />
  <main>
    <div class="hero-container">
      <div class="presentation-container">
        <h1 class="text-heading-xl">Bem-vindo(a)!</h1>
        <h1 class="text-heading-xl">
          Eu sou <span class="name-underline">Weslley Vieira.</span>
        </h1>
        <p class="text-body">
          Sou um desenvolvedor front-end, formado em Engenharia de Software,
          focado em criar interfaces web elegantes, intuitivas e totalmente
          acessíveis.
        </p>
        <a href="#contact" class="contact-button">CONTATO</a>
      </div>
      <img
        class="presentation-pic"
        src="/assets/images/profile-pic.jpg"
        draggable="false"
      />
    </div>
    <Skills />
    <Projects />
    <Contact />
  </main>
</template>

<style>
html {
  scroll-behavior: smooth;
}

body {
  background-color: var(--black);
  position: relative;
  margin: 0;
  padding: 0 10rem;
}

@media (max-width: 1024px) {
  body {
    padding: 0 1.875rem;
  }
}

@media (max-width: 767px) {
  body {
    padding: 0 1rem;
  }
}
</style>

<style scoped>
.hero-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5rem 0 4.5rem;
  border-bottom: 1px solid white;
}

.presentation-container {
  display: flex;
  flex-direction: column;
  width: 60%;
}

.text-heading-xl {
  margin-top: 1rem;
}

.name-underline {
  border-bottom: 6px solid var(--green);
  display: inline-block;
  line-height: 1;
}

.presentation-container p {
  margin: 3rem 0;
}

.contact-button {
  width: fit-content;
  font-weight: bold;
  font-size: 1rem;
  line-height: 1.625rem;
  letter-spacing: 0.143rem;
  color: white;
  text-transform: uppercase;
  text-decoration: none;
  margin: 1.125rem 0 0;
  padding-bottom: 0.625rem;
  border-bottom: 2px solid var(--green);
  cursor: pointer;
}

.contact-button:hover {
  color: var(--green);
}

.presentation-pic {
  height: 23rem;
  width: 23rem;
  border-radius: 50%;
  object-fit: cover;
}

@media (max-width: 1024px) {
  .hero-container {
    padding: 4rem 0;
  }

  .text-heading-xl {
    font-size: 4rem;
    line-height: 4rem;
    margin-top: 0;
  }

  .presentation-container p {
    font-size: 1rem;
    margin: 2.5rem 0 1.5rem;
  }

  .presentation-pic {
    height: 16rem;
    width: 16rem;
  }
}

@media (max-width: 767px) {
  .hero-container {
    flex-direction: column-reverse;
    gap: 2.5rem;
    padding: 2.5rem 0 5rem;
  }

  .presentation-container {
    width: 100%;
    align-items: center;
  }

  .text-heading-xl {
    font-size: 2.3rem;
    line-height: 3rem;
    text-align: center;
  }

  .presentation-container p {
    text-align: center;
    margin: 1.5rem 0;
  }

  .contact-button {
    margin: 0;
  }

  .presentation-pic {
    z-index: 10;
  }
}
</style>
