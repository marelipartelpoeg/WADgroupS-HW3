<template>
    <div>
      <main>
        <section class="signup-page">
          <div class="form-container">
            <form @submit.prevent="submitForm">
              <div class="container">
                <div class="column">
                  <label>Email</label><br>
                  <label>Password</label>
                </div>
                <div class="column">
                  <input type="text" placeholder="Email" name="email" required><br>
                  <input type="password" placeholder="Password" name="psw" required v-model="password">
                </div>
              </div><br>
              <button type="submit">Signup</button>
              <p v-if="passwordValidationMessage">{{ passwordValidationMessage }}</p>
            </form><br>
          </div>
        </section>
      </main>
    </div>
</template>

<script>
export default {
  data() {
    return {
      password: "",
      passwordValidationMessage: "",
    };
  },
  methods: {
    submitForm() {
      // Implement password validation logic
      const isValid = this.validatePassword(this.password);

      if (isValid) {
        // Handle successful form submission
        console.log("Form submitted successfully!");
        this.$router.push({ name: 'main' });
      } else {
        // Display password validation message
        this.passwordValidationMessage =
            "Password is not valid. Password must be 8-14 characters long, contain at least one uppercase letter, two lowercase letters, one digit, start with an uppercase letter, and include the character \"_\".";
      }
    },
    validatePassword: function (password) {
      const minLength = 8;
      const maxLength = 14;
      // Password length check
      if (password.length < minLength || password.length > maxLength) {
        console.log("Wrong length")
        return false;
      }

      // At least one uppercase alphabet character
      if (!/[A-Z]/.test(password)) {
        console.log("No uppercase letters")
        return false;
      }
      // At least two lowercase alphabet characters
      if (!/[a-z]/.test(password) || password.length < 2) {
        console.log("Less than 2 lowercase letters")
        return false;
      }

      // At least one numeric value
      if (!/\d/.test(password)) {
        console.log("No digits")
        return false;
      }

      // Should start with an uppercase alphabet
      if (!password[0].match(/[A-Z]/)) {
        console.log("Doesn't start with uppercase letter")
        return false;
      }

      // Should include the character "_"
      if (!password.includes("_")) {
        console.log("Doesn't include the character \"_\"")
        return false;
      }

      // If all conditions pass, the password is valid
      return true;
    },
  },
};
</script>


<style scoped>
form {
  border-radius: 25px;
  border: 2px solid #2a2cc9;
  background-color:rgb(231, 231, 231);
}

label {
  padding: 12px 15px;
  margin: -1px 10px;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

input {
  width: 100%;
  padding: 12px 20px;
  display: flex;
  border: 1px solid #ccc;
  border-radius: 15px;
  box-sizing: border-box;
}

button {
  background-color: #2a2cc9;
  color: white;
  padding: 14px 20px;
  margin: 8px 0px 15px 0px;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  width: 30%;
}

p {
  width: 320px;
  padding: 0px 15px;
}

button:hover {
  opacity: 0.7;
}

.form-container {
  margin-top: 108px;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.container {
  width: 350px;
  padding: 15px 0px;
  display: inline-flex;
}
</style>
  