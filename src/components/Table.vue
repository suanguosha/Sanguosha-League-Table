<template>
  <v-container>
    <v-card tile width="100%" class="green lighten-1 text-center mb-6">
      <v-card-text class="white--text"
        ><strong>三国杀国战裁判计分器</strong>
      </v-card-text>
    </v-card>
    <v-data-table :headers="headers" :items="players" hide-default-footer>
      <template v-slot:item.name="props">
        <v-text-field
          v-model="props.item.name"
          label="请输入选手ID"
          single-line
        ></v-text-field>
      </template>
      <template v-slot:item.country="props">
        <v-select
          v-model="props.item.country"
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
      <template v-slot:item.aoZhan="props">
        <v-simple-checkbox v-model="props.item.aoZhan"></v-simple-checkbox>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  props: {
    addTable: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      countries: ["魏国", "蜀国", "吴国", "群雄", "野心家"],
      headers: [
        {
          text: "选手",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "国家", value: "country" },
        { text: "鏖战", value: "aoZhan" },
      ],
      players: [
        {
          name: "",
          country: "",
          aoZhan: false,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
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
  watch: {
    addTable(value) {
      if (value) {
        // do some resetting
        this.players.map((item) => { 
          item.country = "";
          item.aoZhan = false;
          return item; 
        });
        this.$emit('done')
      }
    }
  }
};
</script>
