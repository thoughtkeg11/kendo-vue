<template>
  <div id="app">
    <h1>Hello Kendo UI for Vue!</h1>
    <p>
      <dropdownlist
        :data-items="categories"
        :data-item-key="'CategoryID'"
        :text-field="'CategoryName'"
        :default-item="defaultItems"
        @change="handleDropDownChange"
      ></dropdownlist>
      &nbsp; Selected category ID:
      <strong>{{ dropdownlistCategory }}</strong>
    </p>

    <grid
      :data-items="dataResult.data"
      :total="dataResult.total"
      :pageable="pageable"
      :sortable="sortable"
      :sort="sort"
      :take="take"
      :skip="skip"
      :columns="columns"
      @datastatechange="dataStateChange"
      @rowclick="rowClick"
      :style="{ height: '400px' }"
    >
      <template #discontinuedTemplate="{ props }">
        <td>
          <input type="checkbox" :checked="props.dataItem.Discontinued" disabled />
        </td>
      </template>
    </grid>

    <window v-if="windowVisible" :title="'Product Details'" @close="closeWindow" :height="250">
      <dl :style="{ 'text-align': 'left' }">
        <dt>Product Name</dt>
        <dd>{{ gridClickedRow.ProductName }}</dd>
        <dt>Product ID</dt>
        <dd>{{ gridClickedRow.ProductID }}</dd>
        <dt>Quantity per Unit</dt>
        <dd>{{ gridClickedRow.QuantityPerUnit }}</dd>
      </dl>
    </window>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { productsData } from './appdata/products';
import { categoriesData } from './appdata/categories';
import { process, DataResult, State, CompositeFilterDescriptor, SortDescriptor } from '@progress/kendo-data-query';
import { Grid, GridDataStateChangeEvent, GridRowClickEvent, GridColumnProps } from '@progress/kendo-vue-grid';
import { DropDownList as dropdownlist, DropDownListChangeEvent } from '@progress/kendo-vue-dropdowns';
import { Window } from '@progress/kendo-vue-dialogs';

// Data and state references
const categories = categoriesData;
const products = productsData;
const defaultItems = { CategoryID: null, CategoryName: "Product categories" };
const dropdownlistCategory = ref<number | null>(null);
const pageable = ref(true);
const sortable = ref(true);
const skip = ref<number>(0);
const take = ref<number>(10);
const sort = ref<SortDescriptor[]>([
  { field: "ProductName", dir: "asc" }
]);

const filter = ref<CompositeFilterDescriptor>({logic: "and", filters: []});
const columns: GridColumnProps[] = [
  { field: 'ProductName', title: 'Product Name' },
  { field: 'UnitPrice', title: 'Price' },
  { field: 'UnitsInStock', title: 'Units in Stock' },
  { field: 'Discontinued', cell: 'discontinuedTemplate' }
];

const dataResult = ref<DataResult>({ data: [], total: 0 });
const gridClickedRow = ref<{ ProductName: string, ProductID: number, QuantityPerUnit: string }>({ ProductName: '', ProductID: 0, QuantityPerUnit: '' });
const windowVisible = ref(false);

// Lifecycle hook
onMounted(() => {
  const dataState: State = {
    skip: skip.value,
    take: take.value,
    sort: sort.value,
    filter: filter.value // Ensure initial filtering is applied
  };
  dataResult.value = process(products, dataState);
});

// Methods
const handleDropDownChange = (e: DropDownListChangeEvent) => {
  dropdownlistCategory.value = e.target.value.CategoryID;
  if (e.target.value.CategoryID !== null) {
    filter.value = {
      logic: 'and',
      filters: [{ field: 'CategoryID', operator: 'eq', value: e.target.value.CategoryID }]
    };
    skip.value = 0;
  } else {
    filter.value = { logic: "and", filters: [] }; // Clear the filter correctly
    skip.value = 0;
  }

  const event: GridDataStateChangeEvent = {
    data: {
      skip: skip.value,
      take: take.value,
      sort: sort.value,
      filter: filter.value
    }
  };
  dataStateChange(event);
};

const createAppState = (dataState: State) => {
  take.value = dataState.take || take.value;
  skip.value = dataState.skip || skip.value;
  sort.value = dataState.sort || sort.value;
};

const dataStateChange = (event: GridDataStateChangeEvent) => {
  createAppState(event.data);
  dataResult.value = process(products, {
    skip: skip.value,
    take: take.value,
    sort: sort.value,
    filter: event.data.filter || filter.value,
  });
};

const rowClick = (event: GridRowClickEvent) => {
  gridClickedRow.value = event.dataItem;
  windowVisible.value = true;
};

const closeWindow = () => {
  windowVisible.value = false;
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}

dt {
  font-weight: bold;
}
</style>
