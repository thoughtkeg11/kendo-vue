<template>
  <div class="header header-bg">
    <div class="nav-container">
      <div class="title">
        <h1>{{ warehouseMessage }}</h1>
        <span class="vl"></span>
        <h2>{{ teamMessage }}</h2>
      </div>
      <DropDownList
        :style="{ width: '230px', height: '30px' }"
        class="localeDropDownList"
        :value="currentLocale"
        :text-field="'language'"
        @change="localeChange"
        :data-items="locales"
      />
      <DropDownList
        :data-items="themes"
        :text-field="'text'"
        :popup-settings="themesPopupSettings"
        :value-render="myDropDownValueTemplate"
        class="ddl-theme"
        @change="onThemeChange"
      >
        <template v-slot:myDropDownValueTemplate="{}">
          <div style="margin: auto 8px auto 10px">
            <span class="k-icon k-i-palette"> </span>
          </div>
        </template>
      </DropDownList>
      <Avatar :rounded="'full'" :type="'image'" :style="{ width: '40px', height: '40px', 'flex-basis': '40px' }">
        <img src="../assets/images/user.jpg" />
      </Avatar>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, inject, defineEmits } from 'vue';
import { Avatar } from '@progress/kendo-vue-layout';
import { DropDownList } from '@progress/kendo-vue-dropdowns';
import { provideLocalizationService } from '@progress/kendo-vue-intl';

// Define emits for the events you want to emit
const emit = defineEmits(['localeChange', 'themeChange']);

// Injecting the localization service
const kendoLocalizationService = inject('kendoLocalizationService', null);

// Reactive state
const theme = ref('default');
const currentLocale = ref(null);
const locales = [
  { language: 'English', locale: 'en' },
  { language: 'French', locale: 'fr' },
  { language: 'Spanish', locale: 'es' }
];
const themes = [
  { href: 'default', text: 'Default' },
  { href: 'bootstrap', text: 'Bootstrap' },
  { href: 'material', text: 'Material' }
];
const myDropDownValueTemplate = 'myDropDownValueTemplate';
const themesPopupSettings = { width: '150px' };

// Computed properties
const warehouseMessage = computed(() => {
  return provideLocalizationService(kendoLocalizationService).toLanguageString('warehouse', 'Landing');
});

const teamMessage = computed(() => {
  return provideLocalizationService(kendoLocalizationService).toLanguageString('team', 'Patient');
});

// Methods
const onThemeChange = (e) => {
  theme.value = e.value.href;
  const linkTag = document.getElementById('theme-link');
  linkTag.setAttribute('href', `${process.env.BASE_URL}/static/themes/kendo-theme-${theme.value}/all.css`);
  emit('themeChange', e.value.text); // Emit the themeChange event
};

const localeChange = (e) => {
  currentLocale.value = e.target.value;
  emit('localeChange', currentLocale.value); // Emit the localeChange event
};

// Initialization (similar to created lifecycle hook)
currentLocale.value = locales[0];
</script>


<style scoped>
.ddl-theme {
  width: 60px;
  min-width: 60px;
}

.localeDropDownList {
  min-width: 100px;
  margin: 10px;
}

.k-dropdownlist {
  min-height: 30px;
}
</style>
