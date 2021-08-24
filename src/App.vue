<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="三国杀国战计分器"
          class="shrink"
          contain
          min-width="80"
          src="https://www.sanguosha.com/static/pc/dist/img/logo.png?v=20200417"
          width="80"
        />
      </div>
      <v-spacer></v-spacer>
      <v-btn class="mx-2" dark color="yellow darken-1">
        <v-icon left dark>
          mdi-pencil
        </v-icon>
        计分规则
      </v-btn>
      <v-btn class="mx-2" dark color="green darken-1">
        <v-icon left dark>
          mdi-plus
        </v-icon>
        加桌
      </v-btn>
    </v-app-bar>

    <v-main>
      <Table />
    </v-main>
  </v-app>
</template>

<script>
import Table from "./components/Table";

export default {
  name: "App",

  components: {
    Table,
  },

  data: () => ({
    //
  }),
};
</script>
