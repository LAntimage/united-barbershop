<template>
  <div id="app">
    <div class="barbershop">
      <div class="logotype">
        <div class="close" @click="closeWindow"></div>
      </div>
      <div class="content">
        <div class="items">
          <div v-for="(item, index) in items" :key="index" class="item">
            <div class="title"><span>{{ item.title }}</span></div>
            <div class="custom">
              <div class="variants">
                <div class="variant styles">
                  <button class="left" @click="switchStyle(index, -1)"></button>
                  <span>{{ item.styles[item.currentStyle].title }}</span>
                  <button class="right" @click="switchStyle(index, 1)"></button>
                </div>
                <div class="variant colors">
                  <button class="left" @click="switchColor(index, -1)"></button>
                  <span>{{ item.colors[item.currentColor].title }}</span>
                  <button class="right" @click="switchColor(index, 1)"></button>
                </div>
              </div>
              <div class="price">
                <span>Цена</span>
                <span>{{ item.price }}</span>
              </div>
            </div>
            <div class="methods">
              <button @click="buy('bank')">Оплатить картой</button>
              <button @click="buy('wallet')">Оплатить наличными</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="camera-controls">
      <div class="slider">
        <span>Поворот</span>
        <VueSlider v-model="camera.rotation.current" :min="camera.rotation.min" :max="camera.rotation.max" width="100%" :height="9" tooltip="none" :dotOptions="{focusStyle: {'box-shadow': 'none'}}" :dotSize="12" :dotStyle="{background:'#BDBDBD', border: 'unset'}" :railStyle="{background:'#585858'}" :processStyle="{background:'#fff'}" />
      </div>
      <div class="slider">
        <span>Высота</span>
        <VueSlider v-model="camera.height.current" :min="camera.height.min" :max="camera.height.max" width="100%" :height="9" tooltip="none" :dotOptions="{focusStyle: {'box-shadow': 'none'}}" :dotSize="12" :dotStyle="{background:'#BDBDBD', border: 'unset'}" :railStyle="{background:'#585858'}" :processStyle="{background:'#fff'}" />
      </div>
      <div class="slider">
        <span>Дальность</span>
        <VueSlider v-model="camera.range.current" :min="camera.range.min" :max="camera.range.max" width="100%" :height="9" tooltip="none" :dotOptions="{focusStyle: {'box-shadow': 'none'}}" :dotSize="12" :dotStyle="{background:'#BDBDBD', border: 'unset'}" :railStyle="{background:'#585858'}" :processStyle="{background:'#fff'}" />
      </div>
    </div>
  </div>
</template>

<script>
import VueSlider from "vue-slider-component"
import 'vue-slider-component/theme/antd.css'
export default {
  name: 'App',
  components: {
    VueSlider
  },
  data() {
    return {
      items: [
        {
          name: "hairstyle",
          title: "Прическа",
          price: 400,
          currentStyle: 0,
          currentColor: 0,
          styles: [
            { title: "Вариант #1" },
            { title: "Вариант #2" },
            { title: "Вариант #3" },
            { title: "Вариант #4" },
          ],
          colors: [
            { title: "Цвет #1" },
            { title: "Цвет #2" },
            { title: "Цвет #3" },
          ]
        }
      ],
      camera: {
        rotation: {
          min: 0,
          current: 0,
          max: 360
        },
        height: {
          min: 0,
          current: 50,
          max: 100,
        },
        range: {
          min: 0,
          current: 25,
          max: 100
        }
      }
    }
  },
  mounted() {
    // to remove
    // ТОЛЬКО ДЛЯ ТЕСТА
    for (let i = 0; i < 10; i++) {
      this.items.push(
          {
            name: "hairstyle",
            title: "Прическа",
            price: 400,
            currentStyle: 0,
            currentColor: 0,
            styles: [
              { title: "Вариант #1" },
              { title: "Вариант #2" },
              { title: "Вариант #3" },
              { title: "Вариант #4" },
            ],
            colors: [
              { title: "Цвет #1" },
              { title: "Цвет #2" },
              { title: "Цвет #3" },
            ]
          }
      )
    }
  },
  methods: {
    closeWindow() {
      // mp trigger здесь
    },
    buy(method) {
      switch(method) {
        case "wallet":
          // mp trigger покупка наличными
          break;
        case "bank":
          // mp trigger покупка картой
          break;
      }
    },
    switchStyle(index, forward) {
      let item = this.items[index]
      let min = 0
      let max = item.styles.length - 1
      if (forward < 0) {
        if (item.currentStyle + forward < min) {
          item.currentStyle = max
        } else {
          item.currentStyle += forward
        }
      } else {
        if (item.currentStyle + forward > max) {
          item.currentStyle = min
        } else {
          item.currentStyle += forward
        }
      }
    },
    switchColor(index, forward) {
      let item = this.items[index]
      let min = 0
      let max = item.colors.length - 1
      if (forward < 0) {
        if (item.currentColor + forward < min) {
          item.currentColor = max
        } else {
          item.currentColor += forward
        }
      } else {
        if (item.currentColor + forward > max) {
          item.currentColor = min
        } else {
          item.currentColor += forward
        }
      }
    }
  }
}
</script>

