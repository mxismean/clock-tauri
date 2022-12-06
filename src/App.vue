<template>
  <div class="box">
    <div id="main"></div>
    <p data-tauri-drag-region></p>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import * as echarts from 'echarts/core';
import { GaugeChart } from 'echarts/charts';
import { CanvasRenderer } from 'echarts/renderers';

echarts.use([GaugeChart, CanvasRenderer]);

onMounted(() => {
  init();
});

const init = () => {
  const chartDom: HTMLElement = document.getElementById('main')!;
  const myChart = echarts.init(chartDom);
  const option = {
    series: [
      {
        name: 'hour',
        type: 'gauge',
        startAngle: 90,
        endAngle: -270,
        min: 0,
        max: 12,
        splitNumber: 12,
        clockwise: true,
        radius: '100%',
        axisLine: {
          lineStyle: {
            width: 15,
            color: [[1, 'rgba(0,0,0,0.7)']],
            shadowColor: 'rgba(0, 0, 0, 0.5)',
          },
        },
        splitLine: {
          lineStyle: {
            shadowColor: 'rgba(0, 0, 0, 0.3)',
            shadowBlur: 3,
            shadowOffsetX: 1,
            shadowOffsetY: 2,
          },
        },
        axisLabel: {
          fontSize: 30,
          distance: 20,
          formatter: function (value: number) {
            if (value === 0) {
              return '';
            }
            return value + '';
          },
        },

        pointer: {
          icon: 'path://M2.9,0.7L2.9,0.7c1.4,0,2.6,1.2,2.6,2.6v115c0,1.4-1.2,2.6-2.6,2.6l0,0c-1.4,0-2.6-1.2-2.6-2.6V3.3C0.3,1.9,1.4,0.7,2.9,0.7z',
          width: 12,
          length: '55%',
          offsetCenter: [0, '8%'],
          itemStyle: {
            color: '#C0911F',
            shadowColor: 'rgba(0, 0, 0, 0.3)',
            shadowBlur: 8,
            shadowOffsetX: 2,
            shadowOffsetY: 4,
          },
        },
        detail: {
          show: false,
        },
        title: {
          offsetCenter: [0, '30%'],
        },
        data: [
          {
            value: 0,
          },
        ],
      },
      {
        name: 'minute',
        type: 'gauge',
        startAngle: 90,
        endAngle: -270,
        min: 0,
        max: 60,
        clockwise: true,
        axisLine: {
          show: false,
        },
        splitLine: {
          show: false,
        },
        axisTick: {
          show: false,
        },
        axisLabel: {
          show: false,
        },
        pointer: {
          icon: 'path://M2.9,0.7L2.9,0.7c1.4,0,2.6,1.2,2.6,2.6v115c0,1.4-1.2,2.6-2.6,2.6l0,0c-1.4,0-2.6-1.2-2.6-2.6V3.3C0.3,1.9,1.4,0.7,2.9,0.7z',
          width: 8,
          length: '90%',
          offsetCenter: [0, '8%'],
          itemStyle: {
            color: '#C0911F',
            shadowColor: 'rgba(0, 0, 0, 0.3)',
            shadowBlur: 8,
            shadowOffsetX: 2,
            shadowOffsetY: 4,
          },
        },
        anchor: {
          show: true,
          size: 20,
          showAbove: false,
          itemStyle: {
            borderWidth: 15,
            borderColor: '#C0911F',
            shadowColor: 'rgba(0, 0, 0, 0.3)',
            shadowBlur: 8,
            shadowOffsetX: 2,
            shadowOffsetY: 4,
          },
        },
        detail: {
          show: false,
        },
        title: {
          offsetCenter: ['0%', '-40%'],
        },
        data: [
          {
            value: 0,
          },
        ],
      },
      {
        name: 'second',
        type: 'gauge',
        startAngle: 90,
        endAngle: -270,
        min: 0,
        max: 60,
        animationDurationUpdate: 0,
        clockwise: true,
        axisLine: {
          show: false,
        },
        splitLine: {
          show: false,
        },
        axisTick: {
          show: false,
        },
        axisLabel: {
          show: false,
        },
        pointer: {
          icon: 'path://M2.9,0.7L2.9,0.7c1.4,0,2.6,1.2,2.6,2.6v115c0,1.4-1.2,2.6-2.6,2.6l0,0c-1.4,0-2.6-1.2-2.6-2.6V3.3C0.3,1.9,1.4,0.7,2.9,0.7z',
          width: 4,
          length: '110%',
          offsetCenter: [0, '8%'],
          itemStyle: {
            color: '#C0911F',
            shadowColor: 'rgba(0, 0, 0, 0.3)',
            shadowBlur: 8,
            shadowOffsetX: 2,
            shadowOffsetY: 4,
          },
        },
        anchor: {
          show: true,
          size: 15,
          showAbove: true,
          itemStyle: {
            color: '#C0911F',
            shadowColor: 'rgba(0, 0, 0, 0.3)',
            shadowBlur: 8,
            shadowOffsetX: 2,
            shadowOffsetY: 4,
          },
        },
        detail: {
          show: false,
        },
        title: {
          offsetCenter: ['0%', '-40%'],
        },
        data: [
          {
            value: 0,
          },
        ],
      },
    ],
  };
  setInterval(function () {
    var date = new Date();
    var second = date.getSeconds();
    var minute = date.getMinutes() + second / 60;
    var hour = (date.getHours() % 12) + minute / 60;
    myChart.setOption({
      series: [
        {
          name: 'hour',
          animation: hour !== 0,
          data: [{ value: hour }],
        },
        {
          name: 'minute',
          animation: minute !== 0,
          data: [{ value: minute }],
        },
        {
          animation: second !== 0,
          name: 'second',
          data: [{ value: second }],
        },
      ],
    });
  }, 1000);
  option && myChart.setOption(option);
};
</script>

<style>
@keyframes loadding {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.box {
  position: relative;
  animation: loadding 1500ms ease-in;
}
.box > p {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  position: absolute;
  z-index: 99999;
  top: 0;
  left: 0;
  background-color: transparent;
}
#main {
  width: 400px;
  height: 400px;
  border-radius: 50%;
  scale: 0.5;
  transform: translate3d(-200px, -200px, 0);
  background-color: rgba(255, 255, 255, 1);
}
</style>
