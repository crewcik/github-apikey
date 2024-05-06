<style>
* {
  box-sizing: border-box;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

body {
  background-image: url("https://i.pinimg.com/originals/e8/56/fd/e856fdf50ec536d4f3feac12d658f7d1.jpg");
  background-position: center;
  background-repeat: no-repeat;
}

.main {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #000;
  border-radius: 30px;
  text-align: center;
  box-shadow: 0 0 50px 7px #6a5acd;
}

.avatar {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  margin-bottom: 20px;
  border: 4px solid #6a5acd;
  box-shadow: 0 0 30px #6a5acd;
}

h1 {
  font-size: 28px;
  margin-bottom: 10px;
  color: #fff;
}

h2 {
  font-size: 20px;
  margin-bottom: 5px;
  color: #ffffff;
}

p {
  font-size: 18px;
  margin-bottom: 10px;
  color: #ffffff;
}

.linkBtn {
  display: inline-block;
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #fff;
  color: #000a37;
  text-decoration: none;
  border-radius: 5px;
  transition: box-shadow 0.7s ease;
}

.linkBtn:hover {
  box-shadow: 0 0 50px 7px #ffffff;
}

.bioCrew {
  margin-top: 30px;
}

.bioCrew h2 {
  font-size: 18px;
  margin-bottom: 5px;
  color: #ffffff;
}

.bioCrew a {
  display: block;
  margin-top: 5px;
  text-decoration: none;
  color: #ffffff;
}

.bioCrew a:hover {
  text-decoration: underline;
}

.hesapBilgisi h3 {
    color: #fff;
    font-size: 15px
}

span {
  color: #6a5acd;
}

</style>

<template>
  <div class="main">
    <img class="avatar" :src="user.avatar_url" alt="Yükleniyor">
    <h1>{{ user.name }} <span style="font-size: 15px;"> ({{ user.login }})</span></h1>
    <h2>{{ user.bio }}</h2>
    <p>Followers: {{ user.followers }}</p>
    <p>Following: {{ user.following }}</p>
    <p>Projects: {{ user.public_repos }}</p>
    <p>Total Stars: {{ totalStars }}</p>
    <a :href="user.blog" class="linkBtn">{{ user.blog }}</a>

    <div class="bioCrew">
      <h2>{{ user.company ? "Şirket: " + user.company : "" }}</h2>
      <h2>{{ user.location ? "Lokasyon: " + user.location : "" }}</h2>
      <a href="{{ user.twitter_username }}">{{ user.twitter_username ? "Twitter" + user.twitter_username : "" }}</a>
    </div>

    <div class="hesapBilgisi">
      <h3>Bu profil <span>{{ user.created_at }}</span> tarihinde kurulmuş ve <span>{{ user.updated_at }}</span> tarihinde en son güncellenmiş.</h3>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      user: {},
      totalStars: 0
    };
  },
  mounted() {
    axios.get('https://api.github.com/users/crewcik/starred').then(response => {
      this.totalStars = response.data.length;
    });

    axios.get('https://api.github.com/users/crewcik').then(response => {
      this.user = response.data;
    });
  }
};
</script>
