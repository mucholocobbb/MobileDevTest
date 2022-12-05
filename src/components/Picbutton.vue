<template>
  <div class="app">
    <div class="app_upblock">
      <img class="app_logo" alt="Cat logo" src="../assets/logo.png" />
      <h1 class="app_headtext">{{ msg }}</h1>
    </div>
    <img class="app_image" :src="picSrc" :alt="altText" />
    <button class="app_btn" @click="togglePic">CLICK ME</button>
    <button
      class="app_muteBtn"
      :class="{ unmute: !isMute }"
      @click="toggleMute"
    >
      <img v-if="isMute" src="../assets/mute.png" alt="mute" />
      <img v-else src="../assets/unmute.png" alt="unmute" />
    </button>
    <button class="app_testBtn" @click="testAndroidApi">Test Ui</button>
  </div>
</template>

<script>
import SampleCat from "@/assets/SampleCat.jpg";
import soundClick from "@/assets/click.mp3";
import pushBtn from "@/assets/mainBtn.mp3";

export default {
  name: "HelloWorld",
  data() {
    return {
      picSrc: SampleCat,
      altText: "SampleCat",
      isMute: true,
    };
  },
  props: {
    msg: String,
  },
  methods: {
    async togglePic() {
      if (!this.isMute) {
        this.playSound(pushBtn, 0.2);
      }
      this.fetchPic("https://aws.random.cat/meow");
    },
    fetchPic(url) {
      fetch(url)
        .then((res) => res.json())
        .then((pic) => {
          if (pic?.file) {
            this.picSrc = pic.file;
          } else {
            this.picSrc = pic.url;
          }
        })
        .catch(() => this.fetchPic("https://random.dog/woof.json"));
    },
    toggleMute() {
      this.isMute = !this.isMute;
      this.playSound(soundClick, 0.05);
    },
    playSound(sound, vlm) {
      let click = new Audio(sound);
      click.volume = vlm;
      click.play();
    },
    testAndroidApi() {
      navigator.notification.confirm(
        `Проверка использования интерфейса Android`,
        () => {
          if (this.isMute) {
            this.toggleMute();
          }
        },
        "Включить звук ?",
        ["Подтвердить", "Отмена"]
      );
    },
  },
};
</script>

<style scoped lang="scss">
.app {
  position: relative;
  margin: 0 16px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  &_image {
    display: block;
    width: 100%;
    height: 240px;
    border: 1px solid rgb(157, 156, 156);
    margin-bottom: 72px;
    box-sizing: border-box;
  }
  &_btn {
    min-width: 200px;
    min-height: 200px;
    border-radius: 50%;
    font-size: 34px;
    font-weight: 900;
    color: #ffffff;
    outline: none;
    border: 0;
    transition: all 0.1s;
    background-color: rgb(237, 120, 120);
    box-shadow: 0 0 40px -5px black;
    &:hover {
      background-color: rgb(209, 154, 154);
    }
    &:active {
      background-color: rgb(189, 56, 56);
      box-shadow: 0 0 15px -2px black;
    }
  }
  &_muteBtn {
    position: absolute;
    right: 16px;
    bottom: -12px;
    width: 42px;
    height: 42px;
    border-radius: 50%;
    background-color: rgb(186, 186, 186);
    border: 0;
    font-weight: 900;
    color: #ffffff;
    box-shadow: 0 0 20px -2px black;
    display: flex;
    justify-content: center;
    align-items: center;
    &:active {
      transform: scale(1.2, 1.2);
      box-shadow: 0 0 5px 0 black;
    }
  }
  &_testBtn {
    position: absolute;
    left: 24px;
    bottom: -68px;
    width: 84px;
    height: 84px;
    background-color: rgb(125, 191, 134);
    border-radius: 50%;
    border: 0;
    font-weight: 900;
    color: #ffffff;
    box-shadow: 0 0 20px -2px black;
    display: flex;
    justify-content: center;
    align-items: center;
    &:active {
      transform: scale(1.2, 1.2);
      box-shadow: 0 0 5px 0 black;
      background-color: rgba(125, 191, 134, 0.605);
    }
  }
}
.unmute {
  background-color: rgb(125, 125, 191);
}

@media (max-height: 700px) {
  .app_upblock {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    margin-bottom: 4px;
  }
  .app_logo {
    width: 48px;
    height: 48px;
    margin-right: 16px;
  }
  .app_headtext {
    font-size: 18px;
  }
}
</style>
