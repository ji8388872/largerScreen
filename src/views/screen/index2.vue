<template>
  <div id="app">
    <header>
      <img class="caiqi" src="@/assets/images/彩旗.png" alt="">
      <div class="title"><img class="title" src="@/assets/screem/titel.png" alt=""></div>
      <div class="time-day">
        <div class="time">
          <span>{{ today1 }}</span>
          {{ today }}
        </div>
        <div class="day">{{ currentTime }}</div>
      </div>
      <span class="iconfont icon-tuichu2" @click="back"></span>
    </header>
    <nav>
      <div class="container">
        <div class="row">
          <div class="col-md-4 col-sm-4 left">
            <div class="leftTop">
              <div class="photo">
                <img class="title" src="@/assets/images/生态园title.png" alt="">
                <el-carousel :interval="4000" class="elCarousel" @change="handleCarouselChange">
                  <el-carousel-item v-for="item in images" :key="item.id">
                    <div class="image-container">
                      <!-- 显示图片 -->
                      <img class="centered-img" :src="item.url" :title="item.title" @dblclick="showImage(item.url)"/>
                      <!-- 直接显示图片的标题和描述 -->
                      <div class="image-info">
                        <h3>{{ item.title }}</h3>
                      </div>
                    </div>

                  </el-carousel-item>
                </el-carousel>
              </div>
              <div class="shengtai">
                <div class="shengtai-info">
                  <p style="color: white;margin-left: 10px;font-size: 18px;font-weight: 700">{{
                      currentDescription
                    }}</p>
                </div>
              </div>
            </div>
            <div class="leftBottom">
              <div class="answer">
                <div style="font-weight: 600;letter-spacing: -1px;">{{
                    averageData.averageAccuracy
                  }} %
                </div>
                <div style="font-weight: 500;">平均正确率</div>
              </div>
              <div class="zhengque">
                <div style="padding-right: 2rem;">对 {{ averageData.correctCount }} 题</div>
                <div>错 {{ averageData.wrongCount}} 题</div>
              </div>
              <div class="icon1">
                <!--                <img src="@/assets/images/duicuo.png" alt="">-->
                <div style="font-size: 2rem; margin-top: 10px ;letter-spacing: 2px">答题总数</div>
              </div>
            </div>
          </div>
          <div class="col-md-4 col-sm-4">
            <div class="center">
              <div class="img1" @click="dialogVisible3 = true">
                <img src="@/assets/images/纯化1.png" style="cursor: pointer;" alt="">
              </div>
              <div class="img2" @click="dialogVisible1 = true">
                <img src="@/assets/images/价值再生1.png" style="cursor: pointer;" alt="">
              </div>
              <div class="img3" @click="dialogVisible2 = true">
                <img src="@/assets/images/转化1.png" style="cursor: pointer;" alt="">
              </div>
              <div class="img4" @click="dialogVisible4 = true">
                <img src="@/assets/screem/schoolBtn.png" style="cursor: pointer;" alt="">
              </div>
            </div>
          </div>
          <div class="col-md-4 col-sm-4">
            <div class="right">
              <!-- 临时填写数据表 -->
