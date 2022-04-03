<template>
  <div class="carousel">

    <div class="carousel__images">
      <img
          v-for="(image, index) in images"
          :key="index"
          :alt="image.altText"
          :src="require(`../assets/images/${image.src}.jpg`)"
          :style="{
            opacity : index === currentImageIndex ? 1 : 0
          }"
          class="carousel__image"
      >
    </div>

    <div class="carousel__progress-bar">
      <div :style="progressBarFill"
           class="carousel__progress-bar-box"></div>
      <div class="carousel__progress-bar-btn-prev" @click="selectPrevImage">
        <img alt="" src="../assets/images/arrow-left.svg"/>
      </div>
      <div class="carousel__progress-bar-counter">
        {{ currentImageIndex + 1 }} / {{ images.length }}
      </div>
      <div class="carousel__progress-bar-btn-next" @click="selectNextImage">
        <img alt="" src="../assets/images/arrow-right.svg"/>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: "ImageCarousel",

  data() {
    return {
      currentImageIndex: 0,
      timer: 0,
      animationDuration: 7000,
      images: [
        {
          src: '1920x1079',
          altText: 'Картинка 1',
        },
        {
          src: '1920x1081',
          altText: 'Картинка 2',
        },
        {
          src: '1920x1280',
          altText: 'Картинка 3',
        },
        {
          src: '2880x1654',
          altText: 'Картинка 4',
        },
        {
          src: '1920x868',
          altText: 'Картинка 5',
        },
      ],
    };
  },
  mounted() {
    this.startTimer();
  },
  computed: {
    progressBarFill() {
      return `width: ${this.timer / (this.animationDuration / 100)}%`;
    },
  },
  methods: {
    startTimer() {
      setInterval(() => {
        if (this.timer < this.animationDuration) {
          this.timer = this.timer + 10;
        } else {
          this.timer = 0;
          this.selectNextImage()
        }
      }, 10);
    },
    selectPrevImage() {
      if (this.currentImageIndex <= 0) {
        this.currentImageIndex = this.images.length - 1;
      } else {
        this.currentImageIndex--;
      }
      this.timer = 0;
    },
    selectNextImage() {
      if (this.currentImageIndex >= this.images.length - 1) {
        this.currentImageIndex = 0;
      } else {
        this.currentImageIndex++;
      }
      this.timer = 0;
    }
  }
};
</script>

<style lang="scss" scoped>

.carousel {
  width: 900px;
  height: 650px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 0 auto;
  overflow: hidden;

  &__images {
    width: 100%;
    height: 100%;
    position: relative;
    margin-bottom: 20px;
  }

  &__image {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    transition: all 0.4s ease-in;
    object-fit: cover;
  }

  &__progress-bar {
    max-width: 120px;
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 auto;
    color: #ffffff;
    background-color: #afb2b2;
    border-radius: 40px;
    overflow: hidden;
    z-index: 10;

    &-box {
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      display: block;
      background-color: #595b5b;
      z-index: -1;
    }

    &-btn-prev, &-btn-next {
      display: flex;
      align-items: center;
      padding: 8px 15px;
      cursor: pointer;
      z-index: 5;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;

      > img {
        height: 100%;
      }
    }

    &-counter {
      width: 40px;
      font-size: 18px;
      text-align: center;
      z-index: 5;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
    }
  }
}

</style>