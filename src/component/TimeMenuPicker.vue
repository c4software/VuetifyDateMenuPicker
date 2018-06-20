<template>
  <v-menu ref="menu" :close-on-content-click="false" v-model="menuState" lazy full-width :return-value.sync="timeData"
          max-width="290px" min-width="290px">

    <v-text-field slot="activator" v-model="timeData" required :rules="rules"
                  :label="label"
                  :prepend-icon="withIcon?'access_time':undefined"
                  readonly/>

    <v-time-picker v-model="timeData" @change="$refs.menu.save(timeData)" format="24hr"/>

  </v-menu>
</template>
<script>
  export default {
    name: 'TimeMenuPicker',
    props: {
      label: "",
      rules: {},
      time: {},
      withIcon: {type: Boolean, default: false}
    },
    data: function () {
      return {
        timeData: this.time,
        menuState: false,
      }
    },
    watch: {
      time: function (v, o) {
        if (v !== o) {
          this.timeData = v;
        }
      },
      timeData: function (v, o) {
        if (v !== o) {
          this.$emit("change", v);
        }
      },
    },
  }
</script>
