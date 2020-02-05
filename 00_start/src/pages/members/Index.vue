<template>
  <div class="container">
    <member-detail v-bind="{show, member}" @close="closeDialog"></member-detail>
    <h2>Member Page</h2>
    <v-row align="center">
      <v-col cols="12" sm="2" md="2">
        <v-text-field label="Organization" @keyup.enter.native="loadMembers" v-model="organization"></v-text-field>
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
import { MemberTable, MemberDetail } from "../../common/components";
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
    loadMember(id: number) {
      const clickedMember = this.members.find((m) => m.id === id);
      if (clickedMember) this.member = clickedMember;
      this.showDialog();
      // getMemberById(this.organization, id).then(member => {
      //   this.member = member;
      //   this.showDialog();
      // }).catch((err) => {
      //   alert(`Error loading member | ${err}`);
      // });
    },
    showMemberDetail(id: number) {
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

<style module>
</style>