<!--              <div @click="dialogVisibleTemporary = true"-->
<!--                   style="color:#119441;margin-left: 10px;font-size: 20px;background-color: #ffffff;width: 140px;border-radius: 1.1rem"-->
<!--              >临时填写信息表-->
<!--              </div>-->
              <div class="rightTop">
                <div class="detail">
                  <span class="name">大卫虻宝</span> 我是一小大卫，我没有病菌，我的胃口很大，爱吃厨余垃圾，我已经吃了<span>{{ Number(dataListDWMB.total).toFixed(2) }}t</span>的厨余垃圾了！
                </div>
                <div class="detail1">
                  今天吃了<span>{{ dataListDWMB && dataListDWMB.cll ? Number(dataListDWMB.cll).toFixed(2) : 'null' }} Kg</span>“食物”，<br>
                  不停的吃了6天，<br>
                  我就能长大6000倍。
                </div>
                <div class="detail2">
                  虻宝变身<span>{{ dataListDWMB && dataListDWMB.cll ? Number(dataListDWMB.lczl).toFixed(2) : 'null'  }}Kg</span>“蛋白饲料”<br>
                  动物们吃的很香！
                </div>
                <div class="detail3">
                  虫粪变身<span>{{dataListDWMB && dataListDWMB.cll ? Number(dataListDWMB.cszl).toFixed(2) : 'null'}}Kg</span>“营养土”，<br>
                  瓜果蔬菜营养又好吃！
                </div>
              </div>
              <div class="rightBot">
                <div class="chengguo">
                  累计排放量<span>{{
                    (Number(dataListDWMB.total) *
                      0.79).toFixed(2)
                  }}</span>(tCO2e)<br>
                  累计种植树<span>{{
                    ((Number(dataListDWMB.total) * 0.79) * 0.88).toFixed(2)
                  }}</span>棵<br>
                  今日总参观人数<span>{{
                    dataListDWMB && dataListDWMB.cll ? Math.floor(Number(dataListDWMB.cgrs).toFixed(2)) : 'null'
                  }}</span>人
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>
    </nav>
    <div style="text-align: center; position: relative;">
      <el-dialog title="价值再生" :visible.sync="dialogVisible1" width="70%"
                 style="margin-top: -6%; vertical-align:middle;"
      >
        <span style="height: 30rem;padding: 0.2rem;">
          <price></price>
        </span>
      </el-dialog>
      <el-dialog title="转化—废弃物资源化处理" :visible.sync="dialogVisible2" width="70%" style="margin-top: -3%;">
        <div class="zhuanhuanImg">
          <el-carousel height="60rem" direction="vertical" :autoplay="true">
            <el-carousel-item v-for="(item, i) in zhuanhuaImgs" :key="i">
              <img :src="item.url" alt="" style="width: 100%;padding: 0.5rem;height: 100%;">
            </el-carousel-item>
          </el-carousel>
        </div>
      </el-dialog>
      <el-dialog title="纯化—垃圾分类全覆盖体系" :visible.sync="dialogVisible3" width="70%"
                 style="margin-top: -3%;overflow: hidden;"
      >
        <el-carousel height="60rem" direction="vertical" :autoplay="true">
          <el-carousel-item v-for="(item, i) in chunhuaImgs" :key="i">
            <img :src="item.url" alt="" style="width: 100%;padding: 0.5rem;height: 100%;">
          </el-carousel-item>
        </el-carousel>
      </el-dialog>

      <el-dialog title="答题小游戏" :visible.sync="dialogVisible4" width="50%" @close="dialogVisible4 = false"
                 style="margin-top: 10%;"
      >
        <ChoiceGames2 v-if="dialogVisible4"></ChoiceGames2>
        <!-- <qq></qq> -->

      </el-dialog>
      <el-dialog :visible.sync="dialogVisible" width="50%">
        <img :src="currentImageUrl" alt="" style="width: 100%;height: 50rem;"/>
      </el-dialog>


      <!--      填写临时表单数据-->
      <el-dialog
        title="临时信息填写"
        :visible.sync="dialogVisibleTemporary"
        width="30%"
        @close="closeTemporary"
      >
        <el-form :rules="DMSDataTempRules" ref="DMSDataTempRef" :model="DMSDataTemp">
          <el-form-item label="检查日期:" prop="rq" >
            <el-date-picker clearable
                            v-model="DMSDataTemp.rq"
                            type="date"
                            value-format="yyyy-MM-dd"
                            placeholder="请选择日期">
            </el-date-picker>
          </el-form-item>
          <el-form-item label="处理量:" prop="cll">
            <el-input v-model="DMSDataTemp.cll" placeholder="请输入今日处理量"></el-input>
          </el-form-item>
          <el-form-item label="老虫重量:" prop="lctz">
            <el-input v-model="DMSDataTemp.lctz" placeholder="请输入今日老虫重量"></el-input>
          </el-form-item>
          <el-form-item label="虫沙重量:" prop="cszl">
            <el-input v-model="DMSDataTemp.cszl" placeholder="请输入进日虫沙重量"></el-input>
          </el-form-item>
          <el-form-item label="参观人数:" prop="wbrs">
            <el-input v-model="DMSDataTemp.wbrs" placeholder="请输今日参观人数"></el-input>
          </el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisibleTemporary = false">取 消</el-button>
    <el-button type="primary" @click="updateTemporary">确 定</el-button>
  </span>
      </el-dialog>

    </div>
  </div>

