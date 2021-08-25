<template>
  <v-row justify="center">
    <v-dialog
      v-model="dialog"
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
    >
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="closeDialog()">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>记分规则设置</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-toolbar-items>
            <v-btn dark text @click="closeDialog()">
              保存
            </v-btn>
          </v-toolbar-items>
        </v-toolbar>
        <v-list three-line subheader>
          <v-subheader>记分规则</v-subheader>
          <v-list-item>
            <v-list-item-action>
              <v-checkbox v-model="numOfWinners"></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>获胜方玩家数量</v-list-item-title>
              <v-list-item-subtitle>选择获胜方玩家数量</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-action>
              <v-checkbox v-model="numOfWinners"></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>获胜方玩家数量</v-list-item-title>
              <v-list-item-subtitle>选择获胜方玩家数量</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          <v-list-item>
            <v-list-item-action>
              <v-checkbox v-model="numOfWinners"></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>获胜方玩家数量</v-list-item-title>
              <v-list-item-subtitle>选择获胜方玩家数量</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  props: {
    dialog: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      notifications: false,
      sound: true,
      widgets: false,
      numOfWinners: 0,
    };
  },
  methods: {
    closeDialog() {
      this.$emit("close");
    },
  },
};
</script>
