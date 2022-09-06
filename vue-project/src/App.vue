<script>

export default {
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: '_WendyTeo',
        firstName: 'Wendy',
        lastName: 'Teo',
        email: 'wteo@gmail.com',
        admin: true
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
    }
  },
  mounted() {
  // automatically renders functions for the first time
  // lifecycle hooks 
    this.followUser();
  }
}

</script>

<template>
  <div>
    @{{ user.username }} - {{ fullName}}
    <strong>Followers:</strong> {{ followers }}
    <button @click='followUser'>Follow</button>
  </div>
</template>

<style scoped>
</style>
