<template>
  <div>
    <div class="info-page main-content">
      <div class="content">
        <div class="section-1">
          <h1>Kendo UI for Vue</h1>
          <h2>Build Professional-Grade Vue UI</h2>

          <a
            class="github-link"
            target="_blank"
            href="https://github.com/telerik/kendo-vue/tree/master/examples-standalone/coffee-warehouse"
          >
            <img src="../assets/images/github-icon.svg" alt="github icon" />
            <span class="github-text">
              {{ getSourceMessage }}
            </span>
          </a>
        </div>

        <div class="section-2">
          <p>{{ demoInfoMessage }}</p>
        </div>

        <div class="section-3">
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/buttons/"
                  >Buttons</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/buttons/button"
                    >Button</a
                  >
                </li>
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/buttons/buttongroup"
                    >ButtonGroup</a
                  >
                </li>
              </ul>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/data-query/"
                  >Data Query</a
                >
              </h3>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/charts/"
                  >Charts</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/charts/bar/"
                    >Bar Chart</a
                  >
                </li>
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/charts/line/"
                    >Line Chart</a
                  >
                </li>
              </ul>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/labels/"
                  >Labels</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/labels/label/"
                    >Label</a
                  >
                </li>
              </ul>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/dateinputs/"
                  >Date Inputs</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/dateinputs/datepicker/"
                    >DatePicker</a
                  >
                </li>
              </ul>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/dropdowns/"
                  >Dropdowns</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/dropdowns/autocomplete"
                    >AutoComplete</a
                  >
                </li>
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/dropdowns/dropdownlist"
                    >DropDownList</a
                  >
                </li>
              </ul>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/form/"
                  >Form</a
                >
              </h3>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/grid/"
                  >Grid</a
                >
              </h3>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/inputs/"
                  >Inputs</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/inputs/checkbox"
                    >Checkbox</a
                  >
                </li>
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/inputs/radiobutton/"
                    >RadioButton</a
                  >
                </li>
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/inputs/maskedtextbox"
                    >MaskedTextBox</a
                  >
                </li>
              </ul>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/layout/"
                  >Layout</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/layout/avatar"
                    >Avatar</a
                  >
                </li>
              </ul>
            </div>
          </div>
          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/upload/"
                  >Upload</a
                >
              </h3>
            </div>
          </div>

          <div>
            <div class="package-item">
              <h3 class="package-title">
                <a
                  target="_blank"
                  rel="noopener noreferrer"
                  href="https://www.telerik.com/kendo-vue-ui/components/styling/"
                  >Styling</a
                >
              </h3>
              <ul class="package-items">
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/styling/theme-default/"
                    >Default Theme</a
                  >
                </li>
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/styling/theme-bootstrap/"
                    >Bootstrap Theme</a
                  >
                </li>
                <li class="component-link">
                  <a
                    target="_blank"
                    rel="noopener noreferrer"
                    href="https://www.telerik.com/kendo-vue-ui/components/styling/theme-material/"
                    >Material Theme</a
                  >
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, inject } from 'vue';
import { provideLocalizationService } from '@progress/kendo-vue-intl';

// Injecting the localization service
const kendoLocalizationService = inject('kendoLocalizationService', null);

// Computed properties for localization messages
const getSourceMessage = computed(() => {
  return provideLocalizationService(kendoLocalizationService).toLanguageString('getSource', 'Get Source');
});

const demoInfoMessage = computed(() => {
  return provideLocalizationService(kendoLocalizationService).toLanguageString(
    'demoInfo',
    'This demo application is built using the following Kendo UI for Vue components.'
  );
});
</script>

<style>
/* Add your styles here if needed */
</style>