</template>
<script>
import ChoiceGames2 from '@/views/screen/newVue/choiceGames2.vue'
import qq from '@/views/screen/newVue/1.vue'
import price from './newVue/test/price2.vue'
import bus from '@/utils/evenBus.js'
import { getResultList } from '@/api/screen/result.js'
import { getRankList } from '@/api/screen/ranking.js'
import { getTableTopList } from '@/api/screen/tableTop.js'
import { mapState } from 'vuex'
import { addOperationLogApi, getCorrectRateApi,getTemporaryApi } from '@/api/screen/operationLog'

export default {
  name: '',
  data() {
    return {
      dataListDWMB:{},
      questionData:{
        correctCount: 0,
        wrongCount: 0
      },
      // 左下角正确率数据
      averageAccuracyData:{
        correctCount: 0,
        wrongCount: 0,
        averageAccuracy: 0
      },
      // 临时表
      DMSDataTemp:{
        rq:'',
        cll:'',
        lctz:'',
        cszl:'',
        wbrs:''
      },
      // 临时数据验证
      DMSDataTempRules:{
        rq: [
          { required: true, message: '请选择日期', trigger: 'blur' }
        ],
        cll: [
          { required: true, message: '请输入今日处理量', trigger: 'blur' }
        ],
        lctz: [
          { required: true, message: '请输入今日老虫重量', trigger: 'blur' }
        ],
        cszl: [
          { required: true, message: '请输入今日虫沙重量', trigger: 'blur' }
        ],
        wbrs: [
          { required: true, message: '请输入今日参观人数', trigger: 'blur' }
        ]
      },
      // 临时数据框
      dialogVisibleTemporary:false,
      currentIndex: 0, // 记录当前轮播图的索引
      currentDescription: '', // 当前显示的 description
      tableData: [],
      currentTime: '',
      today: '',
      today1: '',

      Choice: {},
      allBj: [],
      BjdialogVisible: false,
      tableData1: [],
      fRank: '',//前三名准确率
      sRank: '',
      tRank: '',
      currentImageUrl: '',
      dialogVisible: false,

      dialogVisible1: false,
      dialogVisible2: false,
      dialogVisible3: false,
      dialogVisible4: false,

      chunhuaImgs: [

        {
          url: require('@/assets/images/chunhua1.png')
        },
        {
          url: require('@/assets/images/chunhua2.png')
        },
        {
          url: require('@/assets/images/chunhua3.png')
        },
        {
          url: require('@/assets/images/chunhua4.png')
        },
        {
          url: require('@/assets/images/chunhua5.png')
        },
        {
          url: require('@/assets/images/chunhua6.png')
        },
        {
          url: require('@/assets/images/chunhua7.png')
        }
      ],
      zhuanhuaImgs: [
        {
          url: require('@/assets/images/zhuanhua1.png')
        },
        {
          url: require('@/assets/images/zhuanhua.png')
        },
        {
          url: require('@/assets/images/zhuanhua2.png')
        },
        {
          url: require('@/assets/images/zhuanhua3.png')
        },
        {
          url: require('@/assets/images/zhuanhua4.png')
        },
        {
          url: require('@/assets/images/zhuanhua5.png')
        }
      ],
      images: [{ id: 1, url: require('@/assets/screem/1.jpg'), title: '万思接待～新航教育机构20人左右参观黑水虻站' },
        { id: 2, url: require('@/assets/screem/2.jpg'), title: '基金会接待～梅沙街道办一行25人参观黑水虻站' },
        { id: 3, url: require('@/assets/screem/3.jpg'), title: '基金会接待～梅沙街道办一行25人参观黑水虻站' },
        { id: 4, url: require('@/assets/screem/4.jpg'), title: '基金会接待～梅沙街道办一行25人参观黑水虻站' },
        {
          id: 5,
          url: require('@/assets/screem/5.jpg'),
          title: '基金会接待～香港中联办新界工作部带领香港北区社区代表考察（60人）参访黑水虻站\n' +
            '主接待：区焕仪\n' +
            '讲解：钟嘉玲'
        },
        {
          id: 6,
          url: require('@/assets/screem/6.jpg'),
          title: '基金会接待～香港中联办新界工作部带领香港北区社区代表考察（60人）参访黑水虻站\n' +
            '主接待：区焕仪\n' +
            '讲解：钟嘉玲'
        },
        {
          id: 7, url: require('@/assets/screem/7.jpg'), title: '深石接待\n' +
            '来访单位：保藤国际\n' +
            '来访人数：2人\n' +
            '主接待：高凌文\n'
        },
        { id: 8, url: require('@/assets/screem/8.jpg'), title: '万思张总陪同客户2人参观黑水虻站' },
        { id: 9, url: require('@/assets/screem/9.jpg'), title: '万思张总陪同客户2人参观黑水虻站' },
        { id: 10, url: require('@/assets/screem/10.jpg'), title: '基金会接待-梅沙街道办一行6人参观黑水虻站' },
        { id: 11, url: require('@/assets/screem/11.jpg'), title: '' },
        { id: 12, url: require('@/assets/screem/12.jpg'), title: '' }],
      // 最新信息图片
      images1: [
        { id: 1, url: require('@/assets/screem/1.jpg'), title: '万思接待～新航教育机构20人左右参观黑水虻站' },
        { id: 2, url: require('@/assets/screem/2.jpg'), title: '基金会接待～梅沙街道办一行25人参观黑水虻站' },
        { id: 3, url: require('@/assets/screem/3.jpg'), title: '基金会接待～梅沙街道办一行25人参观黑水虻站' },
        { id: 4, url: require('@/assets/screem/4.jpg'), title: '基金会接待～梅沙街道办一行25人参观黑水虻站' },
        {
          id: 5,
          url: require('@/assets/screem/5.jpg'),
          title: '基金会接待～香港中联办新界工作部带领香港北区社区代表考察（60人）参访黑水虻站\n' +
            '主接待：区焕仪\n' +
            '讲解：钟嘉玲'
        },
        {
          id: 6,
          url: require('@/assets/screem/6.jpg'),
          title: '基金会接待～香港中联办新界工作部带领香港北区社区代表考察（60人）参访黑水虻站\n' +
            '主接待：区焕仪\n' +
            '讲解：钟嘉玲'
        },
        {
          id: 7, url: require('@/assets/screem/7.jpg'), title: '深石接待\n' +
            '来访单位：保藤国际\n' +
            '来访人数：2人\n' +
            '主接待：高凌文\n'
        },
        { id: 8, url: require('@/assets/screem/8.jpg'), title: '万思张总陪同客户2人参观黑水虻站' },
        { id: 9, url: require('@/assets/screem/9.jpg'), title: '万思张总陪同客户2人参观黑水虻站' },
        { id: 10, url: require('@/assets/screem/10.jpg'), title: '基金会接待-梅沙街道办一行6人参观黑水虻站' },
        { id: 11, url: require('@/assets/screem/11.jpg'), title: '展示区1' },
        { id: 12, url: require('@/assets/screem/12.jpg'), title: '展示区2' }

      ],
      // 活动瞬间图片
      images2: [
        { id: 1, url: require('@/assets/images/hd1.png') },
        { id: 2, url: require('@/assets/images/hd2.png') },
        { id: 3, url: require('@/assets/images/hd3.png') },
        { id: 4, url: require('@/assets/images/hd4.png') },
        { id: 5, url: require('@/assets/images/hd5.png') },
        { id: 6, url: require('@/assets/images/hd6.png') },
        { id: 7, url: require('@/assets/images/hd7.png') }

      ],
      // 随手小记图片
      images3: [
        { id: 1, url: require('@/assets/images/ss1.png') },
        { id: 2, url: require('@/assets/images/ss2.png') },
        { id: 3, url: require('@/assets/images/ss3.png') },
        { id: 4, url: require('@/assets/images/ss4.png') },
        { id: 5, url: require('@/assets/images/ss5.png') },
        { id: 6, url: require('@/assets/images/ss6.png') },
        { id: 7, url: require('@/assets/images/ss7.png') },
        { id: 8, url: require('@/assets/images/ss8.png') },
        { id: 9, url: require('@/assets/images/ss9.png') },
        { id: 10, url: require('@/assets/images/ss10.png') },
        { id: 11, url: require('@/assets/images/ss11.png') }

      ]
    }
  },
  components: {
    ChoiceGames2,
    qq,
    price

  },
  created() {
    this.getDataListDWMB()
    // this.getRank()
    this.getChoice()
    // 初始化当前显示的 description
    this.currentDescription = this.images[this.currentIndex].title
    this.$store.dispatch('screen/getDMSDataStore')
  },
  mounted() {
    // 获取平均正确率数据
    // this.getRightRate()
    this.$store.dispatch('screen/getAverageDataStore',{correctCount: this.questionData.correctCount,
      wrongCount: this.questionData.wrongCount})

    this.getData()
    this.updateTime()
    setInterval(this.updateTime, 1000) // 每秒钟更新一次时间
    this.getDayOfWeek()
    setInterval(this.getDayOfWeek, 10000)
    this.images = this.images1

    bus.$on('updateGame', (val) => {
      this.Choice = val
    })
  },
  methods: {
    //大卫忙宝查询临时表数据
   async getDataListDWMB(){
     const res = await getTemporaryApi()
     // console.log(res)
     if(res.code === 200){
       // 解析日期并查找最新日期的数据
       const latestData = res.data.reduce((latest, current) => {
         // 将日期字符串转换为 Date 对象
         const currentDate = new Date(current.rq);
         const latestDate = latest ? new Date(latest.rq) : null;

         // 比较日期，找出最新的
         return !latestDate || currentDate > latestDate ? current : latest;
       }, null);
       // console.log(latestData)
       this.dataListDWMB = latestData
     }

   },
    // 计算正确率
    // async getRightRate() {
    //   this.questionData.correctCount = parseInt(this.questionData.correctCount,10)
    //   this.questionData.wrongCount = parseInt(this.questionData.wrongCount,10)
    //   const res = await getCorrectRateApi(this.questionData.correctCount,this.questionData.wrongCount)
    //   if (res.code === 200){
    //     this.averageAccuracyData = res.data
    //   }
    //   // console.log(res)
    // },
    // 临时信息填报表关闭，清空数据
    closeTemporary(){
      this.DMSDataTemp = {}
    },
    // 点击确认，发送请求，修改数据
    updateTemporary(){
      // 表单与验证
      this.$refs.DMSDataTempRef.validate(async valid => {
        if (!valid) return
        let arr = [this.DMSDataTemp]
        const res = await addOperationLogApi(arr)
        // console.log(res)
        // if(res.code !== 200){
        //   return this.$message.error('添加失败')
        // }
        this.dialogVisibleTemporary = false
        this.$message.success('临时数据添加成功')

})

    },
    //监听轮播图切换事件，更新当前 description
    handleCarouselChange(index) {
      this.currentIndex = index
      this.currentDescription = this.images[index].title
    },
    showImage(url) {
      this.currentImageUrl = url
      this.dialogVisible = true
    },
    // 获取数据
    async getData() {
      await getTableTopList().then(res => {
        if (res.code === 200) {
          this.tableData = res.rows[0]
        }
      })
    },

    updateTime() {
      const now = new Date()
      const year = now.getFullYear()
      const month = String(now.getMonth() + 1).padStart(2, '0')
      const day = String(now.getDate()).padStart(2, '0')
      const hours = String(now.getHours()).padStart(2, '0')
      const minutes = String(now.getMinutes()).padStart(2, '0')
      const seconds = String(now.getSeconds()).padStart(2, '0')

      this.currentTime = `${year}/${month}/${day}   ${hours}:${minutes}`
    },
    getDayOfWeek() {
      const daysOfWeek = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']

      const currentDate = new Date()
      const dayIndex = currentDate.getDay()

      this.today = daysOfWeek[dayIndex]
      this.today1 = dayIndex == 0 ? 7 : dayIndex

    },
    async getChoice() {
      await getResultList().then(res => {
        // console.log(res)
        if (res.code === 200) {
          this.Choice = res.rows[0]
        }
      })

    },
    // 获取排名班级
    async getRank() {
      await getRankList().then(res => {
        // console.log(res)
        if (res.code === 200) {
          this.allBj = res.rows.map(item => {
            return item.bj
          })
          // 获取所有排名
          this.tableData1 = res.rows
          this.fRank = this.tableData1[0].zql
          this.sRank = this.tableData1[1].zql
          this.tRank = this.tableData1[2].zql

        }
      })
    },
    handleDialogClose() {
      // 在对话框关闭时触发，用于停止视频播放
      const videoPlayer = this.$refs.videoPlayer
      if (videoPlayer) {
        videoPlayer.pause()
      }
    },
    // 图片切换
    ToggleEvent(type) {
      if (type == 1) {
        this.images = this.images1
      } else if (type == 2) {
        this.images = this.images2
      } else {
        this.images = this.images3
      }
    },

    back() {
      this.$router.back()
      if (document.exitFullscreen) {
        document.exitFullscreen() // 退出全屏
      } else if (document.mozCancelFullScreen) {
        document.mozCancelFullScreen() // Firefox
      } else if (document.webkitExitFullscreen) {
        document.webkitExitFullscreen() // Chrome 和 Safari
      } else if (document.msExitFullscreen) {
        document.msExitFullscreen() // IE
      }
    }
  },
  computed: {
    ...mapState('screen', ['DMSdata', 'averageData'])
  }

}
</script>
<style lang="less" scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

