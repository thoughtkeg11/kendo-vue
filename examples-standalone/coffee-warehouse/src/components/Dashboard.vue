<template>
  <div>
    <div class="card-header-wrapper">
      <h3 class="card-title">{{ teamEfficiencyMessage }}</h3>
      <buttongroup>
        <k-button
          :togglable="true"
          @click="buttonGroupClick($event, 0)"
          :selected="selectedIndex === 0"
        >
          {{ trendMessage }}
        </k-button>
        <k-button
          :togglable="true"
          @click="buttonGroupClick($event, 1)"
          :selected="selectedIndex === 1"
        >
          {{ volumeMessage }}
        </k-button>
      </buttongroup>
      <div class="card-ranges">
        <datepicker
          style="width: 130px"
          :value="dateRange.start"
          @change="onFromDateChange"
        >
        </datepicker>
        <span> - </span>
        <datepicker
          style="width: 130px"
          :value="dateRange.end"
          @change="onToDateChange"
        >
        </datepicker>
      </div>
    </div>
    <div v-if="selectedIndex === 0">
      <Chart>
        <ChartTooltip :render="myToolTipTemplate">
          <template #myToolTipTemplate="{ props = { point: {} } }">
            <div>
              {{
                provideIntlService(kendoIntlService)
                  .formatDate(props.point.category, "MMMM yyyy")
                  .toUpperCase()
              }}
              <br />
              <div class="chart-tooltip">
                {{
                  provideIntlService(kendoIntlService).formatNumber(props.point.value, "n3")
                }}
              </div>
            </div>
          </template>
        </ChartTooltip>
        <ChartLegend
          :position="'bottom'"
          :orientation="'horizontal'"
          :background="'#f4f5f8'"
          :spacing="140"
          :padding="{ left: 80, right: 80 }"
        >
        </ChartLegend>
        <ChartCategoryAxis>
          <ChartCategoryAxisItem
            :labels="{ format: 'MMMM yyyy', rotation: 'auto' }"
            :base-unit="'months'"
            :min="dateRange.start"
            :max="dateRange.end"
            :categories="categories"
          />
        </ChartCategoryAxis>
        <ChartSeries>
          <ChartSeriesItem
            v-for="(item, index) in series"
            :key="index"
            :type="'line'"
            :data-items="item.data"
            :name="item.name"
          />
        </ChartSeries>
      </Chart>
    </div>
    <div v-else>
      <Chart>
        <ChartTooltip :render="myToolTipLineTemplate">
          <template #myToolTipLineTemplate="{ props = { point: {} } }">
            <div>
              {{
                provideIntlService(kendoIntlService)
                  .formatDate(props.point.category, "MMMM yyyy")
                  .toUpperCase()
              }}
              <br />
              <div class="chart-tooltip">
                {{
                  provideIntlService(kendoIntlService).formatNumber(props.point.value, "n3")
                }}
              </div>
            </div>
          </template>
        </ChartTooltip>
        <ChartLegend
          :position="'bottom'"
          :orientation="'horizontal'"
          :background="'#f4f5f8'"
          :spacing="140"
          :padding="{ left: 80, right: 80 }"
        >
        </ChartLegend>
        <ChartCategoryAxis>
          <ChartCategoryAxisItem
            :labels="{ format: 'MMMM yyyy', rotation: 'auto' }"
            :base-unit="'months'"
            :min="dateRange.start"
            :max="dateRange.end"
            :categories="categories"
          />
        </ChartCategoryAxis>
        <ChartSeries>
          <ChartSeriesItem
            v-for="(item, index) in series"
            :key="index"
            :type="'column'"
            :data-items="item.data"
            :color="item.color"
            :name="item.name"
          />
        </ChartSeries>
      </Chart>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, inject, onMounted } from 'vue';
import {
  Chart,
  ChartSeries,
  ChartSeriesItem,
  ChartCategoryAxis,
  ChartCategoryAxisItem,
  ChartLegend,
  ChartTooltip,
} from '@progress/kendo-vue-charts';
import { Button as kButton, ButtonGroup as buttongroup } from '@progress/kendo-vue-buttons';
import { DatePicker as datepicker } from '@progress/kendo-vue-dateinputs';
import { provideIntlService, provideLocalizationService } from '@progress/kendo-vue-intl';
import { orders } from '../assets/orders.js';
import 'hammerjs';

// Remove props if unused
// const props = defineProps({
//   localizationLanguage: String,
// });

// Injected services
const kendoIntlService = inject('kendoIntlService', null);
const kendoLocalizationService = inject('kendoLocalizationService', null);

// Reactive state
const selectedIndex = ref(0);
const dateRange = ref({
  start: new Date(2020, 0, 1),
  end: new Date(2020, 4, 1),
});
const categories = ref([]);
const series = ref([]);

// Computed properties
const teamEfficiencyMessage = computed(() => {
  return provideLocalizationService(kendoLocalizationService).toLanguageString(
    'teamEfficiency',
    'Team Efficiency'
  );
});

const trendMessage = computed(() => {
  return provideLocalizationService(kendoLocalizationService).toLanguageString('trend', 'Trend');
});

const volumeMessage = computed(() => {
  return provideLocalizationService(kendoLocalizationService).toLanguageString('volume', 'Volume');
});

// Methods
const fetchData = (team) => {
  return orders.map((dataItem) => {
    if (
      dataItem.teamID === team &&
      dataItem.orderDate >= dateRange.value.start &&
      dataItem.orderDate < dateRange.value.end
    ) {
      return dataItem.orderTotal;
    }
    return null;
  }).filter(item => item !== null);
};

const buttonGroupClick = (e, newIndex) => {
  selectedIndex.value = newIndex;
};

const updateSeries = () => {
  series.value = series.value.map((series, index) => ({
    ...series,
    data: fetchData(index + 1),
  }));
};

const onFromDateChange = (date) => {
  dateRange.value.start = date.value;
  updateSeries();
};

const onToDateChange = (date) => {
  dateRange.value.end = date.value;
  updateSeries();
};

// Lifecycle hook
onMounted(() => {
  categories.value = orders.map((dataItem) => dataItem.orderDate);
  series.value = [
    {
      name: 'Tiger Team',
      data: fetchData(1),
      color: '#FF6358',
    },
    {
      name: 'Lemon Team',
      data: fetchData(2),
      color: '#F7C62F',
    },
    {
      name: 'Organic Team',
      data: fetchData(3),
      color: '#55AB1D',
    },
    {
      name: 'Ocean Team',
      data: fetchData(4),
      color: '#28B4C8',
    },
  ];
});

// Templates
const myToolTipTemplate = 'myToolTipTemplate';
const myToolTipLineTemplate = 'myToolTipLineTemplate';
</script>

<style scoped>
.chart-tooltip {
  text-align: center;
  font-size: 15px;
  font-weight: bold;
}

.card-header-wrapper {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.card-title {
  grid-column: 1 / 2;
  grid-row: 1;
  margin-block-start: 1em;
  margin-block-end: 1em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
}

.k-button-group {
  display: block;
  margin-block-start: 1em;
  margin-block-end: 1em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
}

.card-ranges {
  margin-top: 1rem;
  text-align: left;
}
</style>
