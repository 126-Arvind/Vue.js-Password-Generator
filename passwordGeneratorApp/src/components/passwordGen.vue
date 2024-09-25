<script setup>
import { ref } from "vue";

const passwordLength = ref(12);
const includeUppercase = ref(true);
const includeNumbers = ref(true);
const includeSymbols = ref(true);
const generatedPassword = ref("");

const generatePassword = () => {
  const lowercaseChars = "abcdefghijklmnopqrstuvwxyz";
  const uppercaseChars = includeUppercase.value
    ? "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    : "";
  const numberChars = includeNumbers.value ? "0123456789" : "";
  const symbolChars = includeSymbols.value ? "!@#$%^&*()_+[]{}|;:,.<>?/~`" : "";

  const allChars = lowercaseChars + uppercaseChars + numberChars + symbolChars;

  let password = "";
  for (let i = 0; i < passwordLength.value; i++) {
    const randomIndex = Math.floor(Math.random() * allChars.length);
    password += allChars[randomIndex];
  }

  generatedPassword.value = password;
};
</script>

<template>
  <div class="password-generator-container">
    <h2 class="password-generator-title">🔒 Password Generator</h2>
    <div class="settings-container">
      <div class="setting">
        <label for="length">Password Length:</label>
        <input
          type="number"
          id="length"
          v-model="passwordLength"
          min="4"
          max="32"
        />
      </div>
      <div class="setting">
        <label for="includeUppercase">Include Uppercase:</label>
        <input type="checkbox" id="includeUppercase" v-model="includeUppercase" />
      </div>
      <div class="setting">
        <label for="includeNumbers">Include Numbers:</label>
        <input type="checkbox" id="includeNumbers" v-model="includeNumbers" />
      </div>
      <div class="setting">
        <label for="includeSymbols">Include Symbols:</label>
        <input type="checkbox" id="includeSymbols" v-model="includeSymbols" />
      </div>
    </div>
    <button @click="generatePassword" class="generate-button">
      Generate Password
    </button>
    <div class="generated-password">
      <strong>Your Password : </strong> <span>{{ generatedPassword }}</span>
    </div>
  </div>
</template>

<style scoped>
.password-generator-container {
  max-width: 500px;
  margin: 50px auto;
  padding: 30px;
  background: linear-gradient(135deg, #ff7e5f, #feb47b);
  border-radius: 10px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  color: #fff;
  text-align: center;
  font-family: 'Arial', sans-serif;
}

.password-generator-title {
  font-size: 28px;
  margin-bottom: 20px;
  color: #fff;
}

.settings-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 15px;
}

.setting {
  flex: 1 1 calc(50% - 15px);
  background: rgba(255, 255, 255, 0.2);
  padding: 10px;
  border-radius: 5px;
}

.setting label {
  display: block;
  font-size: 16px;
  margin-bottom: 5px;
  color: #000000;
  font-size: 18px;
}

.setting input[type="number"] {
  width: 90%;
  padding: 10px;
  border-radius: 4px;
  border: none;
}

.setting input[type="checkbox"] {
  margin-top: 5px;
}

.generate-button {
  margin-top: 20px;
  padding: 15px 30px;
  font-size: 18px;
  background-color: #3498db;
  color: #0a0a0a;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.generate-button:hover {
  background-color: #2980b9;
}

.generated-password {
  margin-top: 30px;
  padding: 15px;
  color: black;
  font-size: 20px;
  border: 2px dashed #fff;
  border-radius: 10px;
  background-color: rgba(0, 0, 0, 0.1);
}

.generated-password strong {
  font-size: 18px;
}

.generated-password span {
  font-size: 20px;
  color: #f7e018;
  word-wrap: break-word;
}
</style>
