<template>
  <div id="background">
    <h1>Jukebox</h1>
    <div id="nav-menu">
      <h2>All Songs</h2>
      <h2 id="unactive" @click="redirect('playlists')">Playlists</h2>
    </div>
    <v-slide-group class="carousel">
      <v-slide-item v-for="(song, index) in songs" :key="index">
        <v-card
          width="279"
          height="419"
          class="ml-5 my-4 px-6 py-6 rounded-xl d-flex flex-column align-center"
          :elevation="6"
          
        >
          <v-img :src="song.cover" height="256" width="256" class="rounded-lg" @click="playSong(song)">
          </v-img>
          <v-card-text width="128" class="title" color="">
            <div class="song-title">
              {{ song.SongName }}
            </div>
            <div class="artist-name">
              {{ song.Artist }}
            </div>
            <div v-if="playingIndex == index" id="center">
              <!-- <img src="../assets/images/sound.svg" alt=""> -->
              <div v-if="songState == 'play'">
                <img src="../assets/images/pause.svg" alt="" @click="pauseSong()">
              </div>
              <div v-if="songState == 'pause'">
                <img src="../assets/images/play.svg" alt="" @click="resumeSong()">
              </div>
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
          fileName: "danceq.mp3",
          pathName: "dancingQueen"
        },
        {
          SongName: "Mamma Mia",
          Artist: "ABBA",
          cover: require("../assets/images/mammamia.jpeg"),
          fileName: "mammamia.mp3",
          pathName: "mammaMia"
        },
        {
          SongName: "ABC",
          Artist: "The Jackson 5",
          cover: require("../assets/images/j5-abc.jpeg"),
          fileName: "ABC.mp3",
          pathName: "abc"
        },
        {
          SongName: "Mr. Blue Sky",
          Artist: "Electric Light Orchestra",
          cover: require("../assets/images/mrbluesky.jpg"),
          fileName: "bluesky.mp3",
          pathName: "mrBlueSky"
        },
        {
          SongName: "I Want You Back",
          Artist: "The Jackson 5",
          cover: require("../assets/images/wantuback.jpeg"),
          fileName: "wantubak.mp3",
          pathName: "wantYouBack"
        },
        {
          SongName: "Hooked On A Feeling",
          Artist: "Blue Swede, Bjorn Skifs",
          cover: require("../assets/images/hookedon.jpeg"),
          fileName: "hookedon.mp3",
          pathName: "hookedOnAFeeling"
        },
        {
          SongName: "Spirit in the Sky",
          Artist: "Norman Greenbaum",
          cover: require("../assets/images/spiritinsky.jpeg"),
          fileName: "spiritin.mp3",
          pathName: "spiritInTheSky"
        },
        {
          SongName: "Aint No Mountain High Enough",
          Artist: "Marvin Gaye, Tammi Terrell",
          cover: require("../assets/images/aint-no.jpeg"),
          fileName: "aintno.mp3",
          pathName: "aintNoMountain"
        },
        {
          SongName: "Come And Get Your Love",
          Artist: "Redbone",
          cover: require("../assets/images/geturluv.jpeg"),
          fileName: "geturluv.mp3",
          pathName: "comeAndGetYourLove"
        },
        {
          SongName: "Escape (The Pina Colada Song)",
          Artist: "Rupert Holmes",
          cover: require("../assets/images/escape.jpeg"),
          fileName: "escape.mp3",
          pathName: "escapePinaColada"
        },
        {
          SongName: "O-o-h Child",
          Artist: "The Five Stairsteps",
          cover: require("../assets/images/oohchild.jpeg"),
          fileName: "ohchild.mp3",
          pathName: "oohChild"
        },
        {
          SongName: "The Boys Are Back In Town",
          Artist: "Thin Lizzy",
          cover: require("../assets/images/boysareback.jpeg"),
          fileName: "boysrbak.mp3",
          pathName: "theBoysAreBackInTown"
        },
      ],
      song: {},
      playingIndex: null,
      songState: 'play'
    };
  },
  created() {
    localStorage.setItem("songs", JSON.stringify(this.songs));
  },
  methods: {
    redirect(x) {
      this.$router.push(`/${x}`);
    },
    playSong: function (song) {
      for ( var i in this.songs){
        if (this.songs[i].fileName == song.fileName){
          this.playingIndex = i;
          console.log("songIndex: ", this.playingIndex);
        }
      }
      this.song = song;
      console.log("song=",this.song);
      var data = 'song=' + encodeURIComponent(song.fileName);
      fetch('http://192.168.4.1/song', {
        method: 'POST',
        body: data,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      });
    },
    pauseSong(){
      this.songState = 'pause';
      var data = 'pause=' + encodeURIComponent(this.songState);
      fetch('http://192.168.4.1/pause', {
        method: 'POST',
        body: data,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      });
    },
    resumeSong(){
      this.songState = 'play';
      var data = 'play=' + encodeURIComponent(this.songState);
      fetch('http://192.168.4.1/play', {
        method: 'POST',
        body: data,
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      });
    }
  },
};
</script>

<style scoped>
#center{
  text-align: center;
}
#background {
  background-image: url("../assets/images/background.svg");
  width: 100vw;
  height: 100vh;
  background-size: cover;
}
h1 {
  font-family: "baloo-bold";
  color: white;
  font-size: 140px;
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
.carousel{
  width: 85%;
  padding-left: 15%;
}
@media (max-width: 425px){
  #background {
    background-image: url("../assets/images/mobile-back.svg");
    width: 169%;
    height: 1200px;
    background-size: cover;
  }
  h1{
    font-size: 100px;
  }
  h2{
    font-size: 18px;
  }
  #nav-menu{
    margin: 0px 30%;
  }
  .carousel{
    margin-top: 50px;
  }

}
</style>
