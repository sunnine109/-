<template>
  <div id="app">

    <div class="focus-image" >
      <img src="./assets/picture/background4.jpg" alt="Focus Image" class="image" />
      <div class="overlay"></div>
      <div class="title">
        <h1 id = "xungen">寻 根 问 祖</h1>
        <h1>探 索 家 族 的 历 史 脉 络</h1>
        <h3>每个姓氏背后都有一段深厚的历史文化...</h3>
      </div>
    </div>


    <div class="focus-img">
      <img src="./assets/picture/background5.jpg" alt="Focus Image" class="img" />

      <div class="content">
        <div class="logo">
          <img src="./assets/picture/g.png" alt="Logo" />
        </div>

        <div class="text-content">
          <h1 style="font-size: 3vw; margin-top: -1vw;font-family: 方正隶变简体">寻根问祖</h1>
          <h1 style="font-size: 3vw; ">可以看见的家谱可视化平台</h1>
          <h1 style="font-size: 1.5vw; margin-top: 150px">“参天之木，必有其根；怀山之水，必有其源” <br>
            在漫长的历史长河中，每个家族都有自己独特的故事。<br>
            而家谱，便是打开家族神秘之门的钥匙。<br>
            我们将带您踏上这场奇妙的探索之旅，
            揭开家谱背后的神秘面纱。</h1>

          <h1 class="rectangle">探脉溯源</h1>
        </div>

      </div>
    </div>

    <h1 class="rounded-title">
      - 寻根之径<br>
      家谱的分布画卷 -
    </h1>
    <h2 style="font-family: 方正隶变简体">在广袤的中华大地上，姓氏如繁星散布，见证着岁月流转与民族融合。这里，我们为你呈现了一幅宏大的家谱地图。
      <br>姓氏收录表等待着你去开启属于自己的故事。选好姓氏，地图将生动展示出各省份的家谱数量。<br>
      或许你会惊喜地发现，自己的姓氏在某些地方有着深厚的根基，而在另一些地方则如星星之火，悄然绽放。
      <br>这不仅仅是一组数字，更是家族在这片土地上繁衍生息的见证。
    </h2>
    <div class="horizontal-container">
      <XingShiXuanZe />
      <DiTu1 />
    </div>

    <div class="main-container">
      <!-- 左侧竖向标题 -->
      <h1 class="vertical-rectangle">
        - 地域之缘<br>
        姓氏的多元图谱 -
      </h1>



      <!-- 右侧内容：地图2和词云 -->
      <div class="horizontal-container1">
        <div class="map-container1">
          <DiTu2 @province-clicked="handleProvinceClick" />
          <div v-if="showPopup" class="popup">
            <div class="popup-content">
              <p>{{ popupMessage }}</p>
              <button @click="closePopup">关闭</button>
            </div>
          </div>
          <h2 style="margin-top: 60px;font-family: 方正隶变简体;text-indent: 2em;width: 500px;margin:  auto">在中国，每个省份都像是一本独特的故事集，不同姓氏家族在这里交织出绚丽的画卷。
            左边的地图是我们探索地域姓氏构成的钥匙。选择一个省份，便会生成相应的姓氏词云。
          </h2>
        </div>
        <div class="wordcloud-container1">
          <CiYun :wordArr="words" @word-clicked="handleWordClick" />
          <h2 style="margin-top: 60px;font-family: 方正隶变简体;text-indent: 2em;width: 500px;margin:  auto">不同颜色与字号代表着在该省份中不同姓氏的家谱保存的完备程度。词云里的一个个姓氏，
            犹如家族的旗帜，高高飘扬。我们可以借此直观地感受到不同姓氏的家谱在各地的分布保存情况，领略地域与家族的紧密联系。</h2>
        </div>
      </div>
    </div>

    <div class="main-container">
      <h1 class="vertical-rectangle">
        - 传承之路 <br> 家谱的时代印记 -
      </h1>
      <div class="horizontal-container2">
        <div class="zhexiantu-container">
          <ZheXianTu ref="zheXianTu" :versionData="versionData" :chartTitle="chartTitle" />
          <h2 style="width:600px;font-family: 方正隶变简体;text-indent: 2em">
            家谱，不仅记录了家族的血脉传承，更见证了历史的变迁。点击词云中的姓氏，我们便会为你呈现这个姓氏在所选省份的家谱数量随着年代的变化的折线图。从古老的过去到现代，家族的兴衰沉浮在这张图上清晰可见。
          </h2>
        </div>
        <div class="zhuzhuangtu-container">
          <ZhuZhuangTu ref="zhuZhuangTu" :versionTypeData="versionTypeData" :ChartTitle="ChartTitle" />
          <h2 style="width:600px; font-family: 方正隶变简体;text-indent: 2em">
            饼状图通过展示相应的家谱类型构成，诉说了家族传承的方式的演变。在这一部分，可以感受到家谱的演变与传承，领略家族文化的深厚底蕴。
          </h2>
        </div>
      </div>
    </div>

    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
 


    <h1 class="rounded-title">
      - 迁徙之旅 <br> 家族的漫漫征程 -
    </h1>
    <h2 style="text-indent: 2em;font-family: 方正隶变简体;width: 1000px;margin: 30px auto">家族的历史，宛如一首波澜壮阔的迁徙之歌。先辈们为了生存与发展，毅然背井离乡，迈向未知的远方。桑基图如一幅神秘的画卷，徐徐展开了相应姓氏家谱中记载的迁徙路线。在这里，你能直观地感受到家族在发展留下的点点足迹。
      让我们跟随家族的迁徙路径，追忆先辈们的奋斗历程，感受家族的坚韧与智慧。
    </h2>
        <div class="sangjitu-container">
          <SangJiTu ref="sangJiTu" :sankeyData="sankeyData" />
        </div>


    <br>
    <br>
    <br>
    <br>


  </div>

