<template>
  <v-card color="white" elevation="0">
    <v-card-title class="text-h5">{{ welcomingString }}</v-card-title>
    <v-card-subtitle></v-card-subtitle>
    <v-card-text>
      <v-row> </v-row>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  name: "CompanyInfo",
  props: ["welcomingString"],
  data() {
    return {};
  },
  methods: {
    //
  },
};
</script>
<style scoped>
.v-card {
  color: rgb(1, 1, 29);
}
</style>