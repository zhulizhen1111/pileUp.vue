<template>
  <div class="info-sumary">
      <p class="accumulation">月累计工单产生数量 <span class="my-size">1200</span> 个   <span class="ratio">工单按时完成率 </span><span class="my-size">95</span>%</p>
      <div class="picture">
        <span class="remark-icon"></span><p class="my-title">本月5类工单数量</p>
         <i-Select v-model="model1" style="width:140px;float:right;margin-right:40px;margin-top:20px">
            <Option v-for="item in cityList" :value="item.value" :key="item.value">{{ item.label }}</Option>
        </i-Select>
        <div id="bill-charts">
           
        </div>
        <div class="legend">
           <div style="background:#4A9EF9"></div>运行类工单&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
           <div style="background:#6ECAF7"></div>巡检类工单&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
           <div style="background:#73DA99"></div>维保类工单&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
           <div style="background:#F3E171"></div>维修类工单&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
           <div style="background:#FABA53"></div>综合工单&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
           <div style="background:#DFE7F0"></div>上月工单总数&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
        </div>
      </div>
      <div class="my-bottom">
        <div class="pie">
           <span class="remark-icon"></span><p class="my-title">工单数量</p>
           <div class="tt-echarts">
              <div id="tt_bill"> </div>
              <div class="tt-legend">
                <div><div class="square"></div>运行类工单<span class="num">500</span><span class="rat">40%</span></div>
                <div><div class="square" style="border:1px solid #6ECAF7"></div>巡检类工单<span class="num">400</span><span class="rat">38%</span></div>
                <div><div class="square" style="border:1px solid #73DA99"></div>维保类工单<span class="num">100</span><span class="rat">30%</span></div>
                <div><div class="square" style="border:1px solid #F3E171"></div>维修类工单<span class="num">100</span><span class="rat">22%</span></div>
                <div><div class="square" style="border:1px solid #FABA53"></div>综合类工单<span class="num">100</span><span class="rat">18%</span></div>
              </div>
           </div>
        </div>
        <div class="my-table">
          <span class="remark-icon"></span><p class="my-title">已完成工单数量</p>
          <div class="tt-v">
            <i-Table stripe  :columns="columns1" :data="data1" size="large"></i-Table>
          </div>  
        </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
var echarts = require("echarts")
export default {
  components: {

  },

  mixins: [],

  props: {

  },

  data () {
    return {
       columns1: [
                    {
                        title: '时间',
                        key: 'name'
                    },
                    {
                        title: '合计',
                        key: 'position'
                    },
                    {
                        title: '运行',
                        key: 'craft'
                    },
                    {
                        title: '巡检',
                        key: 'performance'
                    },
                    {
                        title: '维保',
                        key: 'wage'
                    },
                    {
                        title: '维修',
                        key: 'mark',
                        className: 'table-info-column'
                    },
                    {
                        title: '综合',
                        key: 'ontime'
                    }
                ],
       data1:[
         {name:"上月",position:1600,craft:400,performance:300,wage:300,mark:300,ontime:300},
         {name:"本月",position:1200,craft:300,performance:312,wage:240,mark:300,ontime:300},
         {name:"上周",position:400,craft:100,performance:200,wage:300,mark:300,ontime:300},
         {name:"本周",position:300,craft:80,performance:80,wage:300,mark:300,ontime:300},
         {name:"昨日",position:40,craft:10,performance:8,wage:300,mark:300,ontime:300},
         {name:"今日",position:45,craft:12,performance:13,wage:300,mark:300,ontime:300},
         ],
        cityList: [
                    {
                        value: '一月',
                        label: '一月'
                    },
                    {
                        value: '二月',
                        label: '二月'
                    },
                    {
                        value: '三月',
                        label: '三月'
                    },
                    {
                        value: '四月',
                        label: '四月'
                    },
                    {
                        value: '五月',
                        label: '五月'
                    },
                    {
                        value: '六月',
                        label: '六月'
                    },{
                        value: '七月',
                        label: '七月'
                    },{
                        value: '八月',
                        label: '八月'
                    },{
                        value: '九月',
                        label: '九月'
                    },{
                        value: '十月',
                        label: '十月'
                    },{
                        value: '十一月',
                        label: '十一月'
                    },{
                        value: '十二月',
                        label: '十二月'
                    },
                ],
                model1: '一月'
    
    }
  },

  computed: {

  },

  mounted() {
    this.initCharts();
    this.draw();
  },

  methods: { 
      initCharts(){
        var bill = echarts.init(document.getElementById("bill-charts"));
        bill.setOption({
          tooltip : {
              trigger: 'axis',
              axisPointer : {            // 坐标轴指示器，坐标轴触发有效
                  type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
              }
          },
          grid: {
              left: '3%',
              right: '4%',
              bottom: '3%',
              containLabel: true
          },
          xAxis : [
              {
                  type : 'category',
                  data : ['1','2','3','4','5','6','7','8','9','10','11','12','13','14','15','16','17','18','19','20','21','22',
                  '23','24','25','26','27','28','29','30','31']
              }
          ],
          yAxis : [
              {
                  type : 'value'
              }
          ],
          series : [
              
              {
                  name:'运行类工单',
                  type:'bar',
                  barWidth : 8,
                  itemStyle:{
                    color:'#4A9EF9'
                  },
                  stack: '搜索引擎',
                  data:[120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,132]
              },
              {
                  name:'巡检类工单',
                  type:'bar',
                  itemStyle:{
                    color:'#6ECAF7'
                  },
                  stack: '搜索引擎',
                  data:[120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,100]
              },
              {
                  name:'维保类工单',
                  type:'bar',
                  itemStyle:{
                    color:'#73DA99'
                  },
                  stack: '搜索引擎',
                   data:[120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,132]
              },
              {
                  name:'维修类工单',
                  type:'bar',
                 itemStyle:{
                    color:'#F3E171'
                  },
                  stack: '搜索引擎',
                  data:[120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,100]
              },
              {
                  name:'综合类工单',
                  type:'bar',
                 itemStyle:{
                    color:'#FABA53'
                  },
                  stack: '搜索引擎',
                  data:[120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,120,100,110,114,104,107,100,118,113,100,100]
              },
              {
                  name:'上月工单总数',
                  type:'bar',
                  itemStyle:{
                    color:'#DFE7F0'
                  },
                  data:[450,460,500,520,570,490,440,459,478,492,450,460,500,520,570,490,440,459,478,492,450,460,500,520,570,490,440,459,478,492,450]
              }
          ]
        })
      },
       draw() {
          let myChart = echarts.init(document.getElementById('tt_bill'));

          var scaleData = [{
                  'name': '运行类工单',
                  'value': 500
              },
              {
                  'name': '巡检类工单',
                  'value': 400
              },
              {
                  'name': '维保类工单',
                  'value': 100
              },
              {
                  'name': '维修类工单',
                  'value': 100
              },
              {
                  'name': '综合工单',
                  'value': 100
              },
          ];

          var placeHolderStyle = {
              normal: {
                  label: {
                      show: false
                  },
                  labelLine: {
                      show: false
                  },
                  color: 'rgba(0, 0, 0, 0)',
                  borderColor: 'rgba(0, 0, 0, 0)',
                  borderWidth: 0
              }
          };
          var data = [];

          var color = ['#73DA99', '#FABA53', "#4A9EF9",'#6ECAF7','#F3E171']
          for (var i = 0; i < scaleData.length; i++) {
              data.push({
                  value: scaleData[i].value,
                  name: scaleData[i].name,
                  itemStyle: {
                      normal: {
                          borderWidth: 15,
                          borderColor: color[i],
                      }
                  }
              }, {
                  value: 5,
                  name: '',
                  itemStyle: placeHolderStyle
              });
          }

          var seriesObj = [{
              name: '',
              type: 'pie',
              clockWise: false,
              radius: [70, 70],
              hoverAnimation: false,
              itemStyle: {
                  normal: {
                      label: {
                          show: true,
                          position: 'center',
                          color: '#3B4254',
                          fontSize:18,
                          formatter: function(params) {                   
                              return '\n\n\n\n\n工单总数\n\n 1200'
                          },
                      },

                  }
              },
              data: data
          }];

          myChart.setOption({
            tooltip: {
                show: false
            },
            legend: {
                show: false
            },
            toolbox: {
                show: true
            },
            series: seriesObj
          });

        }

  },

}
</script>

