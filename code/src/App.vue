<script setup>
import Header from "./components/Header.vue";
import Skills from "./components/Skills.vue";
import Projects from "./components/Projects.vue";
import Footer from "./components/Footer.vue";
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
          Eu sou o <span class="name-underline">Weslley Vieira</span>.
        </h1>
        <p class="text-body">
          Sou um desenvolvedor front-end apaixonado por construir aplicações web
          que sejam intuitivas e acessíveis.
        </p>
        <a class="contact-button">CONTATO</a>
      </div>
      <img class="presentation-pic" src="/assets/images/profile-pic.png" />
    </div>
    <Skills />
    <Projects />
  </main>
  <Footer />
</template>

<style>
body {
  background-color: var(--black);
  position: relative;
  margin: 0;
  padding: 0 10.25rem;
}
</style>

<style scoped>
.hero-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5rem 0 12rem;
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
  width: 85%;
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
  margin: 1.125rem 0;
  padding-bottom: 0.625rem;
  border-bottom: 2px solid var(--green);
  cursor: pointer;
}

.contact-button:hover {
  color: var(--green);
}

.presentation-pic {
  justify-self: flex-end;
  height: 23rem;
  width: 23rem;
  border-radius: 50%;
  aspect-ratio: 9/16;
  object-fit: cover;
}
</style>
