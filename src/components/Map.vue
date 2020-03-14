<template>
  <div class="map">
    <div id="chart"></div>
  </div>
</template>

<style>
#chart {
  margin: 0 auto;
  width: 600px;
  height: 500px;
}
</style>

<script>
// eslint-disable-next-line no-unused-vars
import echarts from "echarts";
// eslint-disable-next-line no-unused-vars
import jsonp from "jsonp";
import "echarts/map/js/china"; // 引入中国地图

// 制定图表的配置和数据
// eslint-disable-next-line no-unused-vars
let option = {
  // 配置
  titel: {
    // 标题
    text: "疫情地图demo",
    x: "center",
    textStyle: {
      color: "#9c0505"
    }
  },
  // 提示信息
  tooltip: {
    trigger: "item",
    // {a} 系列名称 {b} 区域名称 {c} 合并数值 {d} 无
    formatter: "地区：{b}<br/>确诊：{c}"
  },
  // 数据
  series: [
    {
      type: "map",
      map: "china",
      // data: [
      //   { name: "北京", value: 200 },
      //   { name: "湖北", value: 20000 },
      //   { name: "湖南", value: 2000 },
      //   { name: "西藏", value: 2 },
      //   { name: "云南", value: 200 }
      // ],
      // 文本标签，详细说明
      label: {
        show: true,
        color: "red",
        fontSize: 10
      },
      // 缩放比例
      zoom: 1.3,
      // 地图样式
      itemStyle: {
        borderColor: "blue"
      },
      // 高亮状态下的设置
      emphasis: {
        label: {
          color: "#fff",
          fontSize: 12
        },
        itemStyle: {
          areaColor: "green"
        }
      }
    }
  ],
  // 视觉地图
  visualMap: {
    // 分段型图表
    type: "piecewise",
    show: true,
    pieces: [
      // 不指定max即是为无限大
      { min: 10000 },
      { min: 1000, max: "9999" },
      { min: 100, max: "999" },
      { min: 10, max: "99" },
      { min: 1, max: "9" },
      { value: 0 } // 不指定min表示为 -infinity
    ],
    isRange: {
      color: ["#fff", "#ffaa85", "#660208"]
    },
    itemWidth: 10,
    itmeHeight: 10
  },
  toolbox: {
    show: true,
    orient: "horizontal",
    left: "right",
    top: "top",
    feature: {
      dataView: { readOnly: false },
      restore: {},
      saveAsImage: {}
    }
  }
};

export default {
  data(){
    return {
      myChart: ''
    }
  },
  mounted(){
    this.getData();
  this.myChart = echarts.init(document.getElementById('chart'));
},
methods: {
  getData(){
        //jsonp('url',function(){})
        jsonp('https://interface.sina.cn/news/wap/fymap2020_data.d.json?_=1580892522427',(err,data)=>{
           // console.log(data.data.list)
            //data.data.list    map()
            var lists = data.data.list.map(item=>{return {name: item.name, value: item.value}});
            console.log(lists);
            option.series[0].data = lists;
            // 使用刚指定的配置项和数据显示图表。
            this.myChart.setOption(option);
        })
    }
}
}
</script>