<!-- ##################################### -->

<!-- ##################################### -->

</template>

<script>
import XingShiXuanZe from './components/XingShiXuanZe.vue';
import DiTu1 from './components/DiTu1.vue';
import CiYun from '@/components/CiYun.vue';
import DiTu2 from '@/components/DiTu2.vue';
import ZheXianTu from '@/components/ZheXianTu.vue';
import ZhuZhuangTu from '@/components/ZhuZhuangTu.vue';
import SangJiTu  from "@/components/SangJiTu.vue";

const jsonData = require('./assets/new.json');

export default {
  name: 'App',
  components: {
    SangJiTu,
    XingShiXuanZe,
    DiTu1,
    CiYun,
    DiTu2,
    ZheXianTu,
    ZhuZhuangTu,
  },
  data() {
    return {
      menuItems: ['家谱地图展示', '地域姓氏构成对比', '姓氏时空上的分布趋势'],
      activeIndex: 0,
      words: [],
      versionData: [],//折线图版本数据
      versionTypeData: [],//柱状图版本类型数据
      chartTitle: '浙江省李姓家谱数量变化',  // 折线图默认标题
      ChartTitle: '浙江省李姓家谱版本类型统计',
      clickedWord: null,
      showPopup: false,
      selectedProvince: '浙江', // 默认选中省份
      defaultSurname: '李', // 默认姓氏
      sankeyData: [], // 用来存储桑基图数据
      // ##################################################
      popupMessage: "该省份暂无数据，请选择其他省份！", // 弹窗提示信息
      // ##################################################
    };
  },
  methods: {
    setActive(index) {
      this.activeIndex = index;
    },

    // // 获取选中省份的前20个姓氏
    // getTop20Surnames(province) {
    //   const surnameCounts = {};
    //   jsonData.forEach((item) => {
    //     if (item.居地 === province) {
    //       surnameCounts[item.姓氏] = (surnameCounts[item.姓氏] || 0) + 1;
    //     }
    //   });

    //   const sortedSurnames = Object.entries(surnameCounts).sort((a, b) => b[1] - a[1]);
    //   return sortedSurnames.map(([name]) => ({ name, light: true }));
    // },

    //  ##################################################
     // 获取选中省份的前30个姓氏
     getTop20Surnames(province) {
      const surnameCounts = {};

      // 统计姓氏数量
      jsonData.forEach((item) => {
        if (item.居地 === province) {
          surnameCounts[item.姓氏] = (surnameCounts[item.姓氏] || 0) + 1;
        }
      });

      // 如果该省份没有数据，触发弹窗
      if (Object.keys(surnameCounts).length === 0) {
        this.showPopup = true; // 显示弹窗
        return []; // 返回空数组，避免继续执行
      }

      // 按数量从高到低排序
      const sortedSurnames = Object.entries(surnameCounts).sort((a, b) => b[1] - a[1]);

      // 分配样式类别
      // eslint-disable-next-line no-unused-vars
      return sortedSurnames.slice(0, 30).map(([name, count], index) => {
        let lightClass;
        if (index < 10) {
          lightClass = "large"; // 前 10 个用 large
        } else if (index < 20) {
          lightClass = "medium"; // 10-20 名用 medium
        } else {
          lightClass = "small"; // 20-30 名用 small
        }
        return { name, light: lightClass }; // 返回对应的样式类别
      });
    },
    closePopup() {
      this.showPopup = false; // 关闭弹窗
    },
    //  ##################################################

    // 获取指定姓氏的版本年代数据
    getSurnameVersionData(surname) {
      const versionCounts = {};

      jsonData.forEach(item => {
        if (item.姓氏 === surname && item.居地 === this.selectedProvince) {
          const version = item.版本年代;
          versionCounts[version] = (versionCounts[version] || 0) + 1;
        }
      });

      const versionData = Object.entries(versionCounts).map(([version, count]) => ({
        version,
        count,
      }));

      versionData.sort((a, b) => a.version - b.version);
      return versionData;
    },

    getVersionTypeData(surname) {
      const versionTypeCounts = {};

      jsonData.forEach(item => {
        if (item.姓氏 === surname && item.居地 === this.selectedProvince) {
          const version = item.版本类型;
          versionTypeCounts[version] = (versionTypeCounts[version] || 0) + 1;
        }
      });

      const  versionTypeData = Object.entries(versionTypeCounts).map(([version, count]) => ({
        version,
        count,
      }));

      versionTypeData.sort((a, b) => a.version - b.version);
      return versionTypeData;
    },
    getSankeyData(surname) {
      const sankeyData = { nodes: [], links: [] };
      const addedNodes = new Map(); // 存储节点及其类别

      jsonData.forEach(item => {
        if (
            item.姓氏 === surname &&
            item.居地 === this.selectedProvince &&
            item.始祖原居地 !== 0 &&
            item.始祖迁居地 !== null &&
            item.始迁祖原居地 !== null &&
            item.始迁祖迁居地 !== 0
        ) {
          const nodes = [
            { name: item.始祖原居地, category: "始祖原居地", depth: 0 },
            { name: item.始祖迁居地, category: "始祖迁居地", depth: 1 },
            { name: item.始迁祖原居地, category: "始迁祖原居地", depth: 2 },
            { name: item.始迁祖迁居地, category: "始迁祖迁居地", depth: 3 }
          ];

          nodes.forEach(node => {
            if (!addedNodes.has(node.name)) {
              addedNodes.set(node.name, node.category);
              sankeyData.nodes.push({ name: node.name, category: node.category, depth: node.depth });
            }
          });

          const link1 = {
            source: item.始祖原居地,
            target: item.始祖迁居地,
            value: 1,
          };
          const link2 = {
            source: item.始迁祖原居地,
            target: item.始迁祖迁居地,
            value: 1,
          };

          if (link1.source !== link1.target && !this.isCircular(link1, sankeyData.links)) {
            sankeyData.links.push(link1);
          }

          if (link2.source !== link2.target && !this.isCircular(link2, sankeyData.links)) {
            sankeyData.links.push(link2);
          }
        }
      });

      return sankeyData;
    },

// 检查是否形成环路
    isCircular(link, existingLinks) {
      const source = link.source;
      const target = link.target;

      // 通过已存在的链接判断是否形成环路
      return existingLinks.some(existingLink => {
        return existingLink.source === target && existingLink.target === source;
      });
    },


    // 处理词云点击事件，显示该姓氏的版本年代数据
    handleWordClick(word) {
      const surname = word.name;
      this.versionData = this.getSurnameVersionData(surname);
      this.chartTitle = `${this.selectedProvince}省${surname}姓家谱数量变化`;  // 动态更新标题
      this.updateLineChart(this.versionData); // 更新折线图

      this.versionTypeData = this.getVersionTypeData(surname); // 获取该姓氏的版本类型数据
      this.ChartTitle = `${this.selectedProvince}省${surname}姓家谱版本类型统计`;  // 动态更新标题
      this.updatePieChart(this.versionTypeData); // 调用饼图更新方法

      this.sankeyData = this.getSankeyData(surname); // 更新桑基图数据
      this.$refs.sangJiTu.updateChart(this.sankeyData); // 更新桑基图
    },

    // 更新折线图
    updateLineChart(versionData) {
      this.$refs.zheXianTu.updateChart(versionData);
    },
    // 更新饼图
    updatePieChart(versionTypeData) {
      this.$refs.zhuZhuangTu.updateChart(versionTypeData); // 通过ref更新柱状图组件的数据
    },

    // 处理地图点击事件，更新当前选中的省份
    handleProvinceClick(province) {
      this.selectedProvince = province;
      this.words = this.getTop20Surnames(province);  // 更新词云数据

      this.versionData = this.getSurnameVersionData(this.defaultSurname);  // 获取默认“李”姓数据
      this.chartTitle = `${province}省${this.defaultSurname}姓家谱数量变化`;  // 更新标题

      this.versionTypeData = this.getVersionTypeData(this.defaultSurname);
      this.ChartTitle = `${province}省${this.defaultSurname}姓家谱版本类型统计`;

      this.sankeyData = this.getSankeyData(this.defaultSurname); // 默认展示“李”姓的桑基图
      this.$refs.sangJiTu.updateChart(this.sankeyData); // 更新桑基图
    },

    // closePopup() {
    //   this.showPopup = false;
    // },
  },
  mounted() {
    this.words = this.getTop20Surnames(this.selectedProvince);  // 初始化词云数据
    this.versionData = this.getSurnameVersionData(this.defaultSurname);  // 默认显示“李”姓数据
    this.versionTypeData = this.getVersionTypeData(this.defaultSurname);
    this.sankeyData = this.getSankeyData(this.defaultSurname); // 默认展示“李”姓的桑基图
  },
};
</script>