@media screen and (min-width: 1200px) {
  html {
    font-size: 85px !important;
  }

  .container {
    max-width: 1232px;
  }
}

@media screen and (min-width: 761px) {
  .container {
    max-width: 100% !important;
  }

}

@media screen and (max-width: 760px) {
  .container {
    max-width: 890px;
  }
}

#app {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100vh;

  background-color: rgb(78, 88, 107);
  background-size: cover;
  overflow: hidden;
}

#app header {
  position: relative;
  /* width: 100%; */
  flex: 1;

  .caiqi {
    position: absolute;
    top: 0;
    left: 0;
  }
}

#app header .icon-tuichu2 {
  position: absolute;
  top: 0;
  right: 0.5%;
  cursor: pointer;
  font-size: 1.8rem;
}

#app header .title {
  text-align: center;
  line-height: 15rem;
  font-family: 华文琥珀, serif;
  font-size: 4.18rem;
  font-weight: normal;
  letter-spacing: 0.4rem;
  color: #ffffff;
  text-shadow: 0 0 .2rem #ffdd00;
}

#app header .time-day {
  position: absolute;
  right: 2%;
  top: 28%;
  text-align: right;
  line-height: 3.3rem;
  color: rgba(249, 249, 249, 0.8);
  font-size: 1.8rem;
  font-weight: normal;
}

