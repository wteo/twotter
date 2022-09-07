<script>

import TwootItem from './TwootItem.vue';

export default {
  data() {
    return {
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instance', name: 'Instance' }
        ],
      followers: 0,
      user: {
        id: 1,
        username: '_WendyTeo',
        firstName: 'Wendy',
        lastName: 'Teo',
        email: 'wteo@gmail.com',
        admin: true,
        twoots: [
        { id: 1, content: 'Twotter is amazing!' }, 
        { id: 2, content: `Please don't forget to subscribe!` }
        ],
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  watch: {
    // watches data point when it changes and thus runs a functions
    // similar to useEffect();
    // pass two parameters that accepts the updated state value and the previous state value.
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
        console.log(`Favourited Tweet ${id}`);
    },
    createNewTwoot() {
        if (this.newTwootContent && this.selectedTwootType !== 'draft') {
            this.user.twoots.unshift({ 
                    id: this.user.twoots.length + 1,
                    content: this.newTwootContent
            });
        }
        this.newTwootContent = '';
    }
  },
  mounted() {
  // automatically renders functions for the first time
  // lifecycle hooks 
    this.followUser();
  },
  components: { TwootItem }
}

</script>

<template>
    <div class="user-profile">
        <div class="user-profile_user-panel">
            <h1 class="user-profile_username">@{{ user.username }}</h1>
            <div class="user-profile_admin-badge" v-if="user.admin">Admin
            </div>
            <div class="user-profile_follower-count">
                <strong>Followers: </strong> {{ followers }}
            </div>
            <form class="user_profile_create-twoot" @submit.prevent="createNewTwoot">
                <label for="newTwoot"><strong>New Twoot</strong></label>
                <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>
                <div class="user-profile_create-twoot-type">
                    <label for="newTwootType"><strong>Type: </strong></label>
                    <select id="newTwoot" v-model="selectedTwootType">
                        <option v-bind:value="option.value" v-for="option in twootTypes" v-bind:key="index">
                            {{ option.name }}
                        </option>
                    </select>
                </div>
                <button>
                    Twoot!
                </button>
            </form>
        </div>
        <div class="_user-profile_twoots-wrapper">
            <TwootItem v-for="twoot in user.twoots" v-bind:key="twoot.id" v-bind:username="user.username" v-bind:twoot="twoot" @favouriteTwoot="toggleFavourite" />    
        </div>
    </div>
</template>

<style>

.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile_admin-badge {
    background-color: darkred;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

.user_profile_create-twoot {
    display: flex;
    flex-direction: column;
    padding-top: 20px;
}

h1 {
    margin: 0;
}

</style>



