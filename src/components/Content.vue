<template>
  <div
    id="content"
    :style="sidebarOpen ? { left: '260px' } : { left: '0', width: '100%' }"
  >
    <!-- <input
      type="text"
      v-model="inputValue"
      @keyup="keyEventHandler($event.key)"
    /> -->
    <div class="questionWrapper" v-for="q in questionData" :key="q.id">
      <div class="qWrap">
        <h1 class="questionKeyValue">{{ q.keyValue }}</h1>
        <h3 class="questionTitle">{{ q.title }}</h3>
      </div>

      <div class="answerWrapper" v-for="a in answerData" :key="a.id">
        <ul v-show="q.id === a.questionId">
          <li>
            <span class="aSpan">{{ a.answerKey }}</span>
            {{ a.answerTitle }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Content",
  data() {
    return {
      // audioTune: new Audio(),
      // inputValue: "",
      // questionKey: "",
      // questionKeyArray: [],
    };
  },
  props: ["sidebarOpen", "questionData", "answerData"],
  // mounted() {
  //   this.audioTune.load();
  //   this.questionKey = this.$el.querySelectorAll(".questionKeyValue");
  //   for (let index = 0; index < this.questionKey.length; index++) {
  //     const element = this.questionKey[index];
  //     this.questionKeyArray.push(element.textContent);
  //     console.log(element.textContent);
  //   }
  // },
  // methods: {
  //   playSound() {
  //     this.audioTune.pause();
  //     this.audioTune.currentTime = 0;
  //     this.audioTune.play();
  //   },
  //   keyEventHandler(e) {
  //     if (this.questionKeyArray.includes(this.inputValue.toUpperCase())) {
  //       this.audioTune.src = "/kathy/z01/z1.mp3";
  //       this.playSound();
  //       this.inputValue = "";
  //     }
  //     console.log(e);
  //   },
  // },
  // computed: {
  //   filterAnswers() {
  //     return "Hello from computed property..";
  //   },
  // },
};
</script>

<style scoped>
#content {
  position: relative;
  /* left: 260px; */
  transition: 0.3s left;
  padding: 5px 30px;
  width: calc(100% - 260px);
}

.questionWrapper {
  /* display: flex;
  align-items: baseline; */
  border-bottom: 1px solid rgba(0, 0, 0, 0.29);
  padding: 15px 0;
  color: #222c3c;
}

.qWrap {
  display: flex;
  align-items: baseline;
}

.questionKeyValue {
  font-size: 20px;
  margin: 0;
  padding-right: 15px;
  font-weight: 700;
}

.questionTitle {
  margin: 0;
  font-size: 16px;
}

.answerWrapper {
  display: flex;
  flex-direction: column;
}

.answerWrapper ul {
  margin: 0;
  padding-inline-start: 25px;
  padding-top: 15px;
}

.answerWrapper li {
  list-style: none;
  line-height: 15px;
}

.aSpan {
  font-weight: 700;
  margin-right: 15px;
}
</style>