<style scoped>
@import './assets/font/font.css'; /* ############ add ######################## */

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  background-image: url('./assets/picture/15.jpg'); /* 替换为你的图片路径 */
  background-size: cover; /* 背景填满整个页面 */
  background-position: center; /* 背景居中 */
  background-attachment: fixed; /* 背景固定，不随页面滚动 */
}
h1 {
  font-family: '方正隶变简体', serif;
  font-size: 8vh;
  color: #000000;
  margin-bottom: 20px;
  font-weight:normal;
  text-shadow: 3px 3px 5px grey;   /* #################################### */
}
#xungen{
  font-size: 11vh;
  margin-top:0;
}
h3 {
  margin-top: 50px;
  font-family: '方正隶变简体', serif;
  font-size: 4vh;
  color: #363533;
  font-weight:normal;
  width: 85%;
  margin-left: 60px;
}


/* ############ add start ######################## */
.focus-img {
  position: relative;
  width: 100%;
  height: 100vh; /* 可调整图片高度 */
}
.focus-img .img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* 保证图片按比例填充容器 */
}
.focus-img .content {
  position: absolute;
  top: 49%; /* 居中 */
  left: 47%;
  height: 100%;
  width: 100%;
  transform: translate(-50%, -50%);
  display: flex; /* 使用Flexbox布局 */
  align-items: center; /* 垂直居中 */
  justify-content: center; /* 居中对齐内容 */
  gap:5vh
}
.logo img {
  width: 30vw; 
  height: 30vw; 
  border-radius: 10%;
}
.text-content {
  display: flex;
  flex-direction: column; /* 使标题纵向排列 */
  align-items: center; /* 文本内容居中 */
}
/* ############# add end ####################### */

