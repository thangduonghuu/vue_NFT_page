<script lang="ts">
import { defineComponent, ref } from "vue";
import heroImage1 from "../assets/image/heroSection-1.png";
import heroImage2 from "../assets/image/heroSection-2.png";
import heroImage3 from "../assets/image/heroSection-3.png";
import heroImage4 from "../assets/image/heroSection-4.png";

const container = ref<HTMLElement>();
const containerRight = ref<HTMLElement>();

export default defineComponent({
  data() {
    return {
      rotation: 0,
      textIndex: 0,
      ListImage: [
        {
          name: "hero-image-1",
          images: heroImage1,
          style: "--i:2",
        },
        {
          name: "hero-image-2",
          images: heroImage2,
          style: "--i:3",
        },
        {
          name: "hero-image-3",
          images: heroImage3,
          style: "--i:4",
        },
        {
          name: "hero-image-4",
          images: heroImage4,
          style: "--i:5",
        },
      ],
    };
  },
  methods: {
    rotateActive() {
      this.rotation += 90;
      if (this.container && container.value) {
        container.value.style.transform = `rotate(${this.rotation}deg)`;
      }
    },
    ActiveText() {
      const textList = Array.from(
        containerRight.value?.childNodes || []
      ) as HTMLElement[];

      for (let i = 0; i < textList.length; i++) {
        textList[i].classList.remove("active");
      }

      textList[this.textIndex]?.classList.add("active");

      if (this.textIndex == textList.length - 1) {
        this.textIndex = 0;
      } else {
        this.textIndex++;
      }
    },
  },
  mounted() {
    setInterval(() => {
      this.rotateActive();
    }, 3000);
    setInterval(() => {
      this.ActiveText();
    }, 2000);
  },

  setup() {
    return { container, containerRight };
  },
});
</script>

<template>
  <div class="flex justify-between items-cemter w-full h-full px-24">
    <div class="flex flex-col justify-center">
      <h1 class="header add-font">NFT</h1>
      <div class="container-right" ref="containerRight">
        <div class="add-color add-font">Orange</div>
        <div class="add-color add-font">Green</div>
        <div class="add-color add-font">Blue</div>
        <div class="add-color add-font">Purple</div>
      </div>
      <p class="description_coin">
        Fuape is a collection of 1000 funny ape NFTs - unique digital
        collectibles living on the Ethereum blockchain.
      </p>
      <div class="title">
        <span class="min-w-24"> Current Bid</span>
        <span> Bid Ends In </span>
      </div>
      <div class="title_description">
        <span class="min-w-24">Ξ 4.5 ETH</span>
        <span>10h:39m:41s</span>
      </div>
      <button
        @click="rotateActive"
        class="outline-0 border-solid border-2 p-3 rounded-lg mt-6 button-description pointer-events-auto"
      >
        Connect Wallet
      </button>
    </div>
    <div class="flex items-center justify-center container-left">
      <div class="container" ref="container">
        <div class="icon">
          <div
            class="imgBx"
            v-for="image in ListImage"
            :key="image.name"
            :style="image.style"
          >
            <img :src="image.images" alt="Hero Image" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.add-font {
  font-family: "Anton", sans-serif;
  font-weight: 700;
  font-style: italic;
  letter-spacing: 3px;
  font-optical-sizing: auto;
}
h1 {
  font-size: 150px;
  width: 300px;
  height: 150px;
  background: linear-gradient(to right, #ff3337, #f8ca53, #009a8f, #ffff);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
.add-color {
  width: 500px;
  font-size: 150px;
  height: 200px;
  display: none;
  background: #f8ca53;
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
  &.active {
    display: block;
    animation: textIn 0.5s ease-in;
  }
}
.description_coin {
  margin-top: 1rem;
  max-width: 350px;
}
.title {
  max-width: 250px;
  margin-top: 2rem;
  display: flex;
  gap: 2rem;
  font-size: 14px;
  /* justify-content: space-between; */
  opacity: 0.5;
}
.title_description {
  max-width: 250px;
  display: flex;
  font-size: 16px;
  gap: 2rem;
  /* justify-content: space-between; */
}
.button-description {
  width: 100%;
  max-width: 250px;
}
.container-left {
  transform: translateX(40%);
}
.container {
  position: relative;
  width: 1200px;
  height: 1200px;
  border: 2px solid #000;
  border-radius: 50%;
  transition: all 2s linear;
  /* animation: rotateActive 5s forwards; */
}
.container .icon {
  position: relative;
  width: 100%;
  height: 100%;
  left: -50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container .icon .imgBx {
  position: absolute;
  width: 540px;
  transition: 0.5s;
  height: 540px;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 0 0 4px #222, 0 0 0 6px #fff;
  transform: rotate(calc(360deg / 4 * var(--i)));
  transform-origin: 840px;
}

.container .icon .imgBx img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  /* transform: rotate(calc(-360deg / 4 * var(--i))); */
}

.container-right {
  position: relative;
  height: 200px;
  overflow: hidden;
}

@keyframes rotateActive {
  50% {
    transform: rotate(180deg);
  }
}

@keyframes textIn {
  0% {
    transform: translateY(100%);
  }
  100% {
    transform: translateY(0%);
  }
}
</style>
