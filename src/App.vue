<template>
  <div>
    <vue-swing @throwout="onThrowout"
                :config="config"
                ref="vueswing">
      <div class="card" v-for="(image, i) in images" :key="i">
        <img :src="getPic(image.imgUrl)" :alt="image.title" >
      </div>
    </vue-swing>
  </div>
</template>

<script>
  import VueSwing from 'vue-swing'
  import Data from './assets/data.json'

  export default {
    name: 'app',

    components: {
      VueSwing
    },

    data() {
      return {
        config: {
          allowedDirections: [
            VueSwing.Direction.UP,
            VueSwing.Direction.DOWN,
            VueSwing.Direction.LEFT,
            VueSwing.Direction.RIGHT
          ],
          minThrowOutDistance: 250,
          maxThrowOutDistance: 300
        },
        images: []
      }
    },

    methods: {
      remove() {
        this.swing();
        setTimeout(() => {
          this.cards.pop();
        }, 100);
      },

      swing() {
        const cards = this.$refs.vueswing.cards;
        cards[cards.length - 1].throwOut(
          Math.random() * 100 - 50,
          Math.random() * 100 - 50
        )
      },
      
      onThrowout({ target, throwDirection }) {
        target.setAttribute('style', 'opacity: 0');
      },
      
      getPic(val) {
          return require('./assets/images/'+val);
      },
    },
    created() {
      this.images = Data;
    }
  }
</script>

<style>

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    background-color: #444;
    margin: 0;
  }

  .card {
    width: 350px;
    height: 490px;
    position: absolute;
    max-width: 80vw;
    max-height: 80vh;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 10px solid #fff;
    margin-top: 100px;
    margin-left: 450px;
  }

  .card img {
    width: 100%;
    height: 223px;
  }
</style>
