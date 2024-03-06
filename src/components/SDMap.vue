<template>
  <v-chart class="chart" :option="option" />
</template>

<script>
import * as echarts from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { MapChart } from "echarts/charts";
import { TooltipComponent, GeoComponent } from "echarts/components";
import VChart, { THEME_KEY } from "vue-echarts";

const mapData = [
  {
    name: "威海市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "烟台市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "青岛市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "潍坊市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "东营市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "滨州市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "德州市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "聊城市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "菏泽市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "济宁市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "济南市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "泰安市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "淄博市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "枣庄市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "临沂市",
    assetSize: 1000,
    companyAmount: 10,
  },
  {
    name: "日照市",
    assetSize: 1000,
    companyAmount: 10,
  },
];

echarts.use([CanvasRenderer, MapChart, TooltipComponent, GeoComponent]);

export default {
  name: "HelloWorld1",
  components: {
    VChart,
  },
  provide: {
    [THEME_KEY]: "dark",
  },
  data() {
    return {
      option: {},
    };
  },
  methods: {
    getMapData() {
      fetch("/map/shandong.json")
        .then((res) => {
          return res.json();
        })
        .then((geoJson) => {
          echarts.registerMap("shandong", geoJson);
          this.option = {
            tooltip: {
              // backgroundColor: "rgba(0, 160, 233, 0.8)",
              // 鼠标是否可进入提示框浮层中，默认为false，如需详情内交互，如添加链接，按钮，可设置为 true。
              enterable: true,
              trigger: "item",
              // 提示框触发的条件，可选 鼠标移动时触发 'mousemove' 鼠标点击时触发 'click' 同时鼠标移动和点击时触发 'mousemove|click'
              // triggerOn: 'click',
              // 提示框浮层内容格式器，支持字符串模板和回调函数两种形式
              formatter: function formatter(params) {
                return (
                  "资产规模：" +
                  params.data.assetSize +
                  "<br/>服务企业：" +
                  params.data.companyAmount
                );
              },
            },
            series: [
              {
                name: "资产登记概览",
                type: "map",
                map: "shandong",
                roam: true,
                // 滚轮缩放的极限控制，通过min, max最小和最大的缩放值，默认的缩放为1。
                scaleLimit: {
                  // 最小的缩放值
                  min: 0.5,
                  // 最大的缩放值
                  max: 2,
                },
                // 图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等
                label: {
                  show: true,
                  color: "#999",
                },
                // 地图区域的多边形 图形样式。
                itemStyle: {
                  areaColor: "rgba(50, 60, 72)",
                  borderColor: "#256baf",
                },
                // 数据源
                data: mapData,
              },
            ],
          };
        });
    },
  },
  created() {
    this.getMapData();
  },
};
</script>

<style scoped>
.chart {
  height: 400px;
}
</style>
