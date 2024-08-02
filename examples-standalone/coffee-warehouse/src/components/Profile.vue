<template>
  <div>
    <k-form @submit="handleSubmit" :initial-values="formValues">
      <FormContent />
    </k-form>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Form as kForm } from '@progress/kendo-vue-form';
import FormContent from './ProfileComponents/FormContent.vue';

// Reactive state
const formValues = ref({
  avatar: [],
  firstName: 'Peter',
  lastName: 'Douglas',
  email: 'peter.douglas@progress.com',
  phoneNumber: '(+1) 8373-837-93-02',
  countryselected: 'Bulgaria',
  biography: null,
  team: 'lemon',
});

// Methods
const handleSubmit = (dataItem) => {
  alert(JSON.stringify(dataItem, null, 2));
  const formValuesStr = JSON.stringify(dataItem, null, 2);
  localStorage.setItem('form', formValuesStr);
};

const setAvatar = () => {
  const avatars = document.querySelectorAll('.k-avatar .k-avatar-image');
  const avatarImg = localStorage.getItem('avatar');
  if (avatarImg) {
    avatars.forEach((avatar) => {
      avatar.querySelector('img').setAttribute('src', avatarImg);
    });
  }
};

const setFormValues = () => {
  const form = localStorage.getItem('form');
  if (form) {
    formValues.value = JSON.parse(form);
  }
};

// Lifecycle hooks
onMounted(() => {
  setFormValues();
  setAvatar();
});
</script>
