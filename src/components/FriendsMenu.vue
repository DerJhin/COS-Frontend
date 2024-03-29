<script lang="ts">
import {CaseService} from "@/services/case.service"

export default {
  data() {
    return {
      tab: null,
      searchInput: '',
      friends: [],
      searchedUsers: []
    }
  },
  created() {
    this.getFriends()
  },
  methods: {
    async getFriends() {
      try {
        this.friends = await CaseService.getFriends();
      } catch (error) {
        console.error('Error fetching case data:', error);
      }
    },
    async searchFriend() {
      try {
        this.searchedUsers = await CaseService.searchFriend(this.searchInput)
      } catch (error) {
        console.error("Error searching friends:", error);
      }
    },
    async sendFriendRequest(userId) {
      try {
        await CaseService.sendFriendRequest(userId);
        console.log('Friend request sent successfully');
      } catch (error) {
        console.error('Error sending friend request:', error);
      }
    }
  },
  computed: {
    filteredFriends() {
      return this.friends.filter(friend => {
        return friend.username.toLowerCase().includes(this.searchInput.toLowerCase());
      });
    }
  }
}
</script>

<template>
  <v-menu :close-on-content-click=false>
    <template v-slot:activator="{ props }">
      <svg xmlns="http://www.w3.org/2000/svg" height="24" width="30" viewBox="0 0 640 512" v-bind="props" class="pointer">
        <path d="M96 128a128 128 0 1 1 256 0A128 128 0 1 1 96 128zM0 482.3C0 383.8 79.8 304 178.3 304h91.4C368.2 304 448 383.8 448 482.3c0 16.4-13.3 29.7-29.7 29.7H29.7C13.3 512 0 498.7 0 482.3zM609.3 512H471.4c5.4-9.4 8.6-20.3 8.6-32v-8c0-60.7-27.1-115.2-69.8-151.8c2.4-.1 4.7-.2 7.1-.2h61.4C567.8 320 640 392.2 640 481.3c0 17-13.8 30.7-30.7 30.7zM432 256c-31 0-59-12.6-79.3-32.9C372.4 196.5 384 163.6 384 128c0-26.8-6.6-52.1-18.3-74.3C384.3 40.1 407.2 32 432 32c61.9 0 112 50.1 112 112s-50.1 112-112 112z"/>
      </svg>
    </template>
    <v-card>
      <v-tabs v-model="tab" background-color="primary" class="justify-center" dark>
        <v-tab value="friends">Freunde</v-tab>
        <v-tab value="add">Hinzufügen</v-tab>
      </v-tabs>
      <v-window v-model="tab">
        <v-window-item value="friends">
          <div class="search-bar">
            <v-text-field
                label="Suchen..."
                type="text"
                v-model="searchInput"
            />
          </div>
          <v-list>
            <v-list-item
              v-for="friend in filteredFriends"
              :key="friend.id"
              :title="friend.username"
              :prepend-avatar="'../../../icons/capy-logo-transparent.png'"
            ></v-list-item>
          </v-list>
        </v-window-item>

        <v-window-item value="add">
          <div class="search-bar">
            <v-text-field
                label="Suchen..."
                type="text"
                v-model="searchInput"
                @input="searchFriend()"
            />
          </div>
          <v-list>
            <v-list-item
                v-for="user in searchedUsers"
                :key="user.id"
                :title="user.username"
                :prepend-avatar="'../../../icons/capy-logo-transparent.png'"
            >
              <v-btn @click="sendFriendRequest(user.id)">Hinzufügen</v-btn>
            </v-list-item>
          </v-list>
        </v-window-item>
      </v-window>
    </v-card>
  </v-menu>
</template>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>