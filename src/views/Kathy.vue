<template>
  <div class="kathy">
    <Header
      v-bind:sidebarOpen="sidebarOpen"
      v-on:collapseSidebar="toggleSidebar"
    />
    <Content
      v-bind:sidebarOpen="sidebarOpen"
      v-bind:questionData="questionData"
      v-bind:answerData="answerData"
    />
    <audio controls id="music" controlsList="nodownload">
      <source v-if="song" type="audio/mpeg" :src="song" />
    </audio>
    <Sidebar
      v-bind:sidebarOpen="sidebarOpen"
      v-bind:sidebarData="sidebarData"
      v-on:keyEventHandler="keyEvent"
      v-model="content"
    />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Content from "@/components/Content.vue";
import Sidebar from "@/components/Sidebar.vue";

import sidebarData from "@/data/sidebarData.js";
import questionData from "@/data/questionData.js";
import answerData from "@/data/answerData.js";
import zKeys from "@/data/zKeys.js";

import z1 from "@/assets/kathy/z01/z1.mp3";
import z1_1 from "@/assets/kathy/z01/z1-1.mp3";
import z1_3 from "@/assets/kathy/z01/z1-3.mp3";
import z1_4 from "@/assets/kathy/z01/z1-4.mp3";

import z2 from "@/assets/kathy/z02/z2.mp3";
import z2_3 from "@/assets/kathy/z02/z2-3.mp3";

import z3 from "@/assets/kathy/z03/z3.mp3";
import z3_3 from "@/assets/kathy/z03/z3-3.mp3";

import z4 from "@/assets/kathy/z04/z4.mp3";
import z4_3 from "@/assets/kathy/z04/z4-3.mp3";

import z5 from "@/assets/kathy/z05/z5.mp3";
import z5_1 from "@/assets/kathy/z05/z5-1.mp3";

import t1 from "@/assets/kathy/rebuttals/t1.mp3";

import cKey from "@/assets/kathy/c.mp3";
import eKey from "@/assets/kathy/e.mp3";
import xKey from "@/assets/kathy/x.mp3";
import sKey from "@/assets/kathy/s.mp3";

