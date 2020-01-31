<template>
  <v-card>
    <v-card-title>
      <v-text-field
        v-model="search"
        label="Search"
        append-icon="mdi-magnify"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="members"
      :items-per-page="5"
      :search="search"
      class="elevation-1"
    >
      <template v-slot:item.avatar_url="{ item }">
        <v-img :src="item.avatar_url" aspect-ratio="1" alt="Avatar" width="10rem"/>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-btn icon @click="viewDetail(item.login)">
          <v-icon large>mdi-eye</v-icon>
        </v-btn>
      </template>
    </v-data-table>
  </v-card>
</template>

<script lang="ts">
import Vue from "vue";
import { Member } from "../../model/member";
import { getAllMembers } from "../../api/memberAPI";

export default Vue.extend({
  name: "MemberTable",
  props: {
    members: {
      type: Array as () => Member[],
      required: true,
      default: () => [],
    }
  },
  data: () => ({
    headers: [
      {
        text: "Avatar",
        value: "avatar_url",
        filterable: false
      },
      {
        text: "ID",
        value: "id",
        filterable: false
      },
      {
        text: "Name",
        value: "login"
      },
      {
        text: "Actions",
        value: "actions"
      }
    ],
    search: '' as string,
  }),
  methods: {
    viewDetail: function(id: string) {
      this.$emit('viewDetail', id)
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
