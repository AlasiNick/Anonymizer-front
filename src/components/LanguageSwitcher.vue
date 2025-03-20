<template>
  <div class="language-switcher">
    <select 
      v-model="currentLocale" 
      @change="changeLanguage"
      class="language-select"
      :title="$t('language')"
    >
      <option value="en">English</option>
      <option value="ee">Eesti</option>
    </select>
  </div>
</template>

<script>
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';

export default {
  name: 'LanguageSwitcher',
  setup() {
    const { locale } = useI18n();
    const currentLocale = ref(locale.value);

    const changeLanguage = () => {
      locale.value = currentLocale.value;
      localStorage.setItem('language', currentLocale.value);
    };

    return {
      currentLocale,
      changeLanguage
    };
  }
};
</script>

<style lang="scss" scoped>
.language-switcher {
  display: inline-block;
}

.language-select {
  background: transparent;
  border: 1px solid rgba(255, 255, 255, 0.3);
  color: white;
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s ease;

  &:hover {
    border-color: rgba(255, 255, 255, 0.5);
  }

  &:focus {
    outline: none;
    border-color: white;
  }

  option {
    background: #3865F2;
    color: white;
  }
}
</style> 