#app header .time {
  position: relative;
  width: 100%;
  height: 100%;
  position: relative;
  background: url('~@/assets/images/星期.png') no-repeat 41% center;

  span {
    position: absolute;
    top: 3%;
    left: 40%;
    font-size: 2rem;
    color: #fff;
  }
}

#app header .day {
}


nav {
  width: 100%;
  flex: 11;
  margin-top: -20px;
}

.container {
  height: 100%;
}

.container .row {
  height: 100%;
}

.container .row .left {
  display: flex;
  flex-direction: column;
  padding-left: 3%;
}

.container .row .left .leftTop {
  flex: 3 !important;
  margin-left: 2%;
  display: flex;
  flex-direction: column;

  .photo {
    flex: 6;
    width: 100%;
    height: 100%;
    margin-top: 8%;
    position: relative;
    background: url('~@/assets/images/生态园足迹.png') no-repeat center;
    background-size: 100% 100%;

    .title {
      position: absolute;
      top: 0%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 999;
    }

    .elCarousel {
      width: 88%;
      min-height: 90%;
      max-height: 95%;
      border-radius: 2%;
      position: absolute;
      top: 52%;
      left: 50.5%;
      transform: translate(-50%, -50%);
      overflow: hidden;

      .centered-img {
        width: 100%;
        height: 85%;
        object-fit: cover;
        display: block;
        border-radius: inherit;
      }
    }
  }

  .shengtai {
    flex: 1;
    margin-top: 4%;

    img {
      width: 30%;
      margin-left: 2%;
      cursor: pointer;

      &:hover {
        transform: scale(1.05);
        transition: all 0.5s;

      }
    }
  }
}


