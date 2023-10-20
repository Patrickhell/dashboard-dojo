<template>
  <div class="layout d-flex justify-content-center">
    <LeftSide first_name="mio nome" class="leftside" />
    <MainSide nav="nav bar" class="mainside" />
  </div>
</template>

<script>
// @ is an alias to /src
import LeftSide from "@/components/LeftSide.vue";
import MainSide from "@/components/MainSide.vue";

export default {
  name: "HomeView",
  components: {
    LeftSide,
    MainSide,
  },
};
</script>
<style scoped lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
div.layout {
  width: 1200px;
}
.leftside {
  width: 200px;
  background-color: #2b4154;
  color: white;
  height: auto;
}
.mainside {
  width: calc(100% - 200px);
  margin: 0 auto;
}
</style>
