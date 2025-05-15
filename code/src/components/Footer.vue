<script setup>
import { ref, reactive, computed, watch } from "vue";
import emailjs from "@emailjs/browser";
import Header from "./Header.vue";

const isSubmitted = ref(false);
const currentTimestamp = ref("");

const formData = reactive({
  name: "",
  email: "",
  message: "",
});

const errors = reactive({
  name: "",
  email: "",
  message: "",
});

function validateForm() {
  Object.keys(errors).forEach((key) => (errors[key] = ""));

  if (!formData.name) {
    errors.name = "Campo obrigatório";
  }

  if (!formData.email) {
    errors.email = "Campo obrigatório";
  } else if (!/\S+@\S+\.\S+/.test(formData.email)) {
    errors.email = "Formato inválido";
  }

  if (!formData.message) {
    errors.message = "Campo obrigatório";
  }

  return Object.values(errors).every((error) => error === "");
}

function submitForm() {
  isSubmitted.value = true;
  if (validateForm()) {
    currentTimestamp.value = new Date().toISOString();
    sendEmail();
    clearForm();
  }
}

function clearForm() {
  Object.keys(formData).forEach((key) => (formData[key] = ""));
}

function sendEmail() {
  emailjs
    .sendForm("wellsz-projects", "wellsz-portfolio-contact", "#contact-form", {
      publicKey: "t7EhqsPPj5zZj1qPz",
    })
    .then(
      () => {
        aler("Email enviado com sucesso!");
      },
      (error) => {
        console.log("FAILED...", error);
        alert("Erro ao enviar o email. Atualize a página e tente novamente.");
      }
    );
}

watch(
  () => formData,
  (newValue) => {
    Object.keys(errors).forEach((key) => {
      if (newValue[key]) {
        errors[key] = "";
      }
    });
  },
  { deep: true }
);
</script>

<template>
  <footer>
    <div class="contact-container">
      <h1 class="text-heading-xl">Contato</h1>
      <form id="contact-form" @submit.prevent="submitForm" class="contact-form">
        <div
          class="field-group"
          :class="{ 'has-error': isSubmitted && errors.name }"
        >
        <input
    type="hidden"
    name="timestamp"
    :value="currentTimestamp"
  />
          <input
            id="name"
            name="name"
            placeholder="NOME"
            v-model="formData.name"
            type="text"
            @input="formData.name = formData.name.toUpperCase()"
          />
          <span v-if="isSubmitted && errors.name" class="error">{{
            errors.name
          }}</span>
        </div>

        <div
          class="field-group"
          :class="{ 'has-error': isSubmitted && errors.email }"
        >
          <input
            id="email"
            name="email"
            placeholder="EMAIL"
            v-model="formData.email"
            type="email"
            @input="formData.email = formData.email.toUpperCase()"
          />
          <span v-if="isSubmitted && errors.email" class="error">{{
            errors.email
          }}</span>
        </div>

        <div
          class="field-group"
          :class="{ 'has-error': isSubmitted && errors.message }"
        >
          <textarea
            id="message"
            name="message"
            placeholder="MENSAGEM"
            v-model="formData.message"
            @input="formData.message = formData.message.toUpperCase()"
          />
          <span v-if="isSubmitted && errors.message" class="error">{{
            errors.message
          }}</span>
        </div>

        <div
          name="g-recaptcha-response"
          class="g-recaptcha"
          data-sitekey="6LdWnDsrAAAAAPtbQf0i3V0XnfzdYEiqvcxKjIjZ"
          data-theme="dark"
        ></div>
        <button type="submit" value="ENVIAR MENSAGEM" class="contact-button">
          ENVIAR MENSAGEM
        </button>
      </form>
    </div>
    <Header />
  </footer>
</template>

<style scoped>
footer {
  position: absolute;
  left: 0;
  width: 100vw;
  background-color: var(--dark-grey);
  padding: 5.25rem 10.25rem;
  box-sizing: border-box;
}

.contact-container {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid white;
}

.contact-form {
  display: flex;
  flex-direction: column;
  min-width: 35%;
  gap: 0;
  padding-bottom: 5.75rem;
}

.field-group {
  display: flex;
  flex-direction: column;
  gap: 0.375rem;
  width: 100%;
  margin: 0 0 2rem;
}

.field-group input,
.field-group textarea {
  font-size: 1rem;
  font-weight: 600;
  line-height: 1.625rem;
  text-transform: uppercase;
  margin: 0;
  padding: 1rem 1.5rem 1.75rem;
  height: 1.625rem;
  width: 100%;
  box-sizing: border-box;
  color: white;
  border: none;
  outline: none;
  border-bottom: 1px solid white;
  background-color: transparent;
}

.field-group textarea {
  height: 6.75rem;
  padding: 0 1.5rem 0.5rem;
}

.field-group input:focus,
.field-group textarea:focus {
  border-bottom: 1px solid var(--green);
}

.field-group.has-error input,
.field-group.has-error textarea {
  border-bottom-color: #ff6f5b;
}

.g-recaptcha {
  align-self: center;
  margin-bottom: 2rem;
}

.contact-button {
  align-self: flex-end;
  width: fit-content;
  font-weight: bold;
  font-size: 1rem;
  line-height: 1.625rem;
  letter-spacing: 0.143rem;
  background-color: transparent;
  border: none;
  color: white;
  text-transform: uppercase;
  text-decoration: none;
  padding: 0 0 0.625rem;
  border-bottom: 2px solid var(--green);
  cursor: pointer;
}

.contact-button:hover {
  color: var(--green);
}

.error:empty {
  display: none;
}

.error {
  color: #ff6f5b;
  font-size: 0.75rem;
  line-height: 1rem;
  letter-spacing: -0.011rem;
  margin: 0;
  display: block;
  align-self: flex-end;
}

.field-group.has-error input,
.field-group.has-error textarea {
  background-image: url("/assets/icons/alert-circle.svg");
  background-repeat: no-repeat;
  background-position: right;
}

footer header {
  margin-top: 3rem;
  padding: 0;
}
</style>