.container .row .left .leftBottom {
  flex: 3;
  width: 100%;
  height: 100%;
  position: relative;
  background: url('~@/assets/screem/生态知识图.png') no-repeat center;
  background-size: 100% 90%;
  letter-spacing: -2px;
  color: #119441;
  font-weight: 500;
  font-size: 1.3rem;

  .banji1 {
    position: absolute;
    top: 40%;
    left: 22%;

    &:hover {
      color: #17783b;
      font-weight: 600;
      font-size: 1.35rem;
    }

  }

  .banji2 {
    position: absolute;
    top: 55%;
    left: 22%;

    &:hover {
      color: #17783b;
      font-weight: 600;
      font-size: 1.35rem;
    }
  }

  .banji3 {
    position: absolute;
    top: 72%;
    left: 22%;

    &:hover {
      color: #17783b;
      font-weight: 600;
      font-size: 1.35rem;
    }
  }

  .answer {
    position: absolute;
    top: 45%;
    left: 10%;
    text-align: center;
    line-height: 50px;
    font-size: 2.1rem;
    letter-spacing: 2px;
  }

  .zhengque {
    display: flex;
    position: absolute;
    top: 45%;
    left: 53%;
    line-height: 50px;
    font-size: 2rem;
    //font-weight: 550;
    //letter-spacing: -1px;
  }

  .icon1 {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 60%;
    left: 60%;
  }
}


