<script lang="ts">

import {CaseService} from "@/services/case.service";

export default {
  props: ['caseName'],
  data() {
    return {
      caseItems: [
        {
          id: 1,
          name: "TestItem1",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Blue"
        },
        {
          id: 2,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Gold"
        },
        {
          id: 3,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Gold"
        },
        {
          id: 4,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Gold"
        },
        {
          id: 5,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Gold"
        },
        {
          id: 6,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Purple"
        },
        {
          id: 7,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Pink"
        },
        {
          id: 8,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Gold"
        },
        {
          id: 9,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Purple"
        },
        {
          id: 10,
          name: "TestItem2",
          image: "../../../icons/capy-logo-transparent.png",
          rarity: "Pink"
        }
      ]
    }
  },
  mounted() {
    //this.getCaseData()
  },
  methods: {
    async getCaseData() {
      try {
        this.caseItems = await CaseService.getCaseData(this.caseName);
      } catch (error) {
        console.error('Error fetching case data:', error);
      }
    }
  }
}
</script>

<template>
  <v-col>
    <v-row>
      <v-col v-for="(item) in caseItems" :key="item.id">
        <v-card :style="{ borderRight: '8px solid ' + item.rarity }">
          <img :src="item.image" :alt="item.id" height="150" />
        </v-card>
      </v-col>
    </v-row>
  </v-col>
</template>

<style scoped>
.v-card {
  max-width: 160px;
  max-height: 150px;
}

.v-col {
  flex-grow: 0;
  padding: 6px;
}

.v-row {
  justify-content: center;
}
</style>