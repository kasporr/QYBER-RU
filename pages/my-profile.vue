<template>
  <div v-if="globalStore.userData.user_nicename">
    <ProfileHead
      :breadcrumbArr="[{ label: 'Личный кабинет' }]"
      :img="imgRef"
      :avatarText="avatarText"
      :profileData="globalStore.userData"
    >
      <h1 :class="globalStore.userData.user_verification == true ? 'verifired' : ''">
        {{ globalStore.userData.user_nicename }}
      </h1>
      <span class="sProfileHead__name">{{ globalStore.userData.display_name }}</span>
      <div class="sProfileHead__status online">Онлайн</div>
      <div class="sProfileHead__time">На сайте с {{ user_registered }}</div>
      <div class="row">
        <div class="col-auto">
          <Badge severity="secondary" value="Кибер Таланты" class="p-badge-outline" />
        </div>
        <div class="col-auto">
          <Badge severity="danger" value="Кибер Атланты" class="p-badge-outline" />
        </div>
      </div>
    </ProfileHead>
    <MyProfileBlock :profileData="globalStore.userData" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useUserStore } from '@/store/userStore';
import { useGlobalStore } from '@/store/globalStore';

const userStore = useUserStore();
const globalStore = useGlobalStore();
// console.log(userStore.userData);
const imgRef = ref(null);
const avatarText = ref(null);
const user_registered = ref('');

onMounted(async () => {
  await userStore.getUserData();
  imgRef.value = globalStore.user_avatar;
  avatarText.value = globalStore.user_first_letter;
});
</script>
<style lang="scss"></style>
