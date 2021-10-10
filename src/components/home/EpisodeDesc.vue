<template>
  <div class="container--episode">
    <div class="section" v-for="(episode, index) in episodeLists" :key="index">
      <div class="card">
        <v-lazy-image :src="episodeImage(episode)" alt="images" style="width: 100%" />
        <p class="info" style="font-weight:700">Season {{ episode.season }}</p>
        <p class="info" style="font-weight:700">Episode {{ episode.number }}</p>
        <p class="info" style="font-weight:500;color:#372768">{{ episode.name }}</p>
        <div class="desc info" v-html="episode.summary"></div>
      </div>
    </div>
  </div>
</template>

<script>
import VLazyImage from "v-lazy-image";
export default {
  data() {
    return {};
  },
  components: {
    VLazyImage
  },
  props: {
    episodeLists: {
      type: Array,
      default: null,
    },
  },
  methods: {
    episodeImage(episode) {
      return episode && episode.image && episode.image.medium;
    },
  },
};
</script>

<style>
.container--episode {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
.section {
  margin-bottom: 40px;
}
.card {
  height: 275px;
  width: 275px;
  border: 2px solid #146169;
  text-align: center;
  border-radius: 5px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
.info {
  margin: 2px;
  font-size: 14px;
}
p {
  margin: 0px;
}
.desc {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  font-size: 12px;
}
</style>