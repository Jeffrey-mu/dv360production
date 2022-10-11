<template>
  <div class="creatives">
    <div class="creatives-view">
      <div class="borderSh">
        <el-tooltip class="item" effect="dark" :content="formText.dv + '_' + item.width + '/' + item.height"
          placement="top-start" v-for="item,index in sizeList" :key="index">
          <creativesItem v-bind="item" :formResources="formResources" :index="index" :formText="formText" />
        </el-tooltip>

      </div>
    </div>
    <div class="creatives-options border">
      <el-form label-position="top" label-width="80px" :model="formResources">
        <el-form-item label="下载全部图片">
          <el-button @click="download" size="small" :loading="loading" type="primary">下载全部图片</el-button>
        </el-form-item>
        <el-form-item label="上传icon">
          <!-- <el-input v-model="formResources.src"></el-input> -->
          <input type="file" @change="handleSuccess">
        </el-form-item>
        <el-form-item label="键值对">
          <el-input v-model="formText.dv" size="small"></el-input>
        </el-form-item>
        <el-form-item label="标题">
          <el-input v-model="formText.title" size="small"></el-input>
        </el-form-item>
        <el-form-item label="描述">
          <el-input v-model="formText.dis" size="small"></el-input>
        </el-form-item>
        <el-form-item label="字体">
          <el-select v-model="formText.typeface" class="m-2" placeholder="Select" size="small">
            <el-option v-for="item in fontFamily" :key="item.value" :label="item.label" :value="item.value" />
          </el-select>
        </el-form-item>
        <el-form-item label="按钮文字">
          <el-input v-model="formText.button" size="small"></el-input>
        </el-form-item>
        <el-form-item label="按钮颜色">
          <el-color-picker v-model="formText.bgColor" show-alpha></el-color-picker>
        </el-form-item>
        <el-form-item label="按钮文字颜色">
          <el-color-picker v-model="formText.color" show-alpha></el-color-picker>
        </el-form-item>
        <el-form-item label="背景颜色">
          <el-color-picker v-model="formResources.bgColor" show-alpha></el-color-picker>
        </el-form-item>
        <el-form-item label="主要颜色">
          <el-color-picker v-model="formResources.color" show-alpha></el-color-picker>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
