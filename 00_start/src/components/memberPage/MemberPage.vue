<template>
  <div>
    <member-detail v-bind="{show, member}" @close="closeDialog"></member-detail>
    <h2>Member Page</h2>
    <v-row>
      <v-col cols="12" sm="2" md="2">
        <v-text-field label="Organization" v-model="organization"></v-text-field>
      </v-col>
      <v-col cols="12" sm="2" md="2">
        <v-btn icon @click="loadMembers"><v-icon>mdi-cloud-download</v-icon></v-btn>
      </v-col>
    </v-row>
    <member-table v-bind="{members}" @viewDetail="showMemberDetail($event)"></member-table>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { MemberTable } from "../memberTable";
import { MemberDetail } from "../memberDetail";
import { Member } from "../../model/member";
import { getAllMembers, getMemberById } from "../../api/memberAPI";

export default Vue.extend({
  name: "MemberPage",
  components: {
    MemberTable,
    MemberDetail
  },
  data: () => ({
    members: [] as Member[],
    organization: 'lemoncode' as string,
    show: false as boolean,
    member: {} as Member,
  }),
  mounted() {
    this.loadMembers();
  },
  methods: {
    loadMembers() {
      getAllMembers(this.organization).then(members => {
        this.members = members;
      });
    },
    loadMember(id: string) {
      getMemberById(this.organization, id).then(member => {
        this.member = member;
        this.showDialog();
      });
    },
    showMemberDetail(id: string) {
      this.loadMember(id);
    },
    showDialog() {
      this.show = true;
    },
    closeDialog() {
      this.show = false,
      this.member = {} as Member;
    },
  }
});
</script>
