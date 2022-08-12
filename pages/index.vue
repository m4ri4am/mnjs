<template>
  <div>
    <companyInfo :welcomingString="welcomingString" fluid> </companyInfo>
    <v-tabs>
      <v-tab>عام</v-tab>
      <v-tab>الفروع</v-tab>
      <v-tab>المخزون</v-tab>
    </v-tabs>
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <v-row>
            <v-col align="end" justify="end">
              <v-btn-toggle
                v-model="toggle_exclusive"
                multiple
                class="mx-2 my-2"
              >
                <v-btn> اليوم </v-btn>
                <v-btn> الشهر </v-btn>
                <v-btn> السنة </v-btn>
              </v-btn-toggle>
            </v-col>
          </v-row>
          <v-row>
            <v-col
              cols="4"
              v-for="(index, item) in graphHeaders.length"
              :key="item"
            >
              <v-card class="mx-auto" max-width="300">
                <v-card-title color="white">
                  <v-row color="white" align="center" justify="center">
                    <div>
                      <strong v-if="avg">{{ graphHeaders[index] }}</strong>
                    </div>
                  </v-row>
                </v-card-title>

                <v-sheet color="white">
                  <v-sparkline
                    :key="String(avg)"
                    :smooth="16"
                    color="blue"
                    :line-width="2"
                    :value="value"
                    auto-draw
                    stroke-linecap="round"
                  >
                    <template v-slot:label="item"> {{ item.value }} </template>
                  </v-sparkline>
                </v-sheet>
              </v-card>
            </v-col>
          </v-row>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const exhale = (ms) => new Promise((resolve) => setTimeout(resolve, ms));
export default {
  name: "IndexPage",
  data() {
    return {
      graphHeaders: [
        "مبيعات",
        "مشتريات",
        "إيرادات",
        "مصروفات",
        "إيرادات الشركة",
        "مصروفات الشركة",
        "مبلغ الخصم",
        "خدمات التوصيل",
        "خدمات التوصيل",
        "خدمات التوصيل"
      ],
      checking: false,
      value: [25, 100, 40, 40, 60, 60, 60, 90, 120],
      toggle_exclusive: [],
      welcomingString: "مرحبا بكم في منصة منجز",
    };
  },
  computed: {
    avg() {
      const sum = this.heartbeats.reduce((acc, cur) => acc + cur, 0);
      const length = this.heartbeats.length;

      if (!sum && !length) return 0;

      return Math.ceil(sum / length);
    },
  },
  created() {
    this.takePulse(false);
  },
  methods: {
    heartbeat() {
      return Math.ceil(Math.random() * (120 - 80) + 80);
    },
    async takePulse(inhale = true) {
      this.checking = true;

      inhale && (await exhale(1000));

      this.heartbeats = Array.from({ length: 20 }, this.heartbeat);

      this.checking = false;
    },
  },
};
</script>
<style>
.container {
  padding: 0 !important;
}
.v-tab--active {
  color: black !important;
  font-weight: 600;
}
</style>
