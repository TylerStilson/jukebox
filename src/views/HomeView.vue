<template>
  <div id="background">
    <h1>Jukebox</h1>
    <div id="nav-menu">
      <h2>All Songs</h2>
      <h2 id="unactive" @click="redirect('/playlists')">Playlists</h2>
    </div>
    <v-slide-group class="carousel">
      <v-slide-item v-for="(song, index) in songs" :key="index">
        <v-card
          width="279"
          height="419"
          class="ml-5 my-4 px-6 py-6 rounded-xl d-flex flex-column align-center"
          :elevation="6"
          @click="test(song)"
        >
          <v-img :src="song.cover" height="256" width="256" class="rounded-lg">
          </v-img>
          <v-card-text width="128" class="title" color="">
            <div class="song-title">
              {{ song.SongName }}
            </div>
            <div class="artist-name">
              {{ song.Artist }}
            </div>
            <!-- cover: {{ song.cover }} -->
          </v-card-text>
          <v-card-subtitle class="d-flex"> </v-card-subtitle>
        </v-card>
      </v-slide-item>
    </v-slide-group>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      songs: [
        {
          SongName: "Dancing Queen",
          Artist: "ABBA",
          cover: require("../assets/images/abba.jpeg"),
          fileName: "dancingQueen.mp3",
        },
        {
          SongName: "Mamma Mia",
          Artist: "ABBA",
          cover: require("../assets/images/mamma-mia.jpeg"),
          fileName: "mammaMia.mp3",
        },
        {
          SongName: "ABC",
          Artist: "The Jackson 5",
          cover: require("../assets/images/j5-abc.jpeg"),
          fileName: "abc.mp3",
        },
        {
          SongName: "Mr. Blue Sky",
          Artist: "Electric Light Orchestra",
          cover: require("../assets/images/mr-blue-sky.jpg"),
          fileName: "blueSky.mp3",
        },
        {
          SongName: "I Want You Back",
          Artist: "The Jackson 5",
          cover: require("../assets/images/want-you-back.jpeg"),
          fileName: "wantYouBack.mp3",
        },
        {
          SongName: "Hooked On A Feeling",
          Artist: "Blue Swede, Bjorn Skifs",
          cover: require("../assets/images/hooked-on-a-feeling.jpeg"),
          fileName: "hookedOnAFeeling.mp3",
        },
        {
          SongName: "Spirit in the Sky",
          Artist: "Norman Greenbaum",
          cover: require("../assets/images/spirit-in-the-sky.jpeg"),
          fileName: "spiritInTheSky.mp3",
        },
        {
          SongName: "Aint No Mountain High Enough",
          Artist: "Marvin Gaye, Tammi Terrell",
          cover: require("../assets/images/aint-no-mountain.jpeg"),
          fileName: "mountain.mp3",
        },
        {
          SongName: "Come And Get Your Love",
          Artist: "Redbone",
          cover: require("../assets/images/come-and-get-your-love.jpeg"),
          fileName: "yourLove.mp3",
        },
        {
          SongName: "Escape (The Pina Colada Song)",
          Artist: "Rupert Holmes",
          cover: require("../assets/images/escape.jpeg"),
          fileName: "escape.mp3",
        },
        {
          SongName: "O-o-h Child",
          Artist: "The Five Stairsteps",
          cover: require("../assets/images/ooh-child.jpeg"),
          fileName: "oohChild.mp3",
        },
        {
          SongName: "The Boys Are Back In Town",
          Artist: "Thin Lizzy",
          cover: require("../assets/images/the-boys-are-back-in-town.jpeg"),
          fileName: "boysBack.mp3",
        },
      ],
      song: {},
    };
  },
  created() {
    localStorage.setItem("songs", JSON.stringify(this.songs));
  },
  methods: {
    redirect(x) {
      this.$router.push(`/${x}`);
    },
    test: function (song) {
      this.song = song;
      console.log(this.song);
    },
  },
};
</script>

<style scoped>
#background {
  background-image: url("../assets/images/background.svg");
  width: 100vw;
  height: 100vh;
  background-size: cover;
}
h1 {
  font-family: "baloo-bold";
  color: white;
  font-size: 200px;
  width: 100%;
  text-align: center;
  padding-top: 2%;
}
h2 {
  font-family: "baloo";
  color: #d90504;
  font-size: 24px;
}
#nav-menu {
  display: flex;
  justify-content: space-around;
  margin: 0px 40%;
}
#unactive {
  color: #ef8382;
}

.song-title {
  text-align: center;
  font-weight: bolder;
  font-size: 24px;
}

.artist-name {
  font-size: 18px;
  text-align: center;
}
</style>