<style lang="scss">

@font-face {
  font-family: Montserrat-Regular;
  src: url("./assets/fonts/Montserrat-Regular.ttf");
}

@font-face {
  font-family: Montserrat-SemiBold;
  src: url("./assets/fonts/Montserrat-SemiBold.ttf");
}

button:active,
button:focus {
  outline: none;
}
button:active {
  filter: brightness(1.3);
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background-image: url("./assets/tmp-background.png");
}

.barbershop {
  display: flex;
  width: 354px;
  height: 710px;

  flex-direction: column;

  position: fixed;
  top: 50%;
  left: 32px;
  transform: translateY(-50%);

  & > .logotype {
    display: flex;
    width: 100%;
    height: 110px;

    background: #9020F9 url("./assets/svg/logotype.svg") no-repeat center 15px;

    border-radius: 12px 12px 0px 0px;

    position: relative;

    & > .close {
      display: block;
      width: 23px;
      height: 23px;

      background-image: url("./assets/svg/x-close.svg");
      background-position: center center;
      background-repeat: no-repeat;

      position: absolute;
      top: 3px;
      right: 4px;
    }
  }

  & > .content {
    display: flex;
    width: 100%;
    height: 600px;

    background-color: #fff;
    border-radius: 0px 0px 12px 12px;

    padding: 5px 4px 5px 9px;

    & > .items {
      display: grid;
      width: 100%;

      grid-template-columns: 330px;
      grid-auto-rows: 117px;
      grid-row-gap: 16px;

      overflow-y: auto;

      padding-right: 11px;

      & > .item {
        display: flex;
        width: 330px;

        flex-direction: column;

        background: #F5F5F5;
        border-radius: 6px;

        padding: 1px 17px 11px 10px;

        & > .title {
          display: flex;
          width: 100%;

          & > span {
            color: #000000;

            font-family: Montserrat-SemiBold, sans-serif;
            font-weight: 600;
            font-size: 16px;
          }
        }

        & > .custom {
          display: flex;
          width: 100%;

          justify-content: space-between;
          align-items: center;

          margin-top: 14px;

          & > .variants {
            display: flex;
            flex-direction: column;

            & > .variant {
              display: flex;
              width: 191px;
              height: 16px;

              justify-content: space-between;
              align-items: center;

              &:last-child {
                margin-top: 9px;
              }

              & > button {
                width: 16px;
                height: 16px;

                background-color: unset;
                background-image: url("./assets/svg/button-left.svg");
                background-position: center center;
                background-repeat: no-repeat;

                border: unset;

                &.right {
                  background-image: url("./assets/svg/button-right.svg");
                }
              }

              & > span {
                color: #000000;

                font-family: Montserrat-Regular, sans-serif;
                font-weight: normal;
                font-size: 13px;
              }
            }
          }

          & > .price {
            display: flex;
            flex-direction: column;

            & > span {
              color: #27AE60;

              font-family: Montserrat-Regular, sans-serif;
              font-weight: normal;
              font-size: 11px;

              &:last-child {
                font-family: Montserrat-SemiBold, sans-serif;
                font-weight: 600;
                font-size: 16px;
              }
            }
          }
        }

        & > .methods {
          display: flex;
          width: 252px;
          height: 16px;

          justify-content: space-between;

          margin-top: 14px;

          & > button {
            width: 119px;
            height: 16px;

            background: none;
            color: #27AE60;

            font-family: Montserrat-Regular, sans-serif;
            font-weight: normal;
            font-size: 8px;

            border: 0.5px solid #27AE60;
            border-radius: 25px;
          }
        }
      }
    }
  }
}

.camera-controls {
  display: grid;
  width: 371px;
  height: 140px;

  grid-template-columns: 348px;
  grid-template-rows: repeat(3, 32px);
  grid-row-gap: 11px;

  background: rgba(130, 130, 130, 0.74);
  border-radius: 10px;

  padding: 11px 11px 0 12px;

  position: fixed;
  right: 24px;
  bottom: 20px;

  & > .slider {
    display: flex;
    flex-direction: column;
    align-items: center;

    & > span {
      color: #fff;

      font-family: Montserrat-SemiBold, sans-serif;
      font-weight: 600;
      font-size: 12px;
    }
  }
}

::-webkit-scrollbar {
  width: 6px;
}

/* Track */
::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.6);
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #DFDFDF;
  border-radius: 36px;
}

</style>
