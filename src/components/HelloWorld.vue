<template>
  <v-container>
    <v-data-table
      v-model="selected"
      :headers="headers"
      :items="filteredDesserts"
      show-select
      item-key="name"
    >
      <template v-slot:header>
        <tr class="grey lighten-3">
          <th>
            <v-icon>mdi-filter-variant</v-icon>
          </th>
          <th v-for="header in headers" :key="header.text">
            <div v-if="filters.hasOwnProperty(header.value)">
              <v-autocomplete
                v-model="filters[header.value]"
                :items="columnValueList(header.value)"
                attach
                chips
                clearable
                dense
                flat
                hide-details
                multiple
              >
                <template v-slot:selection="{ item, index }">
                  <v-chip v-if="index < 5">
                    <span>
                      {{ item }}
                    </span>
                  </v-chip>
                  <span v-if="index === 5" class="grey--text caption">
                    (+{{ filters[header.value].length - 5 }} others)
                  </span>
                </template>
              </v-autocomplete>
            </div>
          </th>
        </tr>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    selected: [],
    headers: [
      {
        text: "Dessert (100g serving)",
        align: "left",
        value: "name",
      },

      { text: "Calories", value: "calories" },
      { text: "Fat (g)", value: "fat" },
      { text: "Carbs (g)", value: "carbs" },
      { text: "Protein (g)", value: "protein" },
      { text: "Iron (%)", value: "iron" },
    ],

    filters: {
      name: [],
      calories: [],
      fat: [],
      carbs: [],
      protein: [],
      iron: [],
    },

    desserts: [
      {
        value: false,
        name: "Frozen Yogurt",
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        iron: "1%",
      },
      {
        value: false,
        name: "Ice cream sandwich",
        calories: 237,
        fat: 9.0,
        carbs: 37,
        protein: 4.3,
        iron: "1%",
      },
      {
        value: false,
        name: "Eclair",
        calories: 262,
        fat: 16.0,
        carbs: 23,
        protein: 6.0,
        iron: "7%",
      },
      {
        value: false,
        name: "Cupcake",
        calories: 305,
        fat: 3.7,
        carbs: 67,
        protein: 4.3,
        iron: "8%",
      },
      {
        value: false,
        name: "Gingerbread",
        calories: 356,
        fat: 16.0,
        carbs: 49,
        protein: 3.9,
        iron: "16%",
      },

      {
        value: false,
        name: "Jelly bean",
        calories: 375,
        fat: 0.0,
        carbs: 94,
        protein: 0.0,
        iron: "0%",
      },
      {
        value: false,
        name: "Lollipop",
        calories: 392,
        fat: 0.2,
        carbs: 98,
        protein: 0,
        iron: "2%",
      },
      {
        value: false,
        name: "Honeycomb",
        calories: 408,
        fat: 3.2,
        carbs: 87,
        protein: 6.5,
        iron: "45%",
      },
      {
        value: false,
        name: "Donut",
        calories: 452,
        fat: 25.0,
        carbs: 51,
        protein: 4.9,
        iron: "22%",
      },
      {
        value: false,
        name: "KitKat",
        calories: 518,
        fat: 26.0,
        carbs: 65,
        protein: 7,
        iron: "6%",
      },
    ],
  }),

  computed: {
    filteredDesserts() {
      return this.desserts.filter((d) => {
        return Object.keys(this.filters).every((f) => {
          return this.filters[f].length < 1 || this.filters[f].includes(d[f]);
        });
      });
    },
  },

  methods: {
    columnValueList(val) {
      return this.desserts.map((d) => d[val]);
    },
  },
};
</script>
