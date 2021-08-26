<!-- -->
<template></template>

<script>
export default {
  name: "TableauUserAuthentication",
  components: {},

  data() {
    return {
      viz: {},
      workBook: {},
      workSheet: {},
      workSheets: {},
      uid: String,
      container: document.getElementById("auth"),
      url: "TABLEAUSERVER",

      options: {
        hideTabs: true,
        hideToolbar: true,
        height: "100vh",
        width: "100vw",
        onFirstInteractive: () => {
          this.workBook = this.viz.getWorkbook();

          this.workSheet = this.workBook
            .getActiveSheet()
            .getWorksheets()
            .get("WS_LOADER");

          this.workSheet.getSummaryDataAsync().then((result) => {
            this.uid = result.getData()[0][0]["formattedValue"];
            this.$parent.uid = this.uid;
            this.$parent.activeComponent = "Content";
            this.viz.dispose();
          });
        },
      },
    };
  },

  methods: {
    initViz: function () {
      this.viz = new tableau.Viz(this.container, this.url, this.options);
    },
  },

  beforeCreate: function () {
    let container = document.createElement("div");
    container.id = "authentication";
    document.getElementsByTagName("body")[0].appendChild(container);
  },

  created: function () {
    this.initViz();
  },

  unmounted: function () {
    this.viz.dispose();
    let container = document.getElementById("authentication");
    container.remove();
  },
};
</script>

<style scoped>
</style>