<template>
  <div class="drumkit">
    <div class="keys">
      <div
        v-for="key in keys"
        :key="key.keyCode"
        :class="[key.isPlaying ? 'playing' : '', 'key']"
        @transitionend="removeTransition($event, key)"
      >
        <kbd>{{ key.keyName }}</kbd>
        <span class="sound">{{ key.soundName }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from "@vue/reactivity";
import { onMounted } from "vue";

export default {
  name: "Drumkit",
  setup() {
    const keys = reactive([
      {
        keyCode: 65,
        keyName: "A",
        soundName: "clap",
        audio: new Audio("../src/assets/sounds/clap.wav"),
        isPlaying: false,
      },
      {
        keyCode: 83,
        keyName: "S",
        soundName: "hihat",
        audio: new Audio("../src/assets/sounds/hihat.wav"),
        isPlaying: false,
      },
      {
        keyCode: 68,
        keyName: "D",
        soundName: "kick",
        audio: new Audio("../src/assets/sounds/kick.wav"),
        isPlaying: false,
      },
      {
        keyCode: 70,
        keyName: "F",
        soundName: "openhat",
        audio: new Audio("../src/assets/sounds/openhat.wav"),
        isPlaying: false,
      },
      {
        keyCode: 71,
        keyName: "G",
        soundName: "boom",
        audio: new Audio("../src/assets/sounds/boom.wav"),
        isPlaying: false,
      },
      {
        keyCode: 72,
        keyName: "H",
        soundName: "ride",
        audio: new Audio("../src/assets/sounds/ride.wav"),
        isPlaying: false,
      },
      {
        keyCode: 74,
        keyName: "J",
        soundName: "snare",
        audio: new Audio("../src/assets/sounds/snare.wav"),
        isPlaying: false,
      },
      {
        keyCode: 75,
        keyName: "K",
        soundName: "tom",
        audio: new Audio("../src/assets/sounds/tom.wav"),
        isPlaying: false,
      },
      {
        keyCode: 76,
        keyName: "L",
        soundName: "tink",
        audio: new Audio("../src/assets/sounds/tink.wav"),
        isPlaying: false,
      },
    ]);
    onMounted(() => {
      window.addEventListener("keydown", playSound);
    });

    const removeTransition = (e, key) => {
      if (e.propertyName !== "transform") {
        return;
      }
      key.isPlaying = false;
    };

    const playSound = (e) => {
      const key = keys.find((key) => {
        return key.keyCode === e.keyCode;
      });
      if (!key) {
        return;
      }

      key.audio.currentTime = 0;
      key.isPlaying = true;
      key.audio.play();
    };

    return {
      keys,
      removeTransition,
      playSound,
    };
  },
};
</script>

<style scoped>
.keys {
  display: flex;
  flex: 1;
  min-height: 100vh;
  align-items: center;
  justify-content: center;
}

.key {
  border: 0.4rem solid black;
  border-radius: 0.5rem;
  margin: 1rem;
  font-size: 1.5rem;
  padding: 1rem 0.5rem;
  transition: all 0.07s ease;
  width: 10rem;
  text-align: center;
  color: white;
  background: rgba(0, 0, 0, 0.4);
  text-shadow: 0 0 0.5rem black;
}

.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}

kbd {
  display: block;
  font-size: 4rem;
}

.sound {
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 0.1rem;
  color: #ffc600;
}
</style>