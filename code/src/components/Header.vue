<script setup></script>

<template>
  <header>
    <span>weslleyvieira-dev</span>
    <div class="socials">
      <a href="https://github.com/weslleyvieira-dev" target="_blank">
        <img src="/assets/icons/github.svg" alt="GitHub" />
      </a>
      <a href="https://www.linkedin.com/in/weslleyvieira-dev/" target="_blank">
        <img src="/assets/icons/linkedin.svg" alt="LinkedIn" />
      </a>
      <a
        href="https://www.frontendmentor.io/profile/weslleyvieira-dev"
        target="_blank"
      >
        <img src="/assets/icons/frontend-mentor.svg" alt="Frontend Mentor" />
      </a>
      <a
        href="https://www.codecademy.com/profiles/weslleyvieira-dev"
        target="_blank"
      >
        <img src="/assets/icons/codecademy.svg" alt="Codecademy" />
      </a>
      <a href="https://vercel.com/weslleyvieira-projects" target="_blank">
        <img src="/assets/icons/vercel.svg" alt="Vercel" />
      </a>
    </div>
  </header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  padding: 2.5rem 0;
}

header span {
  color: white;
  font-weight: bold;
  font-size: 2rem;
  line-height: 2rem;
  letter-spacing: -0.028rem;
  margin: 0;
}

.socials {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.socials a,
.socials img {
  width: 1.5rem;
  height: 1.5rem;
}

.socials a:hover,
.socials img:hover {
  filter: brightness(0) saturate(100%) invert(77%) sepia(21%) saturate(1073%) hue-rotate(98deg) brightness(95%) contrast(92%);
}
</style>
