<template>
  <div :style="itemStyle" class="creatives-item" :id="'creatives' + index">
    <div class="img-box" :style="imgBoxStyle">
      <img :src="formResources.src || '/icon.png'" width="35px" height="35px" alt="">
    </div>
    <div class="text" v-if="showText" :style="textStyle">
      <div class="creatives-title" :style="textStyle.titleStyle">
        {{formText.title}}
      </div>
      <div class="dis" v-if="showDis" :style="textStyle.disStyle">
        {{formText.dis}}
      </div>
    </div>
    <div class="button" :style="buttonStyle">
      <el-button :style="buttonStyle.innerStyle" style="border: none; border-radius: 2px">{{formText.button}}
      </el-button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    index: {
      type: Number
    },
    width: {
      type: String,
    },
    height: {
      type: String,
    },
    iconAlign: {
      type: String
    },
    titleFontSize: {
      type: String
    },
    disFontSize: {
      type: String
    },
    flexDirection: {
      type: String,
      default: 'column'
    },
    showText: {
      type: Boolean,
      default: true
    },
    showDis: {
      type: Boolean,
      default: true
    },
    formResources: {
      type: Object,
    },
    formText: {
      type: Object
    }
  },
  computed: {
    itemStyle() {
      return { width: this.width, height: this.height, border: '1px solid #111', margin: '10px', flexDirection: this.flexDirection, backgroundColor: this.formResources.bgColor, flexShrink: 0 };
    },
    imgBoxStyle() {
      let imgStyle = {}
      if (this.flexDirection === 'row') {
        imgStyle = {
          display: 'flex',
          paddingLeft: '10px',
          justifyContent: 'center',
          flexDirection: 'column'
        }
      }
      return { textAlign: this.iconAlign, ...imgStyle };
    },
    buttonStyle() {
      let buttonStyle = {}
      if (this.flexDirection === 'row') {
        buttonStyle = {
          display: 'flex',
          paddingRight: '10px',
          justifyContent: 'center',
          flexDirection: 'column'
        }
      }
      return { textAlign: this.iconAlign, ...buttonStyle, innerStyle: { backgroundColor: this.formText.bgColor, color: this.formText.color } };
    },
    textStyle() {
      let textStyle = {}
      if (this.flexDirection === 'row') {
        textStyle = {
          display: 'flex',
          paddingLeft: '10px',
          justifyContent: 'center',
          flexDirection: 'column'
        }
      }
      return {
        color: this.formResources.color, fontFamily: this.formText.typeface, ...textStyle, titleStyle: {
          fontSize: this.titleFontSize,
        }, disStyle: {
          fontSize: this.disFontSize,
        }
      };
    }
  }
}
</script>
<style lang="scss">
.creatives-item {
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  text-align: center;

  .text {
    .creatives-title {
      font-size: 30px;
      font-weight: bold;
    }

    .dis {
      font-size: 20px;
    }
  }

  .button {
    display: flex;
    justify-content: center;
  }
}
</style>
