<script setup lang="ts">
import { ref, defineEmits, watch  } from 'vue'

const inform = ref({
  isTyping: false,
  passwordTyping: false,
  isShowPassword: false
})

let typingTimer: any | null = null
const typingDelay = 500 

const emits = defineEmits(['update-values'])

const handleInput = () => {
  inform.value.passwordTyping = false
  inform.value.isTyping = true
  if (typingTimer) {
    clearTimeout(typingTimer)
  }
  typingTimer = setTimeout(() => {
    inform.value.isTyping = false
  }, typingDelay)
}

const password = () => {
  handleInput()
  dontLook()
}

const dontLook = () => {
  inform.value.passwordTyping = true
}

const showPassword = () => {
  dontLook()
  inform.value.isShowPassword = !inform.value.isShowPassword
}

watch(inform.value, (newValue) => {
  emitValues()
})

const emitValues = () => {
  const data = {
    isTyping: inform.value.isTyping,
    passwordTyping: inform.value.passwordTyping,
    isShowPassword: inform.value.isShowPassword
  }
  emits('update-values', data)
}

const login = () =>{
  alert("o foco deste projeto é a animação e para praticar composition api do vue.js")
}
</script>

<template>
  <div class="container">
    
    <div class="content_login">
      <span><img src="/src/assets/logo.svg" alt=""> feito em <strong>vue.js e css puro</strong></span>
      <h1>Bem-vindo de volta!</h1>
      <label for="">
        <p>E-mail</p>
        <input type="email" @input="handleInput" @focus="inform.passwordTyping = false" name="email" id="email">
      </label>
      <div class="content_password">
        <label for="">
          <p>Senha</p>
          <input :type="inform.isShowPassword ? 'text': 'password' "  @input="password" @focus="dontLook" name="password" id="password">
        </label>
        <button @click="showPassword">
          <img v-if="inform.isShowPassword" src="../../../static/icons/Eye.svg" alt="">
          <img v-else src="../../../static/icons/EyeSlash.svg" alt="">
        </button>
        
      </div>
      <button @click="login" class="btnLogin">Entrar</button>
    </div>
  </div>
</template>

<style scoped>
.container{
  display: flex;
  align-items: center;
  
}
  .content_login{
    display: flex;
    width: 100%;
    flex-direction: column;
    gap: 1rem;
  }
  span{
    display: flex;
    gap: .5rem;
  }
  span img{
    width: 1rem;
  }
  .btnLogin{
    background: #232323;
    color: #e5d5c6;
    font-size: 1.1rem;
  }

  .content_password {
    display: flex;
    align-items: end;
  }
  .content_password label{
    width: 100%;
  }

  .content_password button {
    display: grid;
    place-items: center;
    width: 3.5rem;
  }

  .content_password button img{
    width: 1.8rem;
  }
  
  p{
    font-size: 1rem;
  }
  input{
    
    width: 100%;
    outline: none;
    border: none;
    background: #e9e8e4;
    height: 2.5rem;
    padding: 0 .4rem;
  }
  @media only screen and (max-width: 768px) {
    input{
      min-width: 10rem;
    }
    }
  button{
    height: 2.5rem;
    border: none;
    background: #e9e8e4;
  }
</style>