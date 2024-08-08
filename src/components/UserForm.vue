<template>
  <div class="user-form">
    <h1>Formulaire de Saisie</h1>
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Nom:</label>
        <input type="text" v-model="name" @blur="validateName" />
        <span v-if="errors.name" class="error">{{ errors.name }}</span>
      </div>
      
      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="email" @blur="validateEmail" />
        <span v-if="errors.email" class="error">{{ errors.email }}</span>
      </div>
      
      <div>
        <label for="phone">Numéro de Téléphone:</label>
        <input type="text" v-model="phone" @blur="validatePhone" />
        <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
      </div>
      
      <button type="submit">Soumettre</button>
      
      <p v-if="confirmationMessage" class="confirmation">{{ confirmationMessage }}</p>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      email: '',
      phone: '',
      errors: {},
      confirmationMessage: ''
    };
  },
  methods: {
    validateName() {
      if (!this.name) {
        this.errors.name = 'Le nom est requis.';
      } else {
        delete this.errors.name;
      }
    },
    validateEmail() {
      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!this.email) {
        this.errors.email = 'L\'email est requis.';
      } else if (!emailPattern.test(this.email)) {
        this.errors.email = 'L\'email n\'est pas valide.';
      } else {
        delete this.errors.email;
      }
    },
    validatePhone() {
      const phonePattern = /^[0-9]{1}$/;
      if (!this.phone) {
        this.errors.phone = 'Le numéro de téléphone est requis.';
      } else if (!phonePattern.test(this.phone)) {
        this.errors.phone = 'Le numéro de téléphone doit comporter 8 chiffres.';
      } else {
        delete this.errors.phone;
      }
    },
    submitForm() {
      this.validateName();
      this.validateEmail();
      this.validatePhone();

      if (Object.keys(this.errors).length === 0) {
        this.confirmationMessage = 'Formulaire soumis avec succès!';
        this.clearForm();
      }
    },
    clearForm() {
      this.name = '';
      this.email = '';
      this.phone = '';
    }
  }
};
</script>

<style scoped>
.user-form  {
    border: 3px solid rgb(189, 171, 171);
    padding: 60px;
}
.error {
  color: red;
}
.confirmation {
  color: green;
  margin-top: 10px;
}

form {
    width: 300px;
}


div {
    display: flex;
    flex-direction: column;
}

input {
    border-radius: 5px;
    height: 30px;
}

label {
    margin-top: 10px;
}

button {
    margin-top: 20px;
    width: 300px;
    height: 30px;
    background: blue;
    border: none;
    border-radius: 10px;
    color: #ffffff;
}


</style>
