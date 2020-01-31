<template>
  <v-dialog persistent v-model="show" max-width="40rem">
    <v-card>
      <div class="d-flex flex-no-wrap">
        <v-avatar class="ma-3" size="300" tile>
          <v-img :src="member.avatar_url"></v-img>
        </v-avatar>
        <div>
          <v-card-title class="headline" v-text="member.login"></v-card-title>
          <v-card-subtitle v-text="member.id"></v-card-subtitle>
        </div>
        <v-btn @click="close">Close</v-btn>
      </div>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import Vue from "vue";
import { Member } from "../../model/member";

export default Vue.extend({
  name: "MemberDetail",
  props: {
    show: {
      type: Boolean,
      required: true,
      default: false
    },
    member: {
      type: Object as () => Member,
      required: true,
      default: []
    }
  },
  data: () => ({}),
  methods: {
    close: function() {
      this.$emit("close");
    }
  }
});
</script>

<style module>
.table {
  border-collapse: collapse;
  width: 100%;
}

.table tbody tr:nth-of-type(odd) {
  background-color: rgba(0, 0, 0, 0.05);
}
</style>
