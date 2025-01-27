<template>
  <div id="china-map" style="width: 640px; height: 500px;min-width: 640px"></div>
</template>

<script>
import { defineComponent, onMounted } from "vue";
import * as echarts from "echarts/core";
import { use, registerMap } from "echarts/core";
import { MapChart } from "echarts/charts";
import { TooltipComponent } from "echarts/components";
import { CanvasRenderer } from "echarts/renderers";
import chinaMap from "@/assets/china.json"; // 中国地图数据

use([CanvasRenderer, MapChart, TooltipComponent]);

export default defineComponent({
  name: "chinaMap",
  emits: ["province-clicked"], // 声明事件
  setup(props, { emit }) {
    onMounted(() => {
      const chart = echarts.init(document.getElementById("china-map"));

      // 注册地图数据
      registerMap("china", chinaMap);

      // 配置地图
      const option = {
        tooltip: {
          trigger: "item",
          formatter: (params) => {
            return params.name; // 仅显示省份名称
          },
        },
        series: [
          {
            name: "中国地图",
            type: "map",
            map: "china",
            roam: false, // 支持缩放和拖动
            label: {
              show: true, // 显示省份名称
              color: "#808080", // 名称字体颜色（正常状态）
              fontSize: 14, // 名称字体大小
              fontFamily: "微软雅黑", // 设置省份名称字体为黑体
            },
            itemStyle: {
              areaColor: "#e9b090", // 正常状态下的区域颜色
              borderColor: "#fff", // 正常状态下的边界线颜色
            },
            emphasis: {
              label: {
                show: true,
                color: "#fff", // 光标停留时的文字颜色
              },
              itemStyle: {
                areaColor: "#e08150", // 光标停留时的区域颜色
                borderColor: "#fff", // 光标停留时的边界线颜色
              },
            },
            // 选中状态的配置
            selectedMode: 'single', // 允许多选
            select: {
              label: {
                show: true,
                color: "#808080", // 选中时的文字颜色
              },
              itemStyle: {
                areaColor: "#F2DDD2", // 选中时的区域颜色
                borderColor: "#fff", // 选中时的边界线颜色
              },
            },
            data: [], // 不需要显示统计数据，因此数据为空
          },
        ],
      };

      chart.setOption(option);

      // 监听点击事件
      chart.on("click", (params) => {
        if (params.componentType === "series") {
          const provinceName = params.name; // 获取被点击的省份名称
          console.log("点击的省份：", provinceName);
          emit("province-clicked", provinceName); // 通过事件将省份名称传递给父组件
        }
      });
    });
  },
});
</script>

<style>
/* 添加样式（可选） */
</style>
