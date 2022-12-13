<template>
  <div id="background">
    <h1>Jukebox</h1>
    <div id="nav-menu">
      <h2 id="unactive" @click="redirect('')">All Songs</h2>
      <h2>Playlists</h2>
    </div>

    <div id="cont">
      <v-card v-for="(playlist, index) in playlists" v-bind:key="index" class="playlistCard" @click="playdialog(index)">
        <h3>{{playlists[index].playlistName}}</h3>
        <h4>{{playlists[index].description}}</h4>
      </v-card>

    </div>

    <v-dialog
      v-model="dialog2"
      class="dialog-size"
      >

      <v-card id="newFlex" class="scrollOverflow">
        <div id="head">
          <div id="newHead">{{diaName}}</div>
          <div id="newSub">{{diaDesc}}</div>
        </div>
        
        <v-divider></v-divider>
        <div v-for="(song, index) in diaSongs" v-bind:key="index" class="rowFlex" @click="playSong(index)">
          <div class="colFlex">
            <div>
              <h5>{{diaSongs[index].SongName}}</h5>
              <h6>{{diaSongs[index].Artist}}</h6>
            </div>
            <div v-if="(playlistIndex == index)" class="addicon">
              <!-- <img src="../assets/images/sound.svg" alt=""> -->
              <div v-if="songState == 'play'">
                <img src="../assets/images/pause.svg" alt="" @click="pauseSong()">
              </div>
              <div v-if="songState == 'pause'">
                <img src="../assets/images/play.svg" alt="" @click="resumeSong()">
              </div>
            </div>
          </div>
          <v-divider class="newdiv"></v-divider>
        </div>
      </v-card>
    </v-dialog>

    <v-btn
      color="#3097F3"
      fab
      dark
      id="fab-btn"
      @click="createNew()"
      >
      <img id="fab-icon" src="../assets/images/plus.svg">
    </v-btn>

    <v-dialog
      v-model="dialog"
      class="dialog-size"
      >
      <v-card id="newFlex" class="scrollOverflow">
        <div id="head">
          <input type="text" value="playName" v-model="PlayName" placeholder="Playlist Name" id="newHead">
          <input type="text" value="playDesc" v-model="PlayDesc" placeholder="Playlist Description" id="newSub">
        </div>
        
        <v-divider></v-divider>
        <div v-for="(song, index) in songs" v-bind:key="index" class="rowFlex" @click="addSong(index)">
          <div class="colFlex">
            <div>
              <h5>{{songs[index].SongName}}</h5>
              <h6>{{songs[index].Artist}}</h6>
            </div>
            <div v-if="(addedSongs.includes(index))" class="addicon">
              <img src="../assets/images/check.svg" alt="">
            </div>
            <div v-else class="addicon">
              <img src="../assets/images/add.svg" alt="">
            </div>
            
          </div>
          <v-divider class="newdiv"></v-divider>
        </div>
        <div class="whitespace"></div>
        <button id="createButton" @click="createNewPlaylist()">Create Playlist</button>
      </v-card>

    </v-dialog>
    
  </div>

</template>

<script>

  export default {
    name: 'Playlist',
    data () {
      return {
        dialog: false,
        dialog2: false,
        PlayName: '',
        PlayDesc: '',
        Selected: [],
        playlists: [
          // {
          //   playlistName: 'Geez Marty, When Are We',
          //   description: 'rewind with a flash from the past',
          //   songs: [{
          //             SongName: "Mr. Blue Sky",
          //             Artist: "Electric Light Orchestra",
          //             cover: require("../assets/images/mrbluesky.jpg"),
          //             fileName: "bluesky.mp3",
          //             pathName: "mrBlueSky"
          //           },
          //           {
          //             SongName: "I Want You Back",
          //             Artist: "The Jackson 5",
          //             cover: require("../assets/images/wantuback.jpeg"),
          //             fileName: "wantubak.mp3",
          //             pathName: "wantYouBack"
          //           },
          //           {
          //             SongName: "Hooked On A Feeling",
          //             Artist: "Blue Swede, Bjorn Skifs",
          //             cover: require("../assets/images/hookedon.jpeg"),
          //             fileName: "hookedon.mp3",
          //             pathName: "hookedOnAFeeling"
          //           },
          //           {
          //             SongName: "Spirit in the Sky",
          //             Artist: "Norman Greenbaum",
          //             cover: require("../assets/images/spiritinsky.jpeg"),
          //             fileName: "spiritin.mp3",
          //             pathName: "spiritInTheSky"
          //           },
          //           {
          //             SongName: "Aint No Mountain High Enough",
          //             Artist: "Marvin Gaye, Tammi Terrell",
          //             cover: require("../assets/images/aint-no.jpeg"),
          //             fileName: "aintno.mp3",
          //             pathName: "aintNoMountain"
          //           },
          //         ]
          // },
          // {
          //   playlistName: 'Doc I Think We Miss Calculated',
          //   description: 'rewind with a flash from the past, again',
          //   songs: [{
          //             SongName: "Come And Get Your Love",
          //             Artist: "Redbone",
          //             cover: require("../assets/images/geturluv.jpeg"),
          //             fileName: "geturluv.mp3",
          //             pathName: "comeAndGetYourLove"
          //           },
          //           {
          //             SongName: "Escape (The Pina Colada Song)",
          //             Artist: "Rupert Holmes",
          //             cover: require("../assets/images/escape.jpeg"),
          //             fileName: "escape.mp3",
          //             pathName: "escapePinaColada"
          //           },
          //           {
          //             SongName: "O-o-h Child",
          //             Artist: "The Five Stairsteps",
          //             cover: require("../assets/images/oohchild.jpeg"),
          //             fileName: "ohchild.mp3",
          //             pathName: "oohChild"
          //           },
          //           {
          //             SongName: "The Boys Are Back In Town",
          //             Artist: "Thin Lizzy",
          //             cover: require("../assets/images/boysareback.jpeg"),
          //             fileName: "boysrbak.mp3",
          //             pathName: "theBoysAreBackInTown"
          //           },
          //           {
          //             SongName: "Dancing Queen",
          //             Artist: "ABBA",
          //             cover: require("../assets/images/abba.jpeg"),
          //             fileName: "danceq.mp3",
          //             pathName: "dancingQueen"
          //           },
          //           {
          //             SongName: "Mamma Mia",
          //             Artist: "ABBA",
          //             cover: require("../assets/images/mammamia.jpeg"),
          //             fileName: "mammamia.mp3",
          //             pathName: "mammaMia"
          //           },
          //           {
          //             SongName: "ABC",
          //             Artist: "The Jackson 5",
          //             cover: require("../assets/images/j5-abc.jpeg"),
          //             fileName: "ABC.mp3",
          //             pathName: "abc"
          //           }
          //         ]
          // }
        ],
        songs: [],
        addedSongs: [],
        addedSongNames: [],
        diaName: '',
        diaDesc: '',
        diaSongs: [],
        playlistIndex: null,
        songState: 'play'

      }
    },
    created(){
      console.log("hello");
      var x = JSON.parse(localStorage.getItem("songs"));
      if (x == null || x == "") {
        x = [];
      }
      this.songs = x;

      var y = JSON.parse(localStorage.getItem("playlists"));
      if (y == null || y == "") {
        y = [];
      }
      this.playlists = y;

    },
    methods: {
      redirect(x){
        this.$router.push(`/${x}`);
      },
      createNew(){
        this.dialog = true;
      },
      addSong(index){
        console.log(index);
        this.addedSongs.push(index);
      },
      createNewPlaylist(){
        console.log(this.addedSongs);
        for ( var i in this.songs){
          for (var j in this.addedSongs){
            if ( i == this.addedSongs[j]){
              console.log('got a song');
              this.addedSongNames.push(this.songs[i]);
            }
          }
        }
        this.playlists.push({
          playlistName: this.PlayName,
          description: this.PlayDesc,
          songs: this.addedSongNames,
        });
        this.dialog = false;

        localStorage.setItem("playlists", JSON.stringify(this.playlists));

      },
      playdialog(index){
        console.log("playdialog index: ",index);
        this.diaDesc = this.playlists[index].description;
        console.log("desc: ", this.diaDesc);
        this.diaName = this.playlists[index].playlistName;
        this.diaSongs = this.playlists[index].songs;
        this.dialog2 = true;
      },
      playSong(index){
        console.log("playsong index: ",index);
        this.playlistIndex = index;
        console.log("playistINdex: ", this.playlistIndex);
        var song = this.diaSongs[index].fileName;
        this.songState = 'play';

        var data = 'song=' + encodeURIComponent(song);
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

    }

  }
</script>

<style scoped>
.dialog-size{
  width: 50%;
  height: 50%;
}
.volumn-icon{
  color: black;
}
.whitespace{
  height: 100px;
}
#createButton{
  background-color: #F2B705;
  color: white;
  font-family: 'lato';
  font-size: 26px;
  position: fixed;
  bottom: 7%;
  right: 27%;
  border-radius: 12px;
  padding: 15px;
}
.addicon{
  padding-right: 60px;
}
#background{
  background-image: url('../assets/images/background.svg');
  width: 100vw;
  height: 100vh;
  background-size: cover;
}
h1{
  font-family: 'baloo-bold';
  color: white;
  font-size: 140px;
  width: 100%;
  text-align: center;
  padding-top: 2%;
}
h2{
  font-family: 'baloo';
  color: #D90504;
  font-size: 24px;
}
#nav-menu{
  display: flex;
  justify-content: space-around;
  margin: 0px 40%;
}
#unactive{
  color: #EF8382;
}
#cont{
  margin: 5% 20%;
}
.playlistCard{
  margin-bottom: 3%;
  height: 120px;
}
h3{
  font-family: 'lato-bold';
  font-size: 24px;
  padding: 25px 35px 10px 35px;
}
h4{
  font-family: 'lato';
  font-size: 16px;
  padding: 0px 35px 25px 35px;
}
#fab-btn{
  position: fixed;
  bottom: 5%;
  right: 15%;
  width: 100px;
  height: 100px;
}
#fab-icon{
  width: 50px;
  height: 50px;
  font-size: 50px;
}
#newHead{
  font-family: 'lato-bold';
  font-size: 24px;
}
#newSub{
  font-family: 'lato';
  font-family: 16px;
}
#newFlex{
  display: flex;
  flex-direction: column;
}
#head{
  margin: 40px 60px;
  display: flex;
  flex-direction: column;
}
.rolFlex{
  display: flex;
  flex-direction: row;
}
.colFlex{
  display: flex;
  flex-direction: row;
  padding-left: 60px;
  align-items: center;
  justify-content: space-between;
}
h5{
  font-family: 'lato';
  font-size: 24px;
  color: #0360D9;
}
h6{
  font-family: 'lato';
  font-size: 16px;
  color: #0360D9;
}
.scrollOverflow {
  overflow: scroll;
}
.newdiv{
  margin-top: 10px;
  margin-bottom: 10px;
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
  #cont{
    margin: 5% 10%;
  }
  .dialog-size{
    width: 75%;
    height: 50%;
    margin: 32px !important;
  }
  .v-dialog{
    margin: 32px !important;
  }
  #createButton{
    right: 11%;
  }
}
</style>