<template>
  <v-menu ref="menu" :close-on-content-click="false" v-model="menuState" lazy full-width :return-value.sync="dateData"
          max-width="290px" min-width="290px">

    <v-text-field slot="activator" v-model="dateData" required :rules="rules"
                  :label="label" readonly
                  :prepend-icon="withIcon?'calendar_today':undefined"/>

    <v-date-picker v-model="dateData" @change="$refs.menu.save(dateData)"
                   format="24hr"></v-date-picker>
  </v-menu>
</template>
<script>
  export default {
    name: 'DateMenuPicker',
    props: {
      label: "",
      rules: {},
      date: {},
      withIcon: {type: Boolean, default: true}
    },
    data: function () {
      return {
        dateData: this.date,
        menuState: false,
      }
    },
    watch: {
      date: function (v, o) {
        if (v !== o) {
          this.dateData = v;
        }
      },
      dateData: function (v, o) {
        if (v !== o) {
          this.$emit("change", v);
        }
      }
    }
  }
</script>
