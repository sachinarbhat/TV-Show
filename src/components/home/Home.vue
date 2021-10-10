<template>
  <h1>Episodes Name Listing</h1>
  <br />
  <div v-for="(seasonData, group, index) in groupbySeason" :key="index">
    <h3>Starts with :{{ group }}</h3>
    <hr />
    <EpisodeDesc :episodeLists="seasonData" />
  </div>
</template>

<script>
import { defineAsyncComponent } from "vue";
const EpisodeDesc = defineAsyncComponent({
  loader: () =>
    import('./EpisodeDesc.vue'/*webpackChunkName: "Episode Name"*/),
  delay: 500
});
import data from "@/data.json";



export default {
  components: {
    EpisodeDesc
  },
  name: "home",
  data() {
    return {
      episodeLists: [],
    };
  },
  computed: {
    groupbySeason() {
      let list = {};
      let alpha = [];
      for (let i = 65; i <= 90; i++) {
        alpha.push(String.fromCharCode(i))
      }

      this.episodeLists.forEach((ele) => {
        var x = ele.name.charAt(4);

        for (let j = 0; j < 26; j++) {
          if (alpha[j] === x) {
            if (Object.keys(list).includes(x)) {
              list[x] = [...list[x], ele];
            } else {
              list[x] = [ele];
            }
          }
        }

      });

      console.log({ list });
      list = Object.entries(list).sort((a, b) => {
        if (b > a) {
          return -1;
        } else if (b < a) {
          return 1;
        } else return 0;
      });
      list = Object.fromEntries(list);
      console.log();
      return list;
    },
  },
  created() {
    this.episodeLists = data && data._embedded && data._embedded.episodes;
    console.log(this.episodeLists);
  },

  methods: {},
};
</script>

<style>
hr {
  border: 5px solid #5ea3ab;
  border-radius: 5px;
}
</style>