.rounded-title {
  display: inline-block;
  padding: 10px 20px;
  background-color: rgb(231,221,221,0.7); /* 背景颜色 */
  border-radius: 15px; /* 圆角半径 */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* 阴影效果 */
  text-align: center;
  font-family: "方正隶变简体", sans-serif;
  font-size: 6vh;
  color: #333; /* 文字颜色 */
  margin: 20px auto;
}
/* 容器整体布局 */
.main-container {
  display: flex;
  align-items: flex-start;
  gap: 20px; /* 左右内容间距 */
  padding: 20px;
}
.rectangle{
  display: inline-block;
  padding: 10px 20px;
  background-color: rgb(217,185,126); /* 背景颜色 */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* 阴影效果 */
  text-align: center;
  font-family: "方正隶变简体", sans-serif;
  font-size: 3vh;
  color: #333; /* 文字颜色 */
  margin: 20px auto;
  margin-left: 500px;
}
/* 左侧竖向标题样式 */
.vertical-rectangle {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(231,221,221,0.7); /* 背景颜色+透明度 */
  border-radius: 30px; /* 圆角半径 */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* 阴影效果 */
  writing-mode: vertical-rl; /* 设置文字方向为竖向 */
  text-align: center;
  font-family: "方正隶变简体", sans-serif;
  font-size: 6vh;
  color: #333;
  padding: 20px 10px;
  width: auto; /* 宽度自适应 */
  margin-top: 100px;
}

