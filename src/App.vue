<template>
  <div class="container" @click.stop="turnOffModal">
    <div class="screen">
      <div class="image-cover-container">
        <img src="./assets/images/illustration-hero.svg" alt="" />
      </div>
      <div class="main">
        <h1>order summary</h1>
        <p class="quote">
          You can now listen to millions of songs, audiobooks, and podcasts on
          any devices, any where you like
        </p>
        <div class="payment-plan">
          <div class="logo">
            <img src="./assets/images/icon-music.svg" alt="" />
          </div>
          <div class="text">
            <p class="title">{{ planName }} plan</p>
            <p class="price">{{ planPrice }}$/year</p>
          </div>
          <button @click="handleClick">Change</button>
        </div>
        <button class="proceed" @click.stop="turnOnModal">
          Proceed to Payment
        </button>
        <button class="cancel">Cancel Payment</button>
        <div class="modal-container" v-if="this.proceed">
          <span class="modal" @click.stop="">Succeed!</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      planName: "anual",
      planPrice: null,
      currentOptionPosition: 0,
      proceed: false,
    };
  },

  computed: {
    planOptions() {
      return [
        { planName: "anual", planPrice: 8 },
        { planName: "pro", planPrice: 100 },
        { planName: "premium", planPrice: 1000 },
      ];
    },
  },
  created() {
    this.planName = this.planOptions[0].planName;
    this.planPrice = this.planOptions[0].planPrice;
  },

  methods: {
    handleClick() {
      console.log("hello");
      console.log(this.currentOptionPosition);
      this.currentOptionPosition++;
      if (this.currentOptionPosition >= this.planOptions.length) {
        this.currentOptionPosition = 0;
      }
    },
    turnOnModal() {
      this.proceed = true;
    },
    turnOffModal() {
      this.proceed = false;
    },
  },
  watch: {
    currentOptionPosition() {
      this.planName = this.planOptions[this.currentOptionPosition].planName;
      this.planPrice = this.planOptions[this.currentOptionPosition].planPrice;
    },
  },
};
</script>

<style lang="scss">
$text_color1: #748dbb;
$text_color2: #9babc0;

* {
  box-sizing: border-box;
}
button {
  cursor: pointer;
}
html {
  font-size: 14px;
  font-family: "Open Sans", sans-serif;
  color: $text_color2;
}
body {
  @media screen and (min-width: 768px) {
    background-image: url(./assets/images/pattern-background-desktop.svg);
    background-position: 0 0;
    background-repeat: no-repeat;
    background-size: 100% auto;
  }
  @media screen and (max-width: 768px) {
    background-color: #d5e0fe;
  }
}
.container {
  width: 100%;
  height: 100%;
}
.screen {
  width: 350px;
  margin: auto;
  background: white;
  box-shadow: 0 0 40px rgba(0, 0, 0, 0.158);
  border-radius: 15px;
  overflow: hidden;
  .image-cover-container {
    width: 100%;
    margin-bottom: 40px;
    img {
      width: 100%;
      max-width: 450px;
      height: auto;
    }
  }
  .main {
    margin: 0 10% 30px;
    h1 {
      text-align: center;
      text-transform: capitalize;
      font-weight: bold;
      font-size: 2rem;
      color: $text_color1;
      text-shadow: 0rem 0.25rem 0.25rem rgba($text_color1, 0.15);
    }
    p.quote {
      text-align: center;
    }
    .payment-plan {
      display: flex;
      align-items: center;
      justify-content: space-around;
      background: #f8f9fe;
      border-radius: 10px;
      font-size: 0.9rem;
      height: 80px;
      border: 1px solid #dfe3f538;
      div.text {
        width: 100px;
        p {
          margin: 0.2rem 0;
          text-transform: capitalize;
        }
        p.title {
          color: $text_color1;
          font-weight: bold;
        }
      }
      button {
        text-decoration: underline;
        border: none;
        background: none;
        color: $text_color1;
      }
    }
  }
  button.proceed {
    width: 100%;
    display: block;
    background: #382ae1;
    color: white;
    height: 40px;
    box-shadow: 0 18px 15px #4e41e21c;
    border: none;
    border-radius: 10px;
    margin: 25px 0;
    font-size: 0.9rem;
    font-weight: bold;
  }
  button.cancel {
    border: none;
    color: $text_color2;
    font-weight: bold;
    background: none;
    display: block;
    margin: auto;
  }
  .modal-container {
    position: fixed;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    background: rgba(128, 128, 128, 0.5);
    .modal {
      position: absolute;
      top: 40%;
      left: 36%;
      display: block;
      width: 200px;
      padding: 1rem;
      text-align: center;
      font-weight: bold;
      color: rgb(141, 140, 140);
      background: #ffe814;
      border-radius: 5px;
      animation: modalAnimation 0.3s linear;
      transform-origin: center;
      @keyframes modalAnimation {
        0% {
          transform: rotate(-20deg);
        }
        20% {
          transform: rotate(20deg);
        }
        40% {
          transform: rotate(-20deg);
        }
        60% {
          transform: rotate(20deg);
        }
        80% {
          transform: rotate(-20deg);
        }
        100% {
          transform: rotate(20deg);
        }
      }
    }
  }
}
</style>