<style scoped lang="less" >
.info-sumary{
  padding: 20px;
  background: #fff;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,0.05);
  border-radius: 2px;
  min-width: 1500px;
  .accumulation{
    line-height: 40px;
    .my-size{
      font-size: 20px;
      color:#4A9EF9;
      font-weight: bold;
    }
    .ratio{
      padding-left: 50px;
    }
  }
  .picture{
    margin:20px 0;
    border: 1px solid #DBDDE4;
    border-radius: 3px;
   
    position: relative;
    .my-title{
      height: 40px;
      font-size: 16px;
      display: inline-block;
      }
      .remark-icon{
          padding: 7px 3px;
          display: inline-block;
          background:#4A9EF9;
          margin:20px 10px 0 20px;
      }
      #bill-charts{
        width: 100%;
        height: 390px;
      }
      .legend{
        position: absolute;
        right: 58px;
        top: 60px;
        >div{
          display: inline-block;
          width: 10px;
          height: 10px;
          margin-right: 5px;
        }
      }
   
  }
  .my-bottom{
    display: flex;
    .pie{
      width: 25.7%;
      min-width: 400px;
      padding-right:2%;
      border: 1px solid #DBDDE4;
     .tt-echarts{
       display: flex;
        #tt_bill{
          width: 200px;
          height: 200px;
          margin-top: 30px;
          
        }
      .tt-legend{
        margin-top: 61px;
        >div{
          height: 30px;
        }
        .square{
          width: 8px;
          height: 8px;
          background: #fff;
          border: 1px solid #4A9EF9;
          border-radius: 50px;
          display: inline-block;
          margin-right: 10px;
        }
        .num{
          margin-left: 15px;
        }
        .rat{
          margin-left: 15px;
        }
      }
     }
      .my-title{
        height: 40px;
        font-size: 16px;
        display: inline-block;
      }
      .remark-icon{
          padding: 7px 3px;
          display: inline-block;
          background:#4A9EF9;
          margin:20px 10px 0 20px;
      }
    }
    .my-table{
      width: 75.2%;
      border: 1px solid #DBDDE4;
      margin-left: 20px;
      .my-title{
      height: 40px;
      font-size: 16px;
      display: inline-block;
      }
      .remark-icon{
          padding: 7px 3px;
          display: inline-block;
          background:#4A9EF9;
          margin:20px 10px 0 20px;
      }
      .tt-v{
        padding: 0 20px 20px 20px;
      }
    }
  }
  
}

</style>
<style lang="less">
 
     .ivu-table-wrapper{
      border:none;
    }
  
</style>