.center {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  margin-top: -20px;
  position: relative;
  background: url('~@/assets/screem/生态园区.png') no-repeat center;
  background-size: 85% 99%;

  .img1 {
    position: absolute;
    top: 33%;
    left: 65%;

    &:hover {
      transform: scale(1.025);
      transition: all 0.5s;

    }
  }

  .img2 {
    position: absolute;
    top: 33%;
    left: 21%;

    &:hover {
      transform: scale(1.025);
      transition: all 0.5s;

    }
  }

  .img3 {
    position: absolute;
    top: 55%;
    left: 44%;

    &:hover {
      transform: scale(1.025);
      transition: all 0.5s;

    }
  }

  .img4 {
    position: absolute;
    top: 82%;
    left: 25%;

    &:hover {
      transform: scale(1.025);
      transition: all 0.5s;

    }
  }


}

.right {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  margin-top: 50px;
  padding-left: 1%;


  .rightTop {
    position: relative;
    flex: 3;
    width: 100%;
    height: 100%;
    background: url('~@/assets/images/变废为宝.png') no-repeat center;
    background-size: 90% 99%;

    .detail {
      position: absolute;
      top: 20%;
      left: 15%;
      width: 80%;
      line-height: 2.2rem;
      font-size: 1.3rem;
      letter-spacing: 1px;
      color: #fff;

      .name {
        background-color: #ffffff;
        color: #119441;
      }

      span {
        padding: 0px 3px;
        font-size: 1.6rem;
        font-weight: 600;
        border-radius: 1.1rem;
      }
    }

    .detail1 {
      position: absolute;
      top: 35%;
      right: 12%;
      width: 50%;
      font-weight: 500;
      text-align: right;
      font-size: 1.2rem;
      color: #279e52;

      span {
        font-size: 1.6rem;
      }
    }

    .detail2 {
      position: absolute;
      top: 57%;
      left: 18%;
      width: 50%;
      font-weight: 500;
      text-align: left;
      font-size: 1.2rem;
      color: #279e52;

      span {
        font-size: 1.6rem;
      }
    }

    .detail3 {
      position: absolute;
      top: 77%;
      right: 12%;
      width: 50%;
      font-weight: 500;
      text-align: right;
      font-size: 1.2rem;
      color: #279e52;

      span {
        font-size: 1.6rem;
      }
    }
  }

  .rightBot {
    flex: 2;
    width: 100%;
    height: 100%;
    position: relative;
    margin-bottom: 3%;
    background: url('~@/assets/images/生态成果.png') no-repeat center;
    background-size: 90% 75%;

    .chengguo {
      position: absolute;
      top: 34%;
      left: 20%;
      width: 55%;
      font-weight: 500;
      text-align: center;
      font-size: 1.5rem;
      line-height: 3rem;
      color: #119441;
      letter-spacing: 1px;

      span {
        font-weight: 600;
        font-size: 2.2rem;
      }
    }

  }
}

