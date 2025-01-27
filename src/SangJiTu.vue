<template>
  <div class="SangJiTu">
    <div id="SangJiTU"></div>
  </div>
</template>

<script>
import * as echarts from "echarts/core";
import { SankeyChart } from "echarts/charts";
import { TitleComponent, TooltipComponent } from "echarts/components";
import { CanvasRenderer } from "echarts/renderers";

// 注册必要的组件
echarts.use([SankeyChart, TitleComponent, TooltipComponent, CanvasRenderer]);

export default {
  name: "SangJiTu",
  props: {
    sankeyData: Object, // 从父组件传递过来的桑基图数据
  },
  watch: {
    sankeyData(newData) {
      if (newData && newData.nodes.length > 0) {
        this.updateChart(newData); // 当数据变化时更新桑基图
      }
    },
  },
  mounted() {
    this.initChart();
  },
  methods: {
    initChart() {
      const chartDom = document.getElementById("SangJiTU");
      this.myChart = echarts.init(chartDom);
    },

    // 更新桑基图
    updateChart(sankeyData) {
      const option = {
        tooltip: {
          trigger: "item",
          formatter: params => {
            if (params.dataType === "node") {
              return `地点: ${params.name}<br>类别: ${params.data.category}`;
            }
            return `从: ${params.data.source}<br>到: ${params.data.target}<br>值: ${params.data.value}`;
          },
        },
        series: [
          {
            type: "sankey",
            layout: "none", // 禁用自动布局
            data: sankeyData.nodes,
            links: sankeyData.links,
            emphasis: {
              focus: "adjacency",
            },
            layoutIterations: 64, // 增加布局优化次数
            nodeAlign: "justify", // 节点左对齐
            levels: [
              { depth: 0, itemStyle: { color: "#e1d5e7" } }, // 第一列
              { depth: 1, itemStyle: { color: "#d5e8d4" } }, // 第二列
              { depth: 2, itemStyle: { color: "#dae8fc" } }, // 第三列
              { depth: 3, itemStyle: { color: "#ffe6cc" } }, // 第四列
            ],
            lineStyle: {
              color: "source",
              opacity: 0.6,
            },
          },
        ],
        // graphic: [
        //   {
        //     type: "text",
        //     left: "3%",
        //     top: "96%",
        //     style: {
        //       text: "始祖原居地",
        //       fontSize: 16,
        //       fontWeight: "bold",
        //     },
        //   },
        //   {
        //     type: "text",
        //     left: "27%",
        //     top: "96%",
        //     style: {
        //       text: "始祖迁居地",
        //       fontSize: 16,
        //       fontWeight: "bold",
        //     },
        //   },
        //   {
        //     type: "text",
        //     left: "50%",
        //     top: "96%",
        //     style: {
        //       text: "始迁祖原居地",
        //       fontSize: 16,
        //       fontWeight: "bold",
        //     },
        //   },
        //   {
        //     type: "text",
        //     left: "75%",
        //     top: "96%",
        //     style: {
        //       text: "始迁祖迁居地",
        //       fontSize: 16,
        //       fontWeight: "bold",
        //     },
        //   },
        // ],
      };



      this.myChart.setOption(option);
    },
  },
};
</script>

<style scoped>
.SangJiTu {
  width: 100%;
  text-align: center;
}
#SangJiTU {
  width: 100%;
  height: 700px;
}
</style>
