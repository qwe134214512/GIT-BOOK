<template>
  <el-row class="warp">
    <el-col :span="24" class="warp-breadcrum">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }"><b>首页</b></el-breadcrumb-item>
      </el-breadcrumb>
    </el-col>
    <el-carousel :interval="2000" type="card" height="430px">
      <el-carousel-item v-for="(item, index) in imgs" :key="index">
        <img :src="item.url" width="100%" height="100%" alt="">
      </el-carousel-item>
    </el-carousel>
    <el-col :span="24" class="warp-main">
      <section class="chart-container">
        <el-row>
          <el-col :span="12">
            <div id="chartColumn" style="width:100%; height:400px;"></div>
          </el-col>
          <el-col :span="12">
            <div id="chartBar" style="width:100%; height:400px;"></div>
          </el-col>
          <el-col :span="12">
            <div id="chartLine" style="width:100%; height:400px;"></div>
          </el-col>
          <el-col :span="12">
            <div id="chartPie" style="width:100%; height:400px;"></div>
          </el-col>
          <el-col :span="8">
            <el-card :body-style="{ padding: '0px' }">
              <img src="../assets/images/forest.png" class="image">
              <div style="padding: 14px;">
                <span>一个例子而已</span>
                <div class="bottom clearfix">
                  <time class="time">{{ currentDate }}</time>
                </div>
              </div>
            </el-card>
          </el-col>
          <el-col :span="8">
            <el-card :body-style="{ padding: '0px' }">
              <img src="../assets/images/sunrise.png" class="image">
              <div style="padding: 14px;">
                <span>我是一张卡片</span>
                <div class="bottom clearfix">
                  <time class="time">{{ currentDate }}</time>
                </div>
              </div>
            </el-card>
          </el-col>
          <el-col :span="8">
            <el-card :body-style="{ padding: '0px' }">
              <img src="../assets/images/sunshine.png" class="image">
              <div style="padding: 14px;">
                <span>快乐生活每一天</span>
                <div class="bottom clearfix">
                  <time class="time">{{ currentDate }}</time>
                </div>
              </div>
            </el-card>
          </el-col>
        </el-row>
      </section>

    </el-col>
  </el-row>
</template>
<style>
  .el-carousel {
    width: 100%;
  }
  .el-carousel__item h3 {
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
  }
  
  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }
  
  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
  .time {
    font-size: 13px;
    color: #999;
  }

  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .image {
    width: 100%;
    display: block;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }

  .clearfix:after {
    clear: both
  }

  .chart-container {
    width: 100%;
  }
  .chart-container .el-col {
    padding: 30px 20px;
  }
</style>

<script>
  import echarts from 'echarts'

  export default {
    data() {
      return {
        currentDate: new Date(),
        chartColumn: null,
        chartBar: null,
        chartLine: null,
        chartPie: null,
        imgs: [
          { url: require('../assets/images/banner/ban-1.jpg'), value: 1 },
          { url: require('../assets/images/banner/ban-2.jpg'), value: 2 },
          { url: require('../assets/images/banner/ban-3.jpg'), value: 3 },
          { url: require('../assets/images/banner/ban-4.jpg'), value: 4 },
          { url: require('../assets/images/banner/ban-5.jpg'), value: 5 },
          ]
      };
    },
    mounted: function () {
      var _this = this;
      //基于准备好的dom，初始化echarts实例
      this.chartColumn = echarts.init(document.getElementById('chartColumn'));
      this.chartBar = echarts.init(document.getElementById('chartBar'));
      this.chartLine = echarts.init(document.getElementById('chartLine'));
      this.chartPie = echarts.init(document.getElementById('chartPie'));

      this.chartColumn.setOption({
        color: ['#3398DB'],
        title: { text: 'Column Chart' },
        tooltip: {},
        xAxis: {
          data: ["哲学类 ", "文化教育", "自然科学", "工业技术", "少儿读物", "财经管理", "语言文字", "戏曲小品"]
        },
        yAxis: {},
        series: [{
          name: '销量',
          type: 'bar',
          data: [500, 2000, 3600, 1000, 1000, 2000, 2500, 500]
        }]
      });

      this.chartBar.setOption({
        color: ['#8B8B7A', '#3398DB'],
        title: {
          text: 'Bar Chart',
          subtext: '数据来自系统'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        legend: {
          data: ['2017年', '2018年']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'value',
          boundaryGap: [0, 0.01]
        },
        yAxis: {
          type: 'category',
          data: ['经典著作', '社会科学', '军事科学', '历史地理', '中国文学', '图书总数（本）']
        },
        series: [
          {
            name: '2017年',
            type: 'bar',
            data: [1120, 448, 1293, 1049, 2317, 5802]
          },
          {
            name: '2018年',
            type: 'bar',
            data: [1195, 640, 1600, 1214, 3341, 6818]
          }
        ]
      });

      this.chartLine.setOption({
        title: {
          text: 'Line Chart'
        },
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['借出数量', '借阅次数', '阅读人数']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name: '借阅次数',
            type: 'line',
            stack: '总量',
            data: [120, 132, 101, 134, 90, 230, 210]
          },
          {
            name: '阅读人数',
            type: 'line',
            stack: '总量',
            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: '借出数量',
            type: 'line',
            stack: '总量',
            data: [520, 632, 601, 634, 990, 1030, 1020]
          }
        ]
      });

      this.chartPie.setOption({
        title: {
          text: 'Pie Chart',
          subtext: '纯属虚构',
          x: 'center'
        },
        tooltip: {
          trigger: 'item',
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: 'vertical',
          left: 'left',
          data: ['生活', '小说', '文学', '艺术', '体育']
        },
        series: [
          {
            name: '访问来源',
            type: 'pie',
            radius: '55%',
            center: ['50%', '60%'],
            data: [
              { value: 335, name: '生活' },
              { value: 310, name: '小说' },
              { value: 1548, name: '文学' },
              { value: 135, name: '艺术' },
              { value: 234, name: '体育' }
            ],
            itemStyle: {
              emphasis: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: 'rgba(0, 0, 0, 0.5)'
              }
            }
          }
        ]
      });
    }
  }
</script>
