<template>
  <section>
    <div v-if="loading">
      <h3>Loading...</h3>
    </div>

    <div v-if="error">
      <h1>{{error}}</h1>
      <router-link to="/">Go Back</router-link>
    </div>

    <div v-if="profileData != undefined" class="container">
      <h1 class="gamertag">
        <img :src="profileData.platformInfo.avatarUrl" alt class="platform-avatar" />
        {{profileData.platformInfo.platformUserIdentifier}}
      </h1>
      <div class="grid">
        <div>
          <img src="../assets/divi.png" alt="division" />
        </div>
        <div>
          <ul>
            <li>
              <h4>Player level</h4>
              <p>LEVEL {{ profileData.segments[0].stats.highestPlayerLevel.displayValue }}</p>
            </li>
            <li>
              <h4>Headshots</h4>
              <p>
                {{ profileData.segments[0].stats.headshots.displayValue }}
                <span>({{ profileData.segments[0].stats.headshots.percentile }}%)</span>
              </p>
            </li>
            <li>
              <h4>Skill Kills</h4>
              <p>
                {{ profileData.segments[0].stats.killsSkill.displayValue }}
                <span>({{ profileData.segments[0].stats.killsSkill.percentile }}%)</span>
              </p>
            </li>
            <li>
              <h4>Time Played</h4>
              <p>{{ profileData.segments[0].stats.timePlayed.displayValue }}</p>
            </li>
            <li>
              <h4>Players Killed</h4>
              <p>
                {{ profileData.segments[0].stats.playersKilled.displayValue }}
                <span>({{ profileData.segments[0].stats.playersKilled.percentile }}%)</span>
              </p>
            </li>
          </ul>
        </div>
        <router-link to="/">Go Back</router-link>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Profile',
  data() {
    return {
      loading: false,
      error: null,
      profileData: null
    };
  },
  beforeCreate() {
    document.body.className = 'body-bg-no-image';
  },
  async created() {
    this.loading = true;

    try {
      const res = await axios.get(
        `/api/v1/profile/${this.$route.params.platform}/${this.$route.params.gamertag}`
      );
      this.profileData = res.data.data;
      this.loading = false;
    } catch (err) {
      this.loading = false;
      this.error = err.response.data.message;
    }
  }
};
</script>

<style scoped>
.container {
  background: rgba(0, 0, 0, 0.5);
  color: #fff;
  max-width: 700px;
  margin: 1rem auto;
  padding: 2rem 1.5rem;
  border-radius: 20px;
}
h1.gamertag {
  font-size: 2rem;
  background: rgba(0, 0, 0, 0.6);
  padding: 0.3rem 0.5rem;
  text-align: center;
  border-radius: 20px;
  margin-bottom: 3rem;
  display: flex;
  align-items: center;
}
a {
  display: inline-block;
  margin-top: 2rem;
  border: #fff 2px solid;
  padding: 0.5rem 0.8rem;
}
a:hover {
  border: #ccc 2px solid;
  color: #ccc;
}
.platform-avatar {
  width: 60px;
  padding: 4px;
  margin-right: 0.7rem;
}
img {
  width: 100%;
}
.grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 1rem;
}
li {
  background: rgba(0, 0, 0, 0.6);
  padding: 1rem;
  margin-bottom: 0.7rem;
  border-radius: 10px;
}
li p {
  font-size: 2rem;
}
li:first-child p {
  font-size: 1.5rem;
}
li span {
  font-size: 1rem;
  color: #ccc;
}
@media (max-width: 500px) {
  h1 {
    font-size: 1.5rem;
    display: block;
    text-align: center;
  }
  .platform-avatar {
    display: none;
  }
  .grid {
    grid-template-columns: 1fr;
  }
  li p {
    font-size: 1.5rem;
  }
}
</style>