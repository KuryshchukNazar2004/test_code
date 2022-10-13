<template>
  <div class="main">
    <h1 class="main_title">Книги Бестселери</h1>
    <h3 class="title_desc">Найпопулярніші художні та публіцистичні книги Нью-Йорка. 25 вересня 2022 р.</h3>  
    <div class="audio_books">
      <div class="container">
        <div class="audio_contain">
          <div v-if="!isPlayerVisible" >
            <div 
              v-for="(song, songIndex) in list" v-bind:key="song.id"
              v-on:click="playSong(songIndex)"
              class="content"
            >
              <div>
                <img
                  class="img_books"
                  v-bind:src="song.src"
                />
              </div>  
              <div class="general_desc">
                <span class="name">{{ song.name }}</span>
                <br/>
                <span class="name_desc">{{ song.artistName }} - {{ song.year }}</span>
              </div>
              </div> 
            </div>
          </div>
          <div v-if="isPlayerVisible">
            <AudioPlayer
              v-bind:song="list[currentSongIndex]"
              @goback="isPlayerVisible = !isPlayerVisible"
              @next = "playNext"
              @previous="playPrevious"
            />
          </div>
      </div>
    </div>
  </div>
  
</template>

<script>
import AudioPlayer from "./Audio/AudioPlayer.vue";

