<script setup>
import { ref, reactive, onMounted, watch } from "vue";
import emailjs from "@emailjs/browser";
import Header from "./Header.vue";

const isSubmitted = ref(false);

const formData = reactive({
  name: "",
  email: "",
  message: "",
  time: "",
});

const errors = reactive({
  name: "",
  email: "",
  message: "",
  captcha: "",
});

function validateForm() {
  Object.keys(errors).forEach((key) => (errors[key] = ""));
  const nameRegex = /^[A-Za-zÀ-ÖØ-öø-ÿ\s'-]+$/;
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/;

  if (!formData.name) {
    errors.name = "Campo obrigatório";
  } else if (
    !nameRegex.test(formData.name) ||
    formData.name.length < 2 ||
    formData.name.length > 50
  ) {
    errors.name = "Nome inválido";
  }

  if (!formData.email) {
    errors.email = "Campo obrigatório";
  } else if (!emailRegex.test(formData.email)) {
    errors.email = "Formato inválido";
  }

  if (!formData.message) {
    errors.message = "Campo obrigatório";
  }

  const captchaResponse = grecaptcha.getResponse(window.recaptchaWidgetId);
  if (!captchaResponse) {
    errors.captcha = "Confirme que você não é um robô";
  }

  return Object.values(errors).every((error) => error === "");
}

function submitForm() {
  isSubmitted.value = true;

  if (validateForm()) {
    sendEmail();
  }
}

function sendEmail() {
  formData.time = new Date().toLocaleString("pt-BR", {
    timeZone: "America/Sao_Paulo",
  });

  emailjs
    .send(
      "wellsz-projects",
      "wellsz-portfolio-contact",
      {
        name: formData.name,
        email: formData.email,
        message: formData.message,
        time: new Date().toLocaleString("pt-BR", {
          timeZone: "America/Sao_Paulo",
        }),
        "g-recaptcha-response": grecaptcha.getResponse(
          window.recaptchaWidgetId
        ),
      },
      {
        publicKey: "t7EhqsPPj5zZj1qPz",
      }
    )
    .then(
      () => {
        alert("Email enviado com sucesso!");
        window.location.reload(true);
      },
      (error) => {
        console.log("FAILED...", error);
        alert("Erro ao enviar o email. Tente novamente.");
        window.location.reload(true);
      }
    );
}

function resetRecaptcha() {
  grecaptcha.reset(window.recaptchaWidgetId);
}

onMounted(() => {
  const checkGrecaptcha = setInterval(() => {
    if (window.grecaptcha && document.getElementById("contact-recaptcha")) {
      clearInterval(checkGrecaptcha);
      window.recaptchaWidgetId = grecaptcha.render("contact-recaptcha", {
        sitekey: "6LdWnDsrAAAAAPtbQf0i3V0XnfzdYEiqvcxKjIjZ",
        theme: "dark",
        "expired-callback": resetRecaptcha,
      });
    }
  }, 1000);
});

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
    <div id="contact" class="contact-container">
      <div class="message-container">
        <h1 class="text-heading-xl">Contato</h1>
        <p class="text-body">
          Estou à disposição para novas oportunidades.
          <br />Deixe seu contato que retornarei o mais breve possível!
        </p>
      </div>
      <form id="contact-form" @submit.prevent="submitForm" class="contact-form">
        <div
          class="field-group"
          :class="{ 'has-error': isSubmitted && errors.name }"
        >
          <input id="time" name="time" type="hidden" v-model="formData.time" />
          <input
            id="name"
            name="name"
            placeholder="NOME"
            v-model.trim="formData.name"
            type="text"
            autocomplete="name"
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
            v-model.trim="formData.email"
            type="email"
            autocomplete="email"
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
            v-model.trim="formData.message"
            @input="formData.message = formData.message.toUpperCase()"
          />
          <span v-if="isSubmitted && errors.message" class="error">{{
            errors.message
          }}</span>
        </div>

        <div id="contact-recaptcha" class="g-recaptcha"></div>
        <span v-if="isSubmitted && errors.captcha" class="error">
          {{ errors.captcha }}
        </span>

        <button type="submit" value="ENVIAR MENSAGEM" class="submit-button">
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
  width: 100%;
  background-color: var(--dark-grey);
  padding: 5rem 10rem;
  box-sizing: border-box;
}

.contact-container {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid white;
}

.message-container {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.contact-form {
  display: flex;
  flex-direction: column;
  min-width: 35%;
  gap: 0;
  padding: 2rem 0 3rem;
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
  resize: none;
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
  align-self: end;
}

.contact-button,
.submit-button {
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

.submit-button {
  margin-top: 2rem;
}

.contact-button:hover,
.submit-button:hover {
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

@media (max-width: 1024px){
  footer {
    padding: 3.75rem 1.875rem 2.5rem;
  }

  .contact-container {
    flex-direction: column;
    align-items: center;
    gap: 3rem;
  }

  .message-container {
    align-items: center;
    text-align: center;
    width: 28rem;
    gap: 1.25rem;
  }

  .contact-form {
    width: 28rem;
    padding: 0 0 5rem;
  }

  footer header {
    margin-top: 1.875rem;
  }
}

@media (max-width: 767px){
  footer {
    padding: 3.75rem 1rem;
  }

  .message-container {
    width: 100%;
  }

  .text-heading-xl {
    font-size: 2.5rem;
    line-height: 2.5rem;
  }

  .text-body {
    font-size: 0.9rem;
    line-height: 1.5rem;
    text-align: center;
  }

  .contact-form {
    width: 100%;
  }

  footer header {
    margin-top: 2.5rem;
  }
}
</style>
