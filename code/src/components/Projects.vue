<script setup>
import { ref } from "vue";

const projects = ref([
  {
    preview: "https://space-tourism-website-eight-xi.vercel.app/",
    code: "https://github.com/weslleyvieira-dev/Space-Tourism-Website",
    thumb: "/assets/images/thumbs/space-tourism-website.jpg",
    title: "Space Tourism Website",
    skills: ["Vue.JS", "HTML", "CSS", "JavaScript"],
  },
  {
    preview: "https://product-list-with-cart-one-phi.vercel.app/",
    code: "https://github.com/weslleyvieira-dev/Product-List-With-Cart",
    thumb: "/assets/images/thumbs/product-list-with-cart.jpg",
    title: "Product List with Cart",
    skills: ["Vue.JS", "HTML", "CSS", "JavaScript"],
  },
  {
    preview: "https://ecommerce-product-page-tawny.vercel.app/",
    code: "https://github.com/weslleyvieira-dev/Ecommerce-Product-Page",
    thumb: "/assets/images/thumbs/ecommerce-product.jpg",
    title: "Ecommerce Product",
    skills: ["Vue.JS", "HTML", "CSS", "JavaScript"],
  },
  {
    preview: "https://sunnyside-agency-landing-page-chi-six.vercel.app/",
    code: "https://github.com/weslleyvieira-dev/Sunnyside-Agency-Landing-Page",
    thumb: "/assets/images/thumbs/sunnyside-agency-landing-page.jpg",
    title: "Sunnyside Landing Page",
    skills: ["Vue.JS", "HTML", "CSS"],
  },
  {
    preview: "https://mortgage-repayment-calculator-peach.vercel.app/",
    code: "https://github.com/weslleyvieira-dev/Mortgage-Repayment-Calculator",
    thumb: "/assets/images/thumbs/mortgage-repayment-calculator.jpg",
    title: "Mortgage Calculator",
    skills: ["Vue.JS", "HTML", "CSS", "JavaScript"],
  },
  {
    preview: "https://contact-form-ebon-six.vercel.app/",
    code: "https://github.com/weslleyvieira-dev/Contact-Form",
    thumb: "/assets/images/thumbs/contact-form-solution.jpg",
    title: "Contact Form",
    skills: ["Vue.JS", "HTML", "CSS", "JavaScript"],
  },
]);
</script>

<template>
  <div class="projects-container">
    <div class="top">
      <h1 class="text-heading-xl">Projetos</h1>
      <a href="#contact" class="view-button">CONTATO</a>
    </div>
    <div class="projects-grid">
      <div v-for="item in projects" class="project-group">
        <div class="image-group">
          <img :src="item.thumb" />
          <div class="actions-group desktop-only">
            <a class="view-button" :href="item.code" target="_blank"
              >VER CÓDIGO</a
            >
            <a class="view-button" :href="item.preview" target="_blank"
              >VER PROJETO</a
            >
          </div>
        </div>
        <h1 class="text-heading-m">{{ item.title }}</h1>
        <div class="skills-group">
          <p v-for="skill in item.skills" class="text-body">{{ skill }}</p>
        </div>
        <div class="actions-group mobile-only">
          <a class="view-button" :href="item.code" target="_blank"
            >VER CÓDIGO</a
          >
          <a class="view-button" :href="item.preview" target="_blank"
            >VER PROJETO</a
          >
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.projects-container {
  margin-bottom: 8.75rem;
}

.top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5rem;
}

.view-button {
  width: fit-content;
  font-weight: bold;
  font-size: 1rem;
  line-height: 1.625rem;
  letter-spacing: 0.143rem;
  color: white;
  text-transform: uppercase;
  text-decoration: none;
  margin: 1.125rem 0;
  padding-bottom: 0.625rem;
  border-bottom: 2px solid var(--green);
  cursor: pointer;
}

.view-button:hover {
  color: var(--green);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 4rem 2rem;
}

.project-group {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.image-group {
  position: relative;
  display: inline-block;
  margin-bottom: 0.5rem;
}

.image-group img {
  display: block;
  width: 100%;
}

.actions-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  position: absolute;
  opacity: 0;
  top: 0;
  left: 0;
  background-color: rgb(0, 0, 0, 0.75);
  z-index: 5;
  transition: all 0.3s ease;
}

.image-group:hover .actions-group {
  opacity: 1;
  pointer-events: auto;
}

.text-heading-m,
.text-body {
  text-transform: uppercase;
}

.skills-group {
  display: flex;
  gap: 1.125rem;
}

.desktop-only {
  display: flex;
}

.mobile-only {
  display: none;
}

@media (max-width: 1024px) {
  .projects-container {
    margin-bottom: 6rem;
  }

  .top {
    margin-bottom: 3.75rem;
  }

  .desktop-only {
    display: none;
  }

  .mobile-only {
    display: flex;
  }

  .actions-group {
    flex-direction: row;
    justify-content: space-between;
    gap: 2rem;
    margin-top: 0.25rem;
    position: relative;
    opacity: 1;
    background-color: transparent;
    transition: none;
  }

  .actions-group a {
    margin: 0;
  }
}

@media (max-width: 767px) {
  .top {
    margin-bottom: 2.5rem;
  }

  .text-heading-xl {
    font-size: 2.5rem;
    line-height: 2.5rem;
  }

  .projects-grid {
    grid-template-columns: repeat(1, 1fr);
    gap: 2.5rem;
  }

  .project-group {
    gap: 0.5rem;
  }

  .image-group {
    margin-bottom: 0.5rem;
  }

  .text-heading-m {
    text-align: center;
  }

  .skills-group {
    justify-content: center;
  }

  .actions-group {
    margin-top: 0.5rem;
    justify-content: space-evenly;
  }
}
</style>
