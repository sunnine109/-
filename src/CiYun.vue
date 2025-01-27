


<template>
  <div class="world-cloud-3d">
    <div class="world-cloud-canvas-wrapper">
      <canvas
          id="world-cloud-canvas"
          width="800"
          height="400"
          style="width: 100%; max-width: 600px"
      ></canvas>
    </div>
    <div style="display: none" id="weightTags"></div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {};
  },
  props: {
    wordArr: {
      type: Array,
      default: () => []
    },
  },
  methods: {
    // 启动词云
    startWorldCloud: function (updateFlag) {
      this.createTagListDom();
      let o = {
        maxSpeed: 0.01,
        minSpeed: 0.01,
        textHeight: 25,
        outlineMethod: "colour",
        fadeIn: 800,
        outlineColour: "#fff456aa",
        outlineOffset: 0,
        depth: 0.97,
        minBrightness: 0.2,
        wheelZoom: false,
        reverse: true,
        shadowBlur: 2,
        shuffleTags: true,
        shadowOffset: [1, 1],
        stretchX: 2, // 水平方向更大
        stretchY: 1, // 垂直方向更大
        initial: [0.1, 0.1],
        textFont: null,
        textColour: null,
        weight: true,
        weightMode: "size",
        weightSize: 1,
      };
      try {
        // 如果不是更新，说明是第一次渲染，就启动 tagcanvas, 否则就代表更新
        if (!updateFlag) {
          // eslint-disable-next-line no-undef
          TagCanvas.Start("world-cloud-canvas", "weightTags", o);
        } else {
          // eslint-disable-next-line no-undef
          TagCanvas.Update("world-cloud-canvas");
        }
      } catch (e) {
        console.error(e);
      }
    },
    // 根据父组件传过来的 wordArr 创建 TagList Dom列表，放到页面中供，canvas 渲染
    // 这里后端的数组中的数据结构是一个对象 { name: 要展示的tag名字， light: true/false 据定是否要加重展示}
    createTagListDom: function () {
      let res = [...this.wordArr];
      let fragment = new DocumentFragment();
      for (let i = 0; i < res.length; i++) {
        let a = document.createElement("a");
        // 字符串长度大于10就要换行
        if (res[i].name.length > 10) {
          let charArr = res[i].name.split("");
          charArr.splice(10, 0, "<br>");
          res[i].name = charArr.join("");
        }
        a.innerHTML = res[i].name;
        a.href = "javascript:void(0)";

        //数据前十名/数据10-20/数据20-30
        if (res[i].light === "large") {
          a.className = "large";
        } else if (res[i].light === "medium") {
          a.className = "medium";
        } else if (res[i].light === "small") {
          a.className = "small";
        }

        // 添加调试输出
        console.log(`Word: ${res[i].name}, Class: ${a.className}`);

        // 为每个词添加点击事件，触发反馈信息
        a.addEventListener("click", () => {
          // 触发 Vue 组件自定义事件并传递点击的词数据
          this.$emit("word-clicked", res[i]);
        });
        fragment.append(a);
      }
      // 更新 tagContainer中的 tag元素
      let tagsContainer = document.querySelector("#weightTags");
      tagsContainer.innerHTML = "";
      tagsContainer.append(fragment);
    }
  },
  watch: {
    // 如果词云发生变化就要 重绘 tagcanvas
    wordArr: function () {
      this.startWorldCloud(true);
    },
  },
  mounted() {
    // 组件装载成果 绘制 tagcanvas
    this.startWorldCloud();
  },
};
</script>
// 这里 style 不能加scope属性不然就不会成功
<style lang="less">
.world-cloud-3d {
  .world-cloud-canvas-wrapper {
    width: 600px;
    height: 400px;
    max-width: 600px;
    max-height: 400px;
    overflow: visible; // 确保文字不被截断
    padding: 20px; // 给文字和边界预留空间
  }
  #weightTags {
    font-size: 12px;
    /*
    .huge {
      font-size: 50px;
      color: #d2b48c; // 浅棕色（棕褐色）
    }
    */
    .large {
      font-size: 70px;
      color: #BD430A; 
      //color: #ffd700; // 金黄色
    }
    .medium {
      font-size: 55px;
      color: #1F78B4; 
      // color: #E08150; // 秘鲁色（更深的棕橙色）
    }
    .small {
      font-size: 35px;
      color: #33A02C; 
      // color: #E9B090; // 深金色
    }
  }
}
</style>