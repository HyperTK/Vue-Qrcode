<template>
  <v-container class="home">
    <ScanDialog />
  </v-container>
</template>

<script>
// @ is an alias to /src
import ScanDialog from "@/components/Fragments/ScanDialog.vue";
export default {
  name: "Home",
  components: {
    ScanDialog,
  }
};
</script>