/* 右侧内容容器 */
.horizontal-container1 {
  display: flex;
  flex-direction: column; /* 垂直排列 */
  justify-content: space-between; /* 均匀分布，严格上下对齐 */
  flex: 1; /* 占用剩余空间 */
  gap: 20px; /* 上下内容间距 */
  width: 100%;
}

/* 地图2和词云占位 */

.map-container1 {
  display: flex;
  flex-direction: row; /* 垂直排列 */
  justify-content: space-between; /* 均匀分布，严格上下对齐 */
  flex: 1; /* 占用剩余空间 */
}

.wordcloud-container1 {
  height: 300px; /* 示例高度 */
  display: flex;
  flex-direction: row; /* 垂直排列 */
  justify-content: space-between; /* 均匀分布，严格上下对齐 */
  flex: 1; /* 占用剩余空间 */
}


.horizontal-container2 {
  display: flex; /* 水平排列 */
  justify-content: space-between; /* 水平间距均匀分布 */
  flex: 1; /* 占用剩余空间 */
}

/* 折线图容器 */
.zhexiantu-container {
  margin-top:150px;
  height: 300px; /* 示例高度 */
  width: 800px; /* 控制宽度 */
}

/* 柱状图容器 */
.zhuzhuangtu-container {
  margin-top:150px;
  height: 300px; /* 示例高度 */
  width: 45%; /* 控制宽度 */
  margin-right: 150px;
}
.focus-image {
  position: relative;
  width: 100%;
  height: 100vh; /* 可调整图片高度 */
}
.focus-image .image {
  width: 100%;
  height: 100%;
  object-fit: cover; /* 保证图片按比例填充容器 */
}
.focus-image .overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.5); /* 白色半透明背景 */
  z-index: 1; /* 确保半透明背景层在图片之下 */
}
.focus-image .title {
  position: absolute;
  top: 40%; /* 居中 */
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2; /* 确保文字在半透明背景层之上 */
}


.horizontal-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 30px;
  padding: 10px;
}
.sangjitu-container{
  margin: 50px auto;
  height: 700px; /* 示例高度 */
  width: 1300px; /* 控制宽度 */
}



/* ############### add start##################### */
.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}
.popup-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}
.popup-content p {
  margin-bottom: 20px;
  font-size: 1rem;
}
.popup-content button {
  padding: 10px 20px;
  border: none;
  background-color: #f60;
  color: white;
  font-size: 1rem;
  border-radius: 5px;
  cursor: pointer;
}
.popup-content button:hover {
  background-color: #e55;
}
/* ############# add end ####################### */

</style>

<style>
/* 确保 HTML 和 body 没有默认边距 */
html, body {
  margin: 0; /* 去除外边距 */
  padding: 0; /* 去除内边距 */
  width: 100%; /* 设置宽度为100% */
  height: 100%; /* 设置高度为100% */
  overflow-x: hidden; /* 防止水平滚动条 */
}

/* 修改 #app 的样式，让背景图片填满整个页面 */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  background-image: url('./assets/picture/background4.jpg'); /* 替换为你的图片路径 */
  background-position: center; /* 背景居中 */
  background-attachment: fixed; /* 背景固定，不随页面滚动 */
  width: 100%; /* 设置宽度为100% */
  min-height: 100vh; /* 确保高度为视口高度 */
}

#app::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.5); /* 半透明的灰色遮罩 */
  z-index: 1; /* 确保遮罩层在背景图片上方 */
  background-size: cover; /* 背景填满整个页面 */
}

/* 确保内容在遮罩层之上 */
#app > * {
  position: relative;
  z-index: 2; /* 确保内容在遮罩层之上 */
}
</style>
