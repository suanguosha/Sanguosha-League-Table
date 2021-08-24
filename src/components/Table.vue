<template>
  <v-container>
    <v-card tile width="100%" class="green lighten-1 text-center mb-6">
      <v-card-text class="white--text"
        ><strong>三国杀国战裁判计分器</strong>
      </v-card-text>
    </v-card>
    <v-data-table :headers="headers" :items="desserts" hide-default-footer>
      <template v-slot:item.name="props">
        <v-text-field
          v-model="props.item.name"
          label="请输入选手ID"
          single-line
        ></v-text-field>
      </template>
      <template v-slot:item.iron="props">
        <v-select
          v-model="props.item.iron"
          :items="countries"
          label="请选择国家"
          align="center"
          justify="center"
        >
          <template #selection="{ item }">
            <v-chip :color="countryColor(item)" text-color="white">{{
              item
            }}</v-chip>
          </template>
        </v-select>
      </template>
      <template v-slot:item.optionA="props">
        <v-simple-checkbox v-model="props.item.optionA"></v-simple-checkbox>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      countries: ["魏国", "蜀国", "吴国", "群雄", "野心家"],
      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Calories", value: "calories" },
        { text: "Iron (%)", value: "iron" },
        { text: "optionA", value: "optionA" },
      ],
      desserts: [
        {
          name: "",
          calories: 159,
          iron: "1%",
          optionA: false,
        },
        {
          name: "",
          calories: 159,
          iron: "1%",
          optionA: false,
        },
        {
          name: "",
          calories: 159,
          iron: "1%",
          optionA: false,
        },
        {
          name: "",
          calories: 159,
          iron: "1%",
          optionA: false,
        },
        {
          name: "",
          calories: 159,
          iron: "1%",
          optionA: false,
        },
        {
          name: "",
          calories: 159,
          iron: "1%",
          optionA: false,
        },
        {
          name: "",
          calories: 159,
          iron: "1%",
          optionA: false,
        },
      ],
    };
  },
  methods: {
    countryColor(country) {
      switch (country) {
        case "魏国":
          return "blue";
        case "蜀国":
          return "red";
        case "吴国":
          return "green";
        case "群雄":
          return "grey";
        default:
          return "purple";
      }
    },
  },
};
</script>
