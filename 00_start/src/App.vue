<template>
  <v-app>
    <member-page/>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import { MemberPage } from "./pages/members";

export default Vue.extend({
  name: "App",
  components: { MemberPage }
});
</script>
