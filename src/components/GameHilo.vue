<template>
  <div class="hilo">
    <div class="hilo-button" @click="open" :class="{'hilo-button_disabled':isOpen}">
      Open
    </div>
    <div class="hilo-wrapper">
      <div class="hilo-show">
        <span>{{ prevNumber }}</span>
        <img class="hilo-sign" src="../assets/cross.svg" alt="cross">
      </div>
      <div class="hilo-options">
        <div class="hilo-options__item">
          <div class="hilo-options__item_front">
          </div>

        </div>
        <div class="hilo-deck">
          <div class="hilo-options__item" :class="{'hilo-options__item_opened':isOpen}">
            <div class="hilo-options__item_front">
            </div>

            <div class="hilo-options__item_back">
              <span>{{currentNumber}}</span>
              <img class="hilo-sign" src="../assets/cross.svg" alt="cross">
            </div>
          </div>
          <div class="hilo-options__item">
            <div class="hilo-options__item_front">
            </div>
          </div>
        </div>
        <div class="hilo-options__item">
          <div class="hilo-options__item_front">
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue";

const isOpen = ref(false)
const prevNumber = ref(12)
const currentNumber = ref()

let cards = ref()

onMounted(()=>{
  cards.value = document.querySelectorAll<HTMLElement>('.hilo-options__item_back, .hilo-options__item_front')
})

function open() {
  if(isOpen.value == false) {
    isOpen.value = true;

    currentNumber.value = Math.floor(Math.random() * 20)

    setTimeout(() => {
      cards.value.forEach((item:HTMLDivElement)=>{
        item.style.transitionDuration = '0s'
      })

      prevNumber.value = currentNumber.value
      isOpen.value = false;
    }, 2800);

    cards.value.forEach((item:HTMLDivElement)=>{
      item.style.transitionDuration = '.4s'
    })

  }
}
</script>

<style lang="scss">
.hilo {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: url("../assets/BG.png"), rgb(22, 26, 49);
  background-size: cover;

  &-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    gap: 20px;
  }

  &-button {
    color: #fff;
    font-family: sans-serif;
    font-size: 48px;
    padding: 10px 20px;
    background: #ffb700;
    border-radius: 20px;
    cursor: pointer;
    margin-bottom: 30px;
    @media (max-width: 1200px) {
      font-size: 28px;
    }
    &_disabled {
      opacity: .7;
    }
  }

  &-show {
    background: #fff;
    display: flex;
    flex-direction: column;
    align-items: start;
    font-size: 28px;
    font-family: sans-serif;
    font-weight: 600;
    padding: 10px;
    box-sizing: border-box;
    border-radius: 20px;
    @media (max-width: 576px) {
      font-size: 18px;
    }
  }
  &-sign {
    @media (max-width: 576px) {
      width: 25px;
    }
  }
  &-options {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin: 0 auto;
    &__item {
      position: relative;
      transition-duration: .4s;

      &:nth-child(2) {
        top: 0;
        position: absolute;
      }

      &:first-child {
        z-index: 1;
      }

      &_opened {
        animation-name: open-card;
        animation-fill-mode: forwards;
        animation-duration: 2s;
        animation-delay: .4s;

        .hilo-options__item_front {
          transform: perspective(600px) rotateY(-180deg);
        }

        .hilo-options__item_back {
          transform: perspective(600px) rotateY(0deg);
        }
      }

      &_front, &_back {
        height: 100%;
        width: 100%;
        transition: transform .4s linear;
        position: absolute;
        backface-visibility: hidden;
        overflow: hidden;
        border-radius: 20px;
        padding: 10px;
        box-sizing: border-box;
        @media (max-width: 576px) {
          border-radius: 10px;
        }
      }

      &_front {
        background: url("../assets/back.svg"), linear-gradient(180.00deg, rgb(48, 133, 232), rgb(22, 96, 182) 100%);
        transform: perspective(600px) rotateY(-360deg);
      }

      &_back {
        transform: perspective(600px) rotateY(-180deg);
        background: #fff;
        display: flex;
        flex-direction: column;
        align-items: start;
        font-size: 28px;
        font-family: sans-serif;
        font-weight: 600;
        @media (max-width: 576px) {
          font-size: 18px;
        }
      }
    }
  }

  &-deck {
    position: relative;
  }
}
.hilo-show, .hilo-options__item {
  width: 180px;
  height: 280px;
  @media (max-width: 1200px) {
    width: 129px;
    height: 200px;
  }
  @media (max-width: 576px) {
    width: 100px;
    height: 150px;
    border-radius: 10px;
  }
}
@keyframes open-card {
  25% {
    transform: scale(1.1);
  }
  50% {
    transform: scale(1.1) translateY(-100%);
  }
  100% {
    transform: scale(1) translateY(calc(-100% - 20px));
  }
}
</style>