import creativesItem from '../components/creativesItem.vue'
import html2canvas from 'html2canvas';
export default {
  components: {
    creativesItem
  },
  data() {
    return {
      loading: false,
      fileList: [],
      formResources: {
        src: '',
        bgColor: '',
        color: ''
      },
      formText: {
        title: 'Express',
        dis: 'ipad Air VS ipad Mini Which ipad Is The Best ?',
        button: 'Open',
        color: 'rgba(252, 252, 252, 1)',
        bgColor: 'rgba(4, 33, 247, 1)',
        typeface: "",
        dv: ''
      },
      sizeList: [
        {
          width: '320px', height: '320px', iconAlign: 'left'
        }, {
          width: '335px', height: '280px', iconAlign: 'left'
        }, {
          width: '300px', height: '250px', iconAlign: 'left'
        }, {
          width: '250px', height: '250px', iconAlign: 'left'
        }, {
          width: '250px', height: '280px', iconAlign: 'left'
        }, {
          width: '970px', height: '250px', iconAlign: 'left'
        }, {
          width: '970px', height: '90px', iconAlign: 'left', flexDirection: 'row'
        }, {
          width: '800px', height: '250px', iconAlign: 'left'
        }, {
          width: '728px', height: '90px', iconAlign: 'left', flexDirection: 'row'
        }, {
          width: '468px', height: '60px', iconAlign: 'left', showDis: false, flexDirection: 'row'
        }, {
          width: '320px', height: '100px', iconAlign: 'left', showDis: false, flexDirection: 'row'
        }, {
          width: '320px', height: '50px', iconAlign: 'left', showDis: false, flexDirection: 'row', titleFontSize: "20px"
        }, {
          width: '300px', height: '100px', iconAlign: 'left', showDis: false, flexDirection: 'row'
        }, {
          width: '300px', height: '50px', iconAlign: 'left', showDis: false, flexDirection: 'row', titleFontSize: "20px"
        }, {
          width: '300px', height: '1050px', iconAlign: 'left'
        }, {
          width: '375px', height: '667px', iconAlign: 'center'
        }, {
          width: '360px', height: '640px', iconAlign: 'center'
        }, {
          width: '300px', height: '600px', iconAlign: 'center'
        }, {
          width: '160px', height: '600px', iconAlign: 'center'
        }, {
          width: '120px', height: '600px', iconAlign: 'center', titleFontSize: "25px", disFontSize: "20px",
        }, {
          width: '360px', height: '592px', iconAlign: 'center'
        }, {
          width: '320px', height: '480px', iconAlign: 'center'
        }
      ],
      fontFamily: [{
        label: '华文细黑',
        value: 'STHeiti Light [STXihei]'
      },
      {
        label: '华文黑体',
        value: 'STHeiti'
      },
      {
        label: '华文宋体',
        value: 'STSong'
      },
      {
        label: '黑体',
        value: 'SimHei'
      },
      {
        label: '宋体',
        value: 'SimSun'
      },
      {
        label: '新宋体',
        value: 'NSimSun'
      },
      {
        label: '仿宋',
        value: 'FangSong'
      },
      {
        label: '楷体',
        value: 'KaiTi'
      },
      {
        label: '仿宋_GB2312',
        value: 'FangSong_GB2312'
      },
      {
        label: '楷体_GB2312',
        value: 'KaiTi_GB2312'
      },
      {
        label: '微软雅黑体',
        value: 'Microsoft YaHei'
      },
      { "label": "隶书", "value": "LiSu" }, { "label": "幼圆", "value": "YouYuan" }, { "label": "华文细黑", "value": "STXihei" }, { "label": "华文楷体", "value": "STKaiti" }, { "label": "华文中宋", "value": "STZhongsong" }, { "label": "华文仿宋", "value": "STFangsong" }, { "label": "方正舒体", "value": "FZShuTi" }, { "label": "方正姚体", "value": "FZYaoti" }, { "label": "华文彩云", "value": "STCaiyun" }, { "label": "华文琥珀", "value": "STHupo" }, { "label": "华文隶书", "value": "STLiti" }, { "label": "华文行楷", "value": "STXingkai" }, { "label": "华文新魏", "value": "STXinwei" }
      ]
    };
  },
  methods: {
    handleChange(val) {
      console.log(val);
    },
    download() {
      this.loading = true;
      let arr = []
      setTimeout(() => {
        this.sizeList.forEach((_, index) => {
          let id = '#' + 'creatives' + index
          arr.push(html2canvas(document.querySelector(id)))

        })
        Promise.all(arr).then((creatives) => {
          creatives.forEach((item, index) => {
            // 谷歌浏览器限制下载个数
            setTimeout(() => { this.downloadImg(item) }, index * 100)
          })
        })
          .finally(() => {
            this.loading = false;
          })
      }
        , 200)
    },
    downloadImg(item) {
      var url = item.toDataURL()
      var xhr = new XMLHttpRequest();
      xhr.open('GET', url, true); // 异步
      xhr.responseType = 'blob'; // blob 类型
      xhr.onload = () => {
        if (xhr.status != 200) {
          alert('下载异常！');
          return;
        }
        if (window.navigator.msSaveOrOpenBlob) {
          // IE
          navigator.msSaveBlob(xhr.response, this.formText.dv + '_' + item.width + '/' + item.height + '.png');
        } else {
          var newUrl = window.URL.createObjectURL(xhr.response);
          var a = document.createElement('a');
          a.setAttribute('href', newUrl);
          a.setAttribute('target', '_blank');
          a.setAttribute('download', this.formText.dv + '_' + item.width + '/' + item.height + '.png'); // 自定义文件名（有效）
          document.body.appendChild(a);
          a.click();
          document.body.removeChild(a);
        }
      };
      xhr.send();
    },
    handleSuccess(e) {
      const file = e.srcElement.files[0]
      const imgURL = window.URL.createObjectURL(file)
      this.formResources.src = imgURL
    }
  }
}
</script>
<style lang="scss">
body {
  margin: 0;
  padding: 0;
}

.creatives {
  display: flex;
  flex-direction: row;
  height: 100%;

  .creatives-view {
    flex: 1;
    overflow: auto;
  }

  .creatives-options {
    overflow: auto;
    width: 300px;

    .el-collapse-item__header {
      padding-left: 30px;
    }

    .el-form {
      padding: 20px;

      .el-form-item {
        margin: 0;
      }
    }
  }

  .border {
    border: 1px solid #ccc;
  }

  .borderSh {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    // justify-content: center;
    border-radius: 2px;

  }
}
</style>
