<template>
    <div class="DiTu1">
      <div ref="chart" style="width: 600px; height: 400px; border: 0px solid gray;"></div>
    </div>
  </template>
  
  <script setup>
  import { onMounted, ref } from 'vue';
  import * as echarts from 'echarts';
  import emitter from '../utils/emitter';
  import Chinamap from '../assets/china.json';
  import MyData from '../assets/new.json';
  
  const province = [
      '北京', '天津', '河北', '山西', '内蒙古', '辽宁', '吉林',
      '黑龙江', '上海', '江苏', '浙江', '安徽', '福建', '江西',
      '山东', '河南', '湖北', '湖南', '广东', '广西', '海南',
      '重庆', '四川', '贵州', '云南', '西藏', '陕西', '甘肃',
      '青海', '宁夏', '新疆', '台湾', '澳门', '香港'
  ];
  
  const phases = [
      { start: 1600, end: 1700 },
      { start: 1701, end: 1800 },
      { start: 1801, end: 1900 },
      { start: 1901, end: 2000 },
      { start: 2001, end: 2024 }
  ];
  
  let myChart;
  const chart = ref();
  const phasesName = ['17世纪', '18世纪', '19世纪', '20世纪', '21世纪'];
  
  const chartOption = {
      baseOption: {
          timeline: {
              axisType: 'category',
              // realtime: false,
              // loop: false
              autoPlay: true,
              playInterval: 5000,
              symbolSize: 16,
              left: '5%',
              right: '5%',
              bottom: '0%',
              width: '90%',
              // controlStyle: {
              //     position: 'left'
              // },
              data: phasesName,
              tooltip: {
                  formatter: phases,
              },
            //   label: {
            //       color: '#616161',
            //       fontWeight: 'bold',
            //       fontSize:16,
            //   },
              label: { // 文字样式控制
                normal: {
                  textStyle: {
                    color: '#616161',
                    fontSize: 14,
                  }
                },
                emphasis: {
                  textStyle: { 
                    color: '#5E5E5E', 
                    fontSize: 17,},
                    fontWeight:'bold'
                },
              },
          },
          tooltip: {
              show: true,
              formatter: function (params) {
                  return params.name + '：' + params.value
              },
          },
          visualMap: {
              type: 'piecewise',
              pieces: [
                  {
                      min: 1000,
                      max: 10000,
                    //   color: '#BD430A'
                      color: '#C4460A'
                  },
                  {
                      min: 501,
                      max: 1000,
                      color: '#E08150'
                  },
                  {
                      min: 101,
                      max: 500,
                      color: '#E9B090'
                  },
                  {
                      min: 1,
                      max: 100,
                      color: '#F2DDD2'
                  },
                  {
                      value: 0,
                      color: '#F7F7F7'
                  }
              ],
              orient: 'vertical',
              itemWidth: 25,
              itemHeight: 15,
              showLabel: true,
              seriesIndex: [0],
  
              textStyle: {
                  color: '#757575',
                  fontWeight: 'bold'
              },
              bottom: '12%',
              left: "4%",
          },
          grid: {
              right: '7%',
              top: '20%',
              bottom: '10%',
              width: '22%'
          },
          xAxis: {
              // min: 0,
              // max: 4000,
              scale: true,
              show: false
          },
          yAxis: [{
              inverse: true,
              offset: '2',
              'type': 'category',
              data: '',
              nameTextStyle: {
                  color: '#fff'
              },
              axisTick: {
                  show: false,
              },
              axisLabel: {
                  //rotate:45,
                  textStyle: {
                      fontSize: 15,
                      color: '#575757',
                      fontWeight:'bold'
                  },
                  interval: 0
              },
              axisLine: {
                  show: false,
                  lineStyle: {
                      color: '#333'
                  },
              },
              splitLine: {
                  show: false,
                  lineStyle: {
                      color: '#333'
                  }
              },
          }],
          geo: {
              map: 'china',
              right: '38%',
              left: '20%',
              emphasis: {
                label: {
                    show:false
                },
                itemStyle: {
                    areaColor: '#8792b3',
                    borderColor: "#fff",
                }
              },
              select: {
                label: {
                    show: false
                },
                itemStyle: {
                    areaColor: '#8792b3' ,
                    borderColor: "#fff",
                }
              },
              selectedMode: 'single',
              itemStyle: {
              borderColor: "#b3b3b3", // 正常状态下的边界线颜色
              },
            //   label: {
            //       emphasis: {
            //           show: false
            //       }
            //   },
            //   itemStyle: {
            //       emphasis: {
            //           areaColor: '#8792b3'
            //       }
            //   }
          },
          series: [{
              name: 'mapSer',
              type: 'map',
              map: 'china',
              roam: false,
              geoIndex: 0,
              label: {
                  show: false,
              },
          },
          {
              'name': '',
              'type': 'bar',
              zlevel: 2,
              barWidth: '40%',
              label: {
                  normal: {
                      show: true,
                      fontSize: 17,
                      position: 'right',
                      formatter: '{c}'
                  }
              },
          }
          ],
      },
      animationDurationUpdate: 5000,
      animationEasingUpdate: 'quinticInOut',
      options: []
  };
  
  
  onMounted(() => {
      echarts.registerMap('china', Chinamap);
      myChart = echarts.init(chart.value);
      updateChart(MyData);
  });
  
  emitter.on('data', updateChart);
  
  function updateChart(data) {
      const options = createOptions(data);
      myChart.setOption({ ...chartOption, options });
  }
  
  function createOptions(data) {
      const counts = Array.from({ length: phases.length }, () => Array(province.length).fill(0)); 
      //创建二维数组用于存储每个时期的各省数据
      data.forEach(item => {
          const year = parseInt(item.版本年代);
          phases.forEach((phase, phaseIndex) => {
              if (year >= phase.start && year <= phase.end) {
                  province.forEach((prov, index) => {
                      if (item.居地.includes(prov)) counts[phaseIndex][index]++;
                  });
              }
          });
      });
  
      return phases.map((_, i) => createPhaseOption(counts[i]));
  }
  
  function createPhaseOption(counts) {
      const sortedData = counts.map((value, i) => ({ name: province[i], value })).sort((a, b) => b.value - a.value);
      const names = sortedData.slice(0, 10).map(item => item.name);
      const values = sortedData.slice(0, 10).map(item => item.value);
  
      return {
          yAxis: { data: names },
          series: [
              { type: 'map', data: sortedData },
              { type: 'bar', data: values, itemStyle: { normal: { color: getColor } } }
          ]
      };
  }
  
  function getColor(params) {
      const colorList = [{
          colorStops: [{
              offset: 0,
              color: '#BD430A' // 0% 处的颜色
          }, {
              offset: 1,
              color: '#BD430A' // 100% 处的颜色
          }]
      },
      {
          colorStops: [{
              offset: 0,
              color: '#BD430A' // 0% 处的颜色
          }, {
              offset: 1,
              color: '#BD430A' // 100% 处的颜色
          }]
      }
      ];
      return colorList[params.dataIndex < 3 ? 0 : 1];
  }
  </script>













