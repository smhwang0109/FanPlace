<template>
  <div class="my-4">
    <div class="row d-flex justify-content-center">
      <h3 class="text-center mb-0">어떤 배우의 게시물을 작성하고 싶으신가요?</h3>
    </div>
    <hr>
    <div class="row customcard p-3 justify-content-around">
      <router-link :to="{ name: 'ArticleCreate', params:{ actor_id: actor.id, actor: actor } }" class="col-2 px-0 mx-2 profile-container" v-for="actor in actors" :key="actor.id">
        <img v-if="actor.profile_path" class="img-fluid rounded-circle image" :src="`https://image.tmdb.org/t/p/w300_and_h300_bestv2/${actor.profile_path}`" :alt="`${actor.name} profile`">
        <img v-else class="img-fluid rounded-circle image" :src="`http://placehold.jp/300x300.png?text=${actor.name}`" :alt="`${actor.name} profile`">
        <div class="overlay rounded-circle">
          <div class="text">{{ actor.name }}</div>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
  name: 'ActorSelect',
  computed: {
    ...mapState(['actors']),    
  },
  methods: {
    ...mapActions(['fetchActors']),
  },
  created() {
    this.fetchActors('')
  },
}
</script>

<style>
.profile-container {
  position: relative;
}

.profile-container:hover {
  cursor: pointer;
}

.image {
  display: block;
  width: 100%;
  height: auto;
}

.overlay {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 0;
  transition: .5s ease;
  background-color: #3e3f3f;
}

.profile-container:hover .overlay {
  opacity: 0.8;
}

.text {
  color: white;
  font-size: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  text-align: center;
  width: 80%;
  font-weight: bold;
}
</style>