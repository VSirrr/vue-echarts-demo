<template>
  <v-chart ref="areaChart" class="chart" :option="option" />
</template>

<script>
import * as echarts from "echarts";
import { CanvasRenderer } from "echarts/renderers";
import { LineChart } from "echarts/charts";
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
} from "echarts/components";
import VChart, { THEME_KEY } from "vue-echarts";
console.log(echarts);

echarts.use([
  CanvasRenderer,
  LineChart,
  TitleComponent,
  TooltipComponent,
  GridComponent,
]);

export default {
  name: "AreaChart",
  components: {
    VChart,
  },
  provide: {
    [THEME_KEY]: "light",
  },
  data() {
    // 获取当前月份与之前的七个月份
    function getPreviousMonths() {
      const currentDate = new Date();
      const currentMonth = currentDate.getMonth() + 1;
      const result = [];
      for (let i = 0; i < 8; i++) {
        let month = currentMonth - i;
        if (month <= 0) {
          month += 12;
        }
        result.unshift(month + "月");
      }
      return result;
    }

    const months = getPreviousMonths();
    return {
      option: {
        title: {
          text: "车辆行情价与厂商指导价对比",
          left: "center",
        },
        tooltip: {
          show: true,
          trigger: "axis",
          // 是否将 tooltip 框限制在图表的区域内。
          confine: true,
          textStyle: {
            fontSize: 10,
            color: "#646464",
          },
          axisPointer: {
            type: "line",
            lineStyle: {
              color: "rgb(52, 118, 253)",
              width: 1,
              type: "dashed",
            },
          },
          formatter(params) {
            const { name } = params[0];
            return `${name}<br/>车辆行情价： XX.XX万<br/>厂商指导价： XX.XX万`;
          },
          alwaysShowContent: true,
        },
        grid: {
          // left: "2%",
          // right: "4%",
          // bottom: "1%",
          containLabel: true,
          // height: "96%",
        },
        xAxis: {
          type: "category",
          data: months,
          boundaryGap: false,
          axisPointer: {
            handle: { show: true },
          },
        },
        yAxis: {
          type: "value",
          axisLabel: {
            formatter() {
              return "";
            },
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: "rgb(229, 229, 229)",
              type: "dashed",
              width: 1,
            },
          },
        },
        series: [
          {
            type: "line",
            smooth: true,
            showSymbol: false,
            itemStyle: {
              color: "#c4c4c4",
              width: 2,
            },
            data: new Array(8).fill(9),
          },
          {
            data: [10, 9, 9, 8, 6, 5, 5, 6],
            type: "line",
            smooth: true,
            showSymbol: false,
            lineStyle: {
              color: "#3377ff",
              width: 2,
            },
            areaStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: "rgba(137, 168, 255, 0.5)" },
                  { offset: 1, color: "rgba(137, 168, 255, 0)" },
                ]),
              },
            },
          },
        ],
      },
    };
  },
  mounted() {
    this.$refs.areaChart.chart.dispatchAction({
      type: "showTip",
      seriesIndex: 0,
      dataIndex: 7,
    });
  },
};
</script>

<style scoped>
.chart {
  height: 400px;
}
</style>