export default {
  name: "Kathy",
  components: {
    Header,
    Content,
    Sidebar,
  },
  data() {
    return {
      // content sidebar da ki input un value su
      content: "",
      sidebarOpen: true,
      sidebarData,
      questionData,
      answerData,
      zKeys,
      player: "",
      song: "",
      currentMainCommand: "",
      currentSubCommand: "",
    };
  },
  mounted() {
    this.player = this.$el.querySelector("#music");
  },
  methods: {
    toggleSidebar() {
      this.sidebarOpen = !this.sidebarOpen;
    },
    playSound(soundUrl) {
      if (soundUrl.toLowerCase() == "z1") this.song = z1;
      if (soundUrl.toLowerCase() == "z1-1") this.song = z1_1;
      if (soundUrl.toLowerCase() == "z1-3") this.song = z1_3;
      if (soundUrl.toLowerCase() == "z1-4") this.song = z1_4;

      if (soundUrl.toLowerCase() == "z2") this.song = z2;
      if (soundUrl.toLowerCase() == "z2-3") this.song = z2_3;

      if (soundUrl.toLowerCase() == "z3") this.song = z3;
      if (soundUrl.toLowerCase() == "z3-3") this.song = z3_3;

      if (soundUrl.toLowerCase() == "z4") this.song = z4;
      if (soundUrl.toLowerCase() == "z4-3") this.song = z4_3;

      if (soundUrl.toLowerCase() == "z5") this.song = z5;
      if (soundUrl.toLowerCase() == "z5-1") this.song = z5_1;

      if (soundUrl.toLowerCase() == "t1") this.song = t1;

      if (soundUrl.toLowerCase() == "c") this.song = cKey;
      if (soundUrl.toLowerCase() == "e") this.song = eKey;
      if (soundUrl.toLowerCase() == "x") this.song = xKey;
      if (soundUrl.toLowerCase() == "s") this.song = sKey;

      this.player.pause();
      this.player.load();
      this.player.play();
      this.content = "";
    },
    stopSound() {
      this.player.pause();
      this.player.currentTime = 0;
    },
    keyEvent(e) {
      if (this.content.startsWith("0") && this.content.length == 1) {
        this.currentMainCommand = "z1";
        this.playSound(this.currentMainCommand);
      }

      // z1 ;
      if (
        this.content.toLowerCase().startsWith("z") &&
        this.zKeys.includes(this.content.toLowerCase())
      ) {
        if (this.content.length == 2) {
          this.currentMainCommand = this.content.toLowerCase();
          this.playSound(this.currentMainCommand);
        }
      } else if (
        !this.content.startsWith("z") ||
        (!this.content.startsWith("Z") && this.content.length > 0)
      ) {
        if (this.currentMainCommand == "z1" && this.content == "1") {
          this.playSound("z1-1");

          setTimeout(() => {
            this.playSound("z2");
          }, 1500);

          this.currentMainCommand = "z2";
        } else if (this.currentMainCommand == "z1" && this.content == "3") {
          this.playSound("z1-3");
        } else if (this.currentMainCommand == "z1" && this.content == "4") {
          this.playSound("z1-4");

          setTimeout(() => {
            this.playSound("z2");
          }, 1800);

          this.currentMainCommand = "z2";
        } else {
          setTimeout(() => {
            this.content = "";
          }, 1200);
        }
      } else {
        setTimeout(() => {
          this.content = "";
        }, 1200);
      }

      // if press 1 on z2 play z3;
      if (this.currentMainCommand == "z2" && this.content == "1") {
        this.playSound("z3");
        this.currentMainCommand = "z3";
      }

      // if press 3 on z2 play z2-3
      if (this.currentMainCommand == "z2" && this.content == "3") {
        this.playSound("z2-3");
      }

      // if press 4 on z2 plat t1 rebuttal;
      if (this.currentMainCommand == "z2" && this.content == "4") {
        this.playSound("t1");
      }

      // z3 de iken 1 e basılırsa z4 çalınacak ve currentMainCommand z4 e eşitlenecek
      if (this.currentMainCommand == "z3" && this.content == "1") {
        this.playSound("z4");
        this.currentMainCommand = "z4";
      }

      // if press 3 on z3 play z3-3
      if (this.currentMainCommand == "z3" && this.content == "3") {
        this.playSound("z3-3");
      }

      // if press 4 on z3 play t1 rebuttal;
      if (this.currentMainCommand == "z3" && this.content == "4") {
        this.playSound("t1");
      }

      // z4 de iken 1 e basılırsa z5 çalınacak ve currentMainCommand z5 e eşitlenecek
      if (this.currentMainCommand == "z4" && this.content == "1") {
        this.playSound("z5");
        this.currentMainCommand = "z5";
      }

      // if press 3 on z4 play z4-3
      if (this.currentMainCommand == "z4" && this.content == "3") {
        this.playSound("z4-3");
      }

      // if press 4 on z4 play t1 rebuttal;
      if (this.currentMainCommand == "z4" && this.content == "4") {
        this.playSound("t1");
      }

      // z5 te iken 1 e basıldığında;
      if (this.currentMainCommand == "z5" && this.content == "1") {
        this.playSound("z5-1");
      }

      // Rebuttals;
      // t1;
      if (this.content.toLowerCase() == "t1") {
        this.playSound("t1");
      }

      // Hotkeys;
      // 9 stop recording;
      if (
        this.content.toLowerCase().startsWith("9") &&
        this.content.length == 1
      ) {
        this.currentMainCommand = "";
        this.stopSound();
      }

      // x thanks bye;
      if (
        this.content.toLowerCase().startsWith("x") &&
        this.content.length == 1
      ) {
        this.playSound("x");
      }

      // c cant hear;
      if (
        this.content.toLowerCase().startsWith("c") &&
        this.content.length == 1
      ) {
        this.playSound("c");
      }

      // e;
      if (
        this.content.toLowerCase().startsWith("e") &&
        this.content.length == 1
      ) {
        this.playSound("e");
      }

      // s;
      if (
        this.content.toLowerCase().startsWith("s") &&
        this.content.length == 1
      ) {
        this.playSound("s");
      }

      console.log(e);
    },
  },
};
</script>

<style scoped>
#music {
  display: none;
}
</style>
