<template>
  <div>
    <h2>Member Page</h2>
    <v-row>
      <v-col cols="12" sm="2" md="2">
        <v-text-field label="Organization" v-model="organization"></v-text-field>
      </v-col>
      <v-col cols="12" sm="2" md="2">
        <v-btn @click="loadMembers"><v-icon>mdi-cloud-download</v-icon>Load</v-btn>
      </v-col>
    </v-row>
    <v-data-table
      :headers="headers"
      :items="members"
      :items-per-page="5"
      class="elevation-1"
    ></v-data-table>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Member } from "../../model/member";
import { getAllMembers } from "../../api/memberAPI";

export default Vue.extend({
  name: "MemberTable",
  data: () => ({
    members: [] as Member[],
    headers: [{
      text: 'ID',
      value: 'id',
    },
    {
      text: 'Avatar',
      value: 'avatar_url',
    },
    {
      text: 'Name',
      value: 'login',
    }],
    organization: 'lemoncode' as string,
  }),
  methods: {
    loadMembers: function() {
      getAllMembers(this.organization).then(members => {
        this.members = members;
      });
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
