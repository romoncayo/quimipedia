<template>
  <v-container fluid class="pa-0 ma-0">
    <v-row style="padding-left: 1%; padding-right: 1%">
      <v-col
        align-self="auto"
        md="2"
        v-for="category in groups"
        :key="category"
      >
        <v-flex>
          <v-btn
            elevation="2"
            small
            style="color: #8b008b"
            @click="changeSelected(category)"
            color="cyan"
          >
            {{ category }}
          </v-btn>
        </v-flex>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  props: ["groups"],
  data() {
    return {};
  },
  methods: {
    changeSelected(category) {
      if (this.selectedCategory != category) {
        if (category == "Metales") {
          this.selectedCategory = category;
          this.selectedColor = "amber";
          this.unselectedColor = "grey";
        } else if (category == "En Ecuador") {
          this.selectedCategory = category;
          this.selectedColor = "lime";
          this.unselectedColor = "grey";
        } else if (category == "Liquidos") {
          this.selectedCategory = category;
          this.selectedColor = "amber";
          this.unselectedColor = "grey";
        } else if (category == "Indeterminado") {
          this.selectedCategory = category;
          this.selectedColor = "amber";
          this.unselectedColor = "grey";
        } else if (category == "Alcalinos") {
          this.selectedCategory = category;
          this.selectedColor = "blue";
          this.unselectedColor = "grey";
        } else if (category == "Alcalinotérreos") {
          this.selectedCategory = category;
          this.selectedColor = "amber";
          this.unselectedColor = "grey";
        } else if (category == "Metales Transitorios") {
          this.selectedCategory = category;
          this.selectedColor = "pink";
          this.unselectedColor = "grey";
        } else if (category == "Otros metales") {
          this.selectedCategory = category;
          this.selectedColor = "teal";
          this.unselectedColor = "grey";
        } else if (category == "Metaloides") {
          this.selectedCategory = category;
          this.selectedColor = "red";
          this.unselectedColor = "grey";
        } else if (category == "Otros no metales") {
          this.selectedCategory = category;
          this.selectedColor = "green";
          this.unselectedColor = "grey";
        } else if (category == "Halógenos") {
          this.selectedCategory = category;
          this.selectedColor = "indigo";
          this.unselectedColor = "grey";
        } else if (category == "Gases Nobles") {
          this.selectedCategory = category;
          this.selectedColor = "purple";
          this.unselectedColor = "grey";
        }
      } else {
        this.selectedCategory = null;
        this.selectedColor = "#19d29d";
        this.unselectedColor = "#19d29d";
      }
      this.$emit("change", this.selectedCategory);
    },
  },
};
</script>