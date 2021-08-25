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
        >
          <template #selection="{ item }">
            <v-chip :color="countryColor(item.value)" text-color="white">
              <v-avatar left :color="countryColor(item.value)" class="darken-4">
                {{ playersInCountry(item.value) }} </v-avatar
              >{{ item.text }}</v-chip
            >
          </template>
        </v-select>
      </template>
      <template v-slot:item.aoZhan="props">
        <v-simple-checkbox v-model="props.item.aoZhan"></v-simple-checkbox>
      </template>
      <template v-slot:item.totalPts="{ item }">
        <v-chip :color="scoreColor(item.totalPts)" dark>
          {{ item.totalPts }}
        </v-chip>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  props: {
    addTable: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      // player info, dynamically updated
      players: [
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
        {
          name: "",
          country: "",
          aoZhan: false,
          totalPts: 0,
        },
      ],
      // titles for data table
      headers: [
        {
          text: "选手",
          align: "start",
          value: "name",
          width: "30%",
        },
        { text: "国家", value: "country", width: "30%" },
        { text: "鏖战", value: "aoZhan", width: "30%" },
        { text: "总分", value: "totalPts", width: "10%" },
      ],
      // countries for v-select 魏国4 蜀国3 吴国2 群雄1 野心家0
      countries: [
        {
          text: "魏国",
          value: 4,
        },
        {
          text: "蜀国",
          value: 3,
        },
        {
          text: "吴国",
          value: 2,
        },
        {
          text: "群雄",
          value: 1,
        },
        {
          text: "野心家",
          value: 0,
        },
      ],
    };
  },
  methods: {
    countryColor(country) {
      switch (country) {
        case 4:
          return "blue";
        case 3:
          return "red";
        case 2:
          return "green";
        case 1:
          return "grey";
        default:
          return "purple";
      }
    },
    scoreColor(score) {
      if (score > 10) return "red";
      else if (score > 5) return "orange";
      else return "green";
    },
    playersInCountry(country) {
      return this.players.reduce(
        (acc, cur) => acc + (cur.country === country),
        0
      );
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
        this.$emit("done");
      }
    },
  },
};
</script>
