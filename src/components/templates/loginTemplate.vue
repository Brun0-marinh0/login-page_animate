<script setup la components: { formLogin, CharacterLogin }, ng="ts">
  import FormLogin from '../organisms/FormLogin.vue';
  import CharacterLogin from '../molecules/CharacterLogin.vue'

  import { ref } from 'vue'

  const values = ref({
    isTyping: false,
    passwordTyping: false,
    isShowPassword: false
})

  const updateInform = (data) => {
    values.value = data
  }

</script>

<template>
    <main>
        <Form-login @update-values="updateInform" class="form"/>

        <CharacterLogin  class="character"
          :isTyping="values.isTyping" 
          :passwordTyping="values.passwordTyping"
          :isShowPassword="values.isShowPassword"
        />

    </main>
</template>

<style scoped>
    main{
        display: grid;
        grid-template: 1fr / 1fr 1fr;
        gap: 2rem;
        grid-template-areas: 'form character';
        height: 100vh;
        width: 100%;
        padding: 12vw 12vw;
    }
    .form{
      grid-area: form;
    }
    .character{
      grid-area: character;
    }
    @media only screen and (max-width: 768px) {
      main{
        padding: 6vw 6vw;
        
      }
    }
    @media only screen and (max-width: 600px) {
      main{
        grid-template: 1fr 1fr/ 1fr;
        grid-template-areas: 
        'character'
        'form'
        ;
        gap: 1rem;
      }
    }
</style>