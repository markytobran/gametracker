<template>
  <section class="search">
    <h1>Track Player Stats Try the app with Platform: Uplay Gamertag: Solivictus</h1>
    <form v-on:submit.prevent="onSubmit">
      <div class="form-group">
        <label for="platform">Platform</label>
        <select name="platform" id="platform" v-model="platform">
          <option value="psn">Playstation</option>
          <option value="xbl">Xbox</option>
          <option value="uplay">Uplay</option>
        </select>
      </div>
      <div class="form-group">
        <label for="gamertag">Gamertag</label>
        <input
          type="text"
          name="text"
          v-model="gamertag"
          id="gamertag"
          placeholder="Uplay username, Xbox Live gamertag, PSN ID, etc"
        />
      </div>
      <div class="form-group">
        <input type="submit" value="Submit" class="btn" />
      </div>
    </form>
  </section>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      platform: 'psn',
      gamertag: ''
    };
  },
  beforeCreate() {
    document.body.className = 'body-bg-image';
  },
  methods: {
    onSubmit() {
      if (!this.gamertag) {
        this.$toasted.show('Please enter a gamertag', {
          duration: 4000,
          icon: 'exclamation-circle'
        });
      } else {
        this.$router.push(`/profile/${this.platform}/${this.gamertag}`);
      }
    }
  }
};
</script>

<style>
</style>