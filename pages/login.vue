<template>
  <sFormPage v-bind="params">
    <form @submit.prevent="userStore.login()">
      <InputGroup>
        <label for="email">Email</label>
        <InputText
          id="email"
          v-model="userStore.dataForm.email"
          aria-describedby="email-help"
          placeholder="Введите Email"
        />
        <small class="p-error" id="password-help">{{ errorsForm.email }}</small>
      </InputGroup> 

      <InputGroup>
        <label for="password">Пароль</label>
        <Password
          id="password"
          v-model="userStore.dataForm.password"
          aria-describedby="password-help"
          placeholder="Введите пароль"
          :feedback="false"
          toggleMask
        />
        <small class="p-error" id="password-help">{{ errorsForm.password }}</small>
      </InputGroup>

      <AgreementForm :agreement="agreement" />
      <div class="mb-4 mt-4">
        <Button type="submit" :label="params.btnName" class="w-100 btn-lg" />
      </div>
      <div class="mb-3 text-center" style="font-size: 14px">
        Еще нет аккаунта?
        <NuxtLink to="/registration" class="text-primary">Регистрация</NuxtLink>
      </div>
    </form>
  </sFormPage>
</template>

<script setup>
// import Auth from '@/services/auth';

import { useUserStore } from '@/store/userStore'; 

definePageMeta({
  layout: 'auth',
});

const errorsForm = ref({
  email: '',
  password: '',
  passwordConfirm: '',
});

const params = {
  title: 'Авторизация', 
  bgImage: '/img/reg-bg-2.jpg',
  btnName: 'Войти',
};

const userStore = useUserStore(); 
</script>