::v-deep .el-table {
  max-height: 45rem;
  overflow-y: auto;
}

::v-deep .el-dialog:not(.is-fullscreen) {
  margin-top: 10% !important;
}

.zhuanhuanImg {
  width: 100%;
  height: 60rem;
  overflow-y: auto;
  border: 1px solid rgb(95, 203, 113);

  &::-webkit-scrollbar {
    display: none;
    /* Chrome、Safari和Opera中隐藏滚动条 */
  }
}


::v-deep .el-dialog__body {
  background-color: rgb(215, 246, 195);

}

::v-deep .el-dialog__header {
  background-color: rgb(215, 246, 195);

}

::v-deep .el-dialog__title {
  color: #000;
  font-size: 2.125rem;
  font-weight: 700;
}


::v-deep .el-dialog__body {
  padding: 5px 20px;
}


::v-deep .el-carousel__button {
  background-color: #fff;
  width: 0.5rem;
  height: 0.5rem;
  border-radius: 0.3rem;
  margin: 0.15rem;
}

// ::v-deep .el-dialog__body {
//   height: 90rem;
//   overflow: hidden;
//   padding: 1rem;
// }

::v-deep .el-carousel__indicators--horizontal {
  left: 50%;
  -webkit-transform: translateX(-50%);
  transform: translateX(-50%);
}

::v-deep .el-carousel__arrow--left {
  left: 10px;
  display: block !important;
}

::v-deep .el-carousel__arrow--right {
  right: 10px;
  display: block !important;
}


/* 定义抖动效果的 keyframes */
@keyframes shake {
  0% {
    // transform: translateX(0);
    transform: scale(1);
  }

  // 20% {
  //   transform: translateX(-3%);
  // }
  50% {
    // transform: translateX(3%);
    transform: scale(1.2);
  }

  // 60% {
  //   transform: translateX(-3%);
  // }
  // 80% {
  //   transform: translateX(-3%);
  // }

  100% {
    transform: translateX(1);
  }
}

/* 定义元素的 CSS 规则，设置 transform-origin 属性 */
img {
  transform-origin: center;
}

/* 添加 .shake 类，元素加入抖动效果 */
.shake {
  animation: shake 0.5s;
}
</style>