export default{
    data() {
        return {
            isPlayerVisible: false,
            currentSongIndex:0,
            list: [
                {
                    id: 1,
                    name: " Fairy Tale",
                    artistName: "Staphen King",
                    year: 2022,
                    src: `https://s3-alpha-sig.figma.com/img/e0e3/ca33/da553dd31e78dcafb3c3395ee2c81236?Expires=1665964800&Signature=K3X33BGRnpfarVse4jD3f0NLrPl1gX-F2ixs6ian8aQ47K-hQdwPGVn9jOW-rRhGkc-ihqKc1AwaNlDH6Ea2JdUoj-kc0NorO9DdEMwuieY7978dz63GJlDWeJJ8-EVCPJXZOfCfzJGVyiQM4cd9jv3tKSzabNHxTiazLgHPX8YzwygmV8knlSwafspF6Qk9e46dKkYV66A~6UyK0o1dhoqO0bByYqQKJt2b0uP7FrRBg1nmiRgr9jit2-I64GoTAwTgYf-HN5WOAvdRzpwxEvdWZK6j8OCOmptsDfh3m8psQVxo6CBMBu-ThI5w0TPVuVbh01JlnucCLo6wFw~7LQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA`,
                    songSrc: `https://filedn.com/lEu1SP9BiLn57JufynR40om/audiobooks/all%20quiet/1.mp3`
                },
                {
                    id: 2,
                    name: "I'm Glad My Mom Died",
                    artistName: "Jennette McCurdy",
                    year: 2022,
                    src:`https://s3-alpha-sig.figma.com/img/80ab/16b7/867f804e3e9fbb2bd46a7f084399f662?Expires=1665964800&Signature=EJqKdir1fh1jAcpbOvij~fLnzCA~4aIM-y5eZnGlvqbkQhLy8GOFPb3LZhnnPivlSWpiqBFRA9ejlgjm3B3NG~aYimn27kpqTQa6mb3Hgy~nYQQpDVljBsOoFHOCeVw98eXtYWWECf6vcL9qyLbsdKCFJx-IGt1PRfgj1W5JnByhLddX2-yQnJqaZoU~7yTwzHqQsQ2QoeypzQwDM0xDguCQEWEsP16yg0FpY3~BZweUMhlejlaKp2N7BgiB86vj07ntBeDFTpl6SeNfrEjYL2y0A2Js8l7g-uEeTg6u3cdKxn6-a07wdO1OaC9usyMZAO9YymzJ~4HYi46fgyuWmw__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA`,
                    songSrc: `https://ipaudio3.club/wp-content/uploads/STEPHEN/Fairy%20Tale%20(Stephen%20King)/01.mp3`
                },
                {
                    id: 3,
                    name: "Atomic Habits",
                    artistName: "James Clear",
                    year: 2018,
                    src:`https://s3-alpha-sig.figma.com/img/a5b7/614f/3833d1e62a2f6203036ed125fcb01eda?Expires=1665964800&Signature=EJML8aQIfpuIRir4Yu-S0dS5y9UB5pxntF44j76XP4NPWrjKcQompEWpHGpW4zkSAI~B4uNt-nDdQa9bwYNgaFEYguFCF5VO8~Hsn24C8jFcHrR4JS8Fz57inqBnVGXSqOQSnUKoaadY~ycnQswgh50DT3y3AGRy9Ig4Mo6rcIkqUkdf87uvSRozXEdHrXJH15DNWa1Dk~mt1NMgFdsRCprNSMV5wXbt5yxv8YiSxCGEFHc3Jc~Y8oZdnVIj0BIjO7p~ZEY8tHF3FqrG6ZinJRDyRBvShYcxSE2mJJeO2nq2eEox6-VkZNaI0nLzVasI99MqJoiHV-gdM3kufvGJkw__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA`,
                    songSrc: `https://filedn.com/lEu1SP9BiLn57JufynR40om/audiobooks/narnia%20book%205/Book%205%201.mp3`
                },
                {
                    id: 4,
                    name: "Where the Crawdads Sing",
                    artistName: "Delia Owens",
                    year: 2018,
                    src:`https://s3-alpha-sig.figma.com/img/2518/2ebb/d360d3eabe20abe9a8bfe9c957dfc498?Expires=1665964800&Signature=AtiAnEIhvxg48xwkHiv-6rP5wmRyM-jjLyQJfzK1Tw-20m6A42p6tAIL9GyY1Jyt9zv8Ndhtrg2N6s~aGCQ8db~nXINOek5MwSVCwE6yKYcsoamfomnQnuDRNIpX-9Zu9g0K1BK7S-qHI75ZdphKVUoSIAJ3FdCrcPSkJ3BosH0vtPBAmu1JBQStjx9N4EPYYekQZ7FVCkXluJAbqETcmTyQk3xX1o9dwsViBObXv7YVR12WHN~cprLyr9SqZBvrq4XZA7SVhwx-ld5g-L~Nzq0OhrPrtPh25vFRgudYqKr-PaybPIBMaSKN8z8ybprmSgmNqT78CCRAPJ9e8O6N8w__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA`,
                    songSrc: `https://ipaudio3.club/wp-content/uploads/STEPHEN/Fairy%20Tale%20(Stephen%20King)/01.mp3`
                },
                {
                    id: 5,
                    name: "Fire & Blood(HBO Tie-in Edition)",
                    artistName: "George R. R. Martin",
                    year: 2018,
                    src:`https://s3-alpha-sig.figma.com/img/9de8/b808/252883309ac46ad41531e8f7898c69b1?Expires=1665964800&Signature=T2FQDdhaJ54KbmziIP5iPJ5xbSMcqekeFpX7RlFzqqKfKKebyCYEY~efbcdZJN9zYpLexxEa2KRYbieJHGrP3DFNbikf-7883tdgztJOBvSmP--cv~grQIROzoLkhFdYaXU7TVzOU7sHC1eh45v5H5m7TUsHeeNV67xBaf1ntMUZm-tAx7NzVX8WH3zeoQlCyoHMA66ZhVYhL93bLhNlQ5WSAPlqt5~s4KMA1rX~TUqJVoLI~RYQr~Y2RIzIFENUlX3GyHGqmJYHynqJPozk~Fk1ABflsgPcHDPL~mtQUtP4eE2LM7an16CG94QRIjSZWD6B-GQ3KYwW2h2EUkAClA__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA`,
                    songSrc: `https://open.spotify.com/track/1k0UHV7u1Myfo4wBgjr4CS?si=ab040e64e8ca4d2c`
                },
            ]
        };
    },
    methods:{
      playSong(index){
        this.currentSongIndex = index;
        this.isPlayerVisible = true;
      },
      playNext(){
        if(this.currentSongIndex < this.list.length - 1){
          this.currentSongIndex += 1;
        } else{
          this.currentSongIndex = 0;
        }
      },
      playPrevious(){
        if(this.currentSongIndex != 0){
          this.currentSongIndex -= 1;
        } else{
          this.currentSongIndex = this.list.length - 1;
        }
      },
    },
    name: "audio",
    components: { AudioPlayer }
}
</script>

<style lang="scss">
  .main{
    margin:0 auto;
  }
  .main_title{
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 400;
    font-size: 36px;
    line-height: 42px;
    text-align: center;

    color: #BD3737;
  }
  .title_desc{
    font-family: 'Kyiv*Type Serif';
    font-style: normal;
    font-weight: 350;
    font-size: 32px;
    line-height: 38px;
    text-align: center;
    color: #FFFFFF;

  }
 .audio_books{
    background: rgba(107, 107, 107, 0.6);
    border-radius: 10%;
  }
  .audio_title{
    color:#BD3737;
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 400;
    font-size: 36px;
    line-height: 42px;
    text-align: center;
  }
  .audio_contain{
    margin-left: 20%;
  }
  .name{
    cursor: pointer;
    font-size: 25px;
  }
 .content{
  position: relative;
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 30px;
  margin-top: 20px;
  padding-top: 20px;
 }
 .img_books{
  width: 8rem;
  border-radius: 30px;
 }
.general_desc{
  margin-top: 20px;
  margin-left: 20px;
}

</style>