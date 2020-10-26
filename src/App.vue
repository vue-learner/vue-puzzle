<template>  
  <HelloWorld msg="Hello Vue 3.0 + Vite" />
  <div class="container">
    <puzzle-board
      v-if="show"
      :autoResize="autoResize"
      :showNumber="showNumber"
      :cols="dimensions.x"
      :rows="dimensions.y"
      :src="src"
      :sources="sources"
      :animation="animation"
      :width="width"
      :height="height"
      @init="onPuzzleBoardInit"
      @start="onPuzzleBoardStart"
      @change="onPuzzleBoardChange"
      @finish="onPuzzleBoardFinish"
    />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import PuzzleBoard from "./components/PuzzleBoard.vue";
import penguinwebm from "./assets/penguin.webm";
import penguinmp4 from "./assets/penguin.mp4";
import catwebm from "./assets/cat.webm";
import catmp4 from "./assets/cat.mp4";
import dogjpg from "./assets/dog.jpg";

const SOURCEPATHS = {
  Dog: {
    src: dogjpg,
  },
  Cat: {
    sources: [
      {
        src: catwebm,
        type: "video/webm",
      },
      {
        src: catmp4,
        type: "video/mp4",
      },
    ],
  },
  Penguin: {
    sources: [
      {
        src: penguinwebm,
        type: "video/webm",
      },
      {
        src: penguinmp4,
        type: "video/mp4",
      },
    ],
  },
  Giphy: {},
};
const DIMENSIONS = {
  Easy: { x: 3, y: 3 },
  Normal: { x: 4, y: 4 },
  Difficult: { x: 5, y: 5 },
};
/* const getGiphySrc = async function () {
  const res = await fetch(
    "//api.giphy.com/v1/gifs/random?api_key=nZATgU4T4iauIJqCFu8rFvoCxCqBRwMt&rating=g&tag=cat"
  );
  const data = await res.json();
  const url = data.data.image_mp4_url;
  return [
    {
      src: url,
      type: "video/mp4",
    },
  ];
}; */

export default {
  name: "App",
  components: {
    HelloWorld,
    PuzzleBoard
  },
  data() {
    return {
      show: true,
      videoTitle: "Penguin",
      difficulty: "Easy",
      distance: null,
      isGoal: false,
      autoResize: true,
      width: 300,
      height: 300,
      showNumber: true,
      animation: true,
      sources: SOURCEPATHS["Penguin"].sources,
    };
  },
  created() {},
  computed: {
    src() {
      return SOURCEPATHS[this.videoTitle].src;
    },
    dimensions() {
      return DIMENSIONS[this.difficulty];
    },
  },
  watch: {
    isGoal(isGoal) {
      if (isGoal) {
        console.log('isGoal!!')
        // 插件暂不支持vue3
        // this.$confetti.start({
        //   shape: "rect",
        // });
      } else {
        // this.$confetti.stop();
      }
    },
  },
  methods: {    
    /* onMeowClick() {
      getGiphySrc().then((data) => {
        this.sources = data;
      });
    }, */
    onPuzzleBoardInit() {
      console.log("init");
      this.isGoal = false;
    },
    onPuzzleBoardStart() {
      console.log("start");
    },
    onPuzzleBoardFinish() {
      console.log("finish");
      this.isGoal = true;
    },
    onPuzzleBoardChange: function (payload) {
      console.log("change");
      this.distance = payload.distance;
    },
  },
};
</script>
<style>
html,
body {
  margin: 0;
  padding: 0;
  background-color: #fafafa;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}

.header {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  z-index: 2;
  font-size: 1.4em;
  position: absolute;
  width: 100%;
  height: 60px;
  color: #fafafa;
  background-color: #e91e63;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
}
.header-item {
  flex-grow: 0;
}
.title {
  width: 20%;
  padding: 0 5px;
  font-weight: bold;
  font-size: 0.8em;
}
.spacer {
  flex-grow: 1;
}
.meow {
  color: white;
  cursor: pointer;
  font-weight: bold;
  font-size: 1.2em;
}
.panel {
  width: 20%;
}
.container {
  position: absolute;
  top: calc(50% + 30px);
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.16), 0 2px 4px rgba(0, 0, 0, 0.23);
  width: 90%;
  height: calc(90% - 60px);
  margin: 0px;
  padding: 0px;
  z-index: 1;
  background-color: #ddd;
  max-width: 600px;
  max-height: 600px;
}
.repo {
  position: absolute;
  bottom: 5px;
  right: 5px;
}
</style>