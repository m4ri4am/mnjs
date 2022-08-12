<template>
  <div>
    <companyInfo :welcomingString="welcomingString"></companyInfo>
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <template>
            <div class="text-left">
              <v-dialog v-model="dialog" width="500" persistent>
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    color="primary darken-2"
                    dark
                    v-bind="attrs"
                    v-on="on"
                    class="mx-3 my-3"
                  >
                    افتح نافذة التقرير
                  </v-btn>
                </template>
                <v-card color="rgb(224 224 224)">
                  <v-card-title class="text-h5 white lighten-2">
                    اعلانات الجهاز
                  </v-card-title>
                  <v-card-text>
                    <v-col cols="12">
                      <p color="text #F44336">ادخل العنوان</p>
                      <v-text-field solo label="" clearable></v-text-field>
                      <p>ادخل العنوان</p>
                      <v-file-input
                        @change="previewMultiImage"
                        chips
                        multiple
                        solo
                        label=""
                        clearable
                        v-model="image"
                        type="file"
                        accept="image/*"
                        class="form-control-file"
                        id="my-file"
                      ></v-file-input>
                      <div class="d-flex">
                        <template v-if="preview_list.length">
                          <v-row>
                            <v-col cols="12" class="d-flex">
                              <div
                                v-for="(item, index) in preview_list"
                                :key="index"
                              >
                                <v-img
                                  clearable
                                  class="mx-2 image-preview"
                                  height="80"
                                  width="80"
                                  :src="item"
                                />
                              </div>
                            </v-col>
                          </v-row>
                        </template>
                      </div>

                      <p>ادخل العنوان</p>
                      <v-text-field solo label="" clearable></v-text-field>
                      <p>ادخل العنوان</p>
                      <v-text-field solo label="" clearable></v-text-field>
                      <v-sheet color="rgb(224 224 224)">
                        <v-switch
                          inset
                          label="ايقاف التحكم اليدوي للجهاز"
                        ></v-switch>
                        <v-switch
                          inset
                          label="ايقاف التحكم اليدوي للجهاز"
                        ></v-switch>
                        <v-switch
                          inset
                          label="ايقاف التحكم اليدوي للجهاز"
                        ></v-switch>
                        <v-switch
                          inset
                          label="ايقاف التحكم اليدوي للجهاز"
                        ></v-switch>
                      </v-sheet>
                    </v-col>
                  </v-card-text>
                  <v-divider></v-divider>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="primary darken-2" text @click="handleClosing">
                      close
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </div>
            <v-data-table
              disable-pagination
              :headers="headers"
              :items="desserts"
              class="elevation-1 mx-3 my-3"
              hide-default-footer
              :hide-default-header="selected.length > 0 ? true : false"
              show-select
              v-model="selected"
              item-key="name"
            >
              <template v-if="selected.length > 0" v-slot:top>
                <v-row>
                  <v-col cols="3" class="d-flex">
                    <p class="mx-5 my-3">
                      محدد {{ "(" + selected.length + ")" }}
                    </p>
                  </v-col>
                  <v-col cols="4" md="2" class="d-flex">
                    <v-select :items="items" label="الاجراءات" solo></v-select>
                  </v-col>
                </v-row>
              </template>
            </v-data-table>
          </template>
          <div class="text-center">
            <v-pagination v-model="page" :length="length" circle>
            </v-pagination>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      preview_list: [],
      url: null,
      image: null,
      selected: [],
      dialog: false,
      items: ["تعديل", "حذف"],
      welcomingString: "الطلبات الجديدة",
      page: 1,
      length: 0,
      headers: [
        {
          text: "الاسم",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "عنوان", value: "calories" },
        { text: "رقم", value: "fat" },
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: "1%",
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: "1%",
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: "7%",
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: "8%",
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: "16%",
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: "0%",
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: "2%",
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: "45%",
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: "22%",
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: "6%",
        },
      ],
    };
  },
  watch: {},

  methods: {
    handleClosing() {
      this.dialog = false;
      this.image = [];
      this.preview_list = [];
    },
    print() {
      this.url = URL.createObjectURL(this.image);
      console.log(this.imageField);
    },
    previewMultiImage() {
      var count = this.image.length;
      var index = 0;
      if (this.image) {
        while (count--) {
          var reader = new FileReader();
          reader.onload = (e) => {
            this.preview_list.push(e.target.result);
          };
          reader.readAsDataURL(this.image[index]);
          index++;
        }
      }
    },
  },
};
</script>
<style scoped>
p {
  color: black;
}
.image-preview {
  width: 50px !important;
}
</style>