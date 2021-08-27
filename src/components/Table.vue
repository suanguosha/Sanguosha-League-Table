/* eslint-disable vue/no-unused-vars */ /* eslint-disable vue/no-unused-vars */
/* eslint-disable vue/no-unused-vars */
<template>
  <v-container>
    <v-card tile width="100%" class="green lighten-1 text-center mb-6">
      <v-card-text class="white--text"
        ><strong>三国杀国战裁判计分器</strong>
      </v-card-text>
    </v-card>
    <v-data-table :headers="headers" :items="players" hide-default-footer>
      <!-- customize "item.name" slot in v-data-table, access "props" binded on this slot  -->
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
      <template v-slot:item.killedPlayers="props">
        <v-combobox
          :items="countries"
          label="击杀角色"
          multiple
          small-chips
          solo
          deletable-chips
          :value="props.item.killedPlayers"
          hide-details
        >
          <!-- dropdown v-list-item, stop propogation @click, enable multiple selection -->
          <template v-slot:item="{ index, item }">
            <v-list-item @click.stop="multipleSelection(item, props)">{{
              item.text
            }}</v-list-item>
          </template>
          <template v-slot:selection="{ index, item }">
            <v-chip
              close
              dark
              :color="countryColor(item.value)"
              @click:close="deleteChip(item, props)"
              >{{ item.text }}</v-chip
            >
          </template>
        </v-combobox>
      </template>
      <template v-slot:item.aoZhan="props">
        <v-simple-checkbox v-model="props.item.aoZhan"></v-simple-checkbox>
      </template>
      <template v-slot:item.zhuLian="props">
        <v-simple-checkbox v-model="props.item.zhuLian"></v-simple-checkbox>
      </template>
      <template v-slot:item.xianQu="props">
        <v-simple-checkbox v-model="props.item.xianQu"></v-simple-checkbox>
      </template>

      <template v-slot:item.currentPts="{ item }">
        <v-chip :color="scoreColor(item.currentPts)" dark>
          {{ item.currentPts }}
        </v-chip>
      </template>
      <template v-slot:item.totalPts="{ item }">
        <v-chip :color="scoreColor(item.currentPts + item.totalPts)" dark>
          {{ item.currentPts + item.totalPts }}
        </v-chip>
      </template>
    </v-data-table>
    <v-col width="100%" class="text-center mb-6">
      <span>本场胜利方：</span>

      <v-btn-toggle id="winnerPanel" v-model="winner" class="ml-4">
        <v-btn color="blue" large dark active-class="btnSelected">
          魏国
        </v-btn>
        <v-btn color="red" large dark active-class="btnSelected">
          蜀国
        </v-btn>
        <v-btn color="green" large dark active-class="btnSelected">
          吴国
        </v-btn>
        <v-btn color="grey" large dark active-class="btnSelected">
          群雄
        </v-btn>
        <v-btn color="purple" large dark active-class="btnSelected">
          野心家
        </v-btn>
      </v-btn-toggle>
    </v-col>
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
      winner: null,
      numOfTables: 0,
      arr: [],
      // player info, dynamically updated
      players: [
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
        {
          name: "",
          country: "",
          currentPts: 0,
          totalPts: 0,
          killedPlayers: [],
          aoZhan: false,
          zhuLian: false,
          xianQu: false,
        },
      ],
      // titles for data table
      headers: [
        {
          text: "选手",
          align: "start",
          value: "name",
          width: "20%",
        },
        { text: "国家", value: "country", width: "10%" },
        { text: "击杀角色", value: "killedPlayers", width: "20%" },
        { text: "鏖战", value: "aoZhan", width: "5%" },
        { text: "珠联", value: "zhuLian", width: "5%" },
        { text: "先驱", value: "xianQu", width: "5%" },
        { text: "当前分", value: "currentPts", width: "10%" },
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
    multipleSelection(item, props) {
      props.item.killedPlayers.push({ ...item });
    },
    deleteChip(item, props) {
      props.item.killedPlayers = props.item.killedPlayers.filter(
        (x) => x !== item
      );
    },
  },
  watch: {
    addTable(value) {
      if (value) {
        // do some resetting
        ++this.numOfTables;
        this.headers.splice(this.headers.length - 2, 0, {
          text: "第" + this.numOfTables + "桌",
          value: "round" + this.numOfTables,
          width: "10%",
        });
        this.players.map((item) => {
          item.country = "";
          item.aoZhan = false;
          item["round" + this.numOfTables] = item.currentPts;
          item.totalPts += item.currentPts;
          item.currentPts = 0;
          return item;
        });
        this.$emit("done");
      }
    },
  },
};
</script>
<style scoped>
#winnerPanel .btnSelected {
  font-size: 1.2rem !important;
  height: 5rem !important;
  color: #ffffff !important;
}
</style>
