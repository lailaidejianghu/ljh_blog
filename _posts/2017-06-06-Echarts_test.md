---
layout: post
title: Echarts用法
category: blog
description: Echarts在markdown中示例
---

<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="width: 600px;height:400px;"></div>
    <script type="text/javascript">
        // 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));
        // 指定图表的配置项和数据
        var option = {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data:['销量']
            },
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        };
        // 使用刚指定的配置项和数据显示图表。
        myChart.setOption(option);
    </script>
    
    
   <div id="main1" style="width: 600px;height:400px;"></div>
    <script type="text/javascript"> 
       var myChart = echarts.init(document.getElementById('main1'));
       var dataAll = [
        [
            [10.0, 8.04],
            [8.0, 6.95],
            [13.0, 7.58],
            [9.0, 8.81],
            [11.0, 8.33],
            [14.0, 9.96],
            [6.0, 7.24],
            [4.0, 4.26],
            [12.0, 10.84],
            [7.0, 4.82],
            [5.0, 5.68]
        ],
        [
            [10.0, 9.14],
            [8.0, 8.14],
            [13.0, 8.74],
            [9.0, 8.77],
            [11.0, 9.26],
            [14.0, 8.10],
            [6.0, 6.13],
            [4.0, 3.10],
            [12.0, 9.13],
            [7.0, 7.26],
            [5.0, 4.74]
        ],
        [
            [10.0, 7.46],
            [8.0, 6.77],
            [13.0, 12.74],
            [9.0, 7.11],
            [11.0, 7.81],
            [14.0, 8.84],
            [6.0, 6.08],
            [4.0, 5.39],
            [12.0, 8.15],
            [7.0, 6.42],
            [5.0, 5.73]
        ]
    ];
    var markLineOpt = {
        animation: false,
        label: {
            normal: {
                formatter: 'y = 0.5 * x + 3',
                textStyle: {
                    align: 'right'
                }
            }
        },
        lineStyle: {
            normal: {
                type: 'solid'
            }
        },
        tooltip: {
            formatter: 'y = 0.5 * x + 3'
        },
        data: [[{
            coord: [0, 2],
            symbol: 'none'
        }, {
            coord: [20, 13],
            symbol: 'none'
        }]]
    };
    option = {
        title: {
            text: 'Anscombe\'s quartet',
            x: 'center',
            y: 0
        },
        grid: [
            {x: '7%', y: '7%', width: '38%', height: '38%'},
            {x2: '7%', y: '7%', width: '38%', height: '38%'},
            {x: '7%', y2: '7%', width: '38%', height: '38%'},
            {x2: '7%', y2: '7%', width: '38%', height: '38%'}
        ],
        tooltip: {
            formatter: 'Group {a}: ({c})'
        },
        xAxis: [
            {gridIndex: 0, min: 0, max: 20},
            {gridIndex: 1, min: 0, max: 20},
            {gridIndex: 2, min: 0, max: 20}
        ],
        yAxis: [
            {gridIndex: 0, min: 0, max: 15},
            {gridIndex: 1, min: 0, max: 15},
            {gridIndex: 2, min: 0, max: 15}
        ],
        series: [
            {
                name: 'I',
                type: 'scatter',
                xAxisIndex: 0,
                yAxisIndex: 0,
                data: dataAll[0],
                markLine: markLineOpt
            },
            {
                name: 'II',
                type: 'scatter',
                xAxisIndex: 1,
                yAxisIndex: 1,
                data: dataAll[1],
                markLine: markLineOpt
            },
            {
                name: 'III',
                type: 'scatter',
                xAxisIndex: 2,
                yAxisIndex: 2,
                data: dataAll[2],
                markLine: markLineOpt
            }
        ]
    };
     myChart.setOption(option);
   </script>

   <div id="main1" style="width: 600px;height:400px;"></div>
   <script type="text/javascript"> 
      var myChart = echarts.init(document.getElementById('main1'));
      var dataAll = [
       [
          [0,2.6],
          [1,3.4],
          [2,4.3],
          [3,4.7],
          [4,5],
          [5,7.2],
          [6,8.4],
          [7,8.4],
          [8,10.7],
          [9,11.3],
          [10,12.6]
       ],
       [
           [0,1.2],
           [1,2.45],
           [2,5],
           [3,6.85],
           [4,7.6],
           [5,8.25],
           [6,8.7],
           [7,10.65],
           [8,10.9],
           [9,9.65],
           [10,9.9]
       ],
       [
           [0,20],
           [1,4.5],
           [2,1],
           [3,11],
           [4,12.5],
           [5,12.8],
           [6,13.2],
           [7,14],
           [8,16],
           [9,18],
           [10,12]
       ]
   ];
   var markLineOpt = {
       animation: false,
       label: {
           normal: {
               formatter: ['y = 1.0145 * x + 1.0582',
                           'y=-0.1294*x^2 +2.4497*x-1.37',
                           'y = -0.0169x5 + 0.5377x4 - 6.4436x3 + 35.56x2 - 86.244x + 76.87'
               ]
               textStyle: {
                   align: 'right'
               }
           }
       },
       lineStyle: {
           normal: {
               type: 'solid'
           }
       },
       tooltip: {
           formatter: ['y = 1.0145 * x + 1.0582',
                       'y=-0.1294*x^2 +2.4497*x-1.37',
                       'y = -0.0169x5 + 0.5377x4 - 6.4436x3 + 35.56x2 - 86.244x + 76.87'
           ]
       },
       data: [[{
           coord: [0, 2],
           symbol: 'none'
       }, {
           coord: [20, 13],
           symbol: 'none'
       }]]
   };
   option = {
       title: {
           text: 'Anscombe\'s quartet',
           x: 'center',
           y: 0
       },
       grid: [
           {x: '7%', y: '7%', width: '38%', height: '38%'},
           {x2: '7%', y: '7%', width: '38%', height: '38%'},
           {x: '7%', y2: '7%', width: '38%', height: '38%'},
           {x2: '7%', y2: '7%', width: '38%', height: '38%'}
       ],
       tooltip: {
           formatter: 'Group {a}: ({c})'
       },
       xAxis: [
           {gridIndex: 0, min: 0, max: 10},
           {gridIndex: 1, min: 0, max: 10},
           {gridIndex: 2, min: 0, max: 10}
       ],
       yAxis: [
           {gridIndex: 0, min: 0, max: 13},
           {gridIndex: 1, min: 1, max: 11},
           {gridIndex: 2, min: 1, max: 20}
       ],
       series: [
           {
               name: 'I',
               type: 'scatter',
               xAxisIndex: 0,
               yAxisIndex: 0,
               data: dataAll[0],
               markLine: markLineOpt
           },
           {
               name: 'II',
               type: 'scatter',
               xAxisIndex: 1,
               yAxisIndex: 1,
               data: dataAll[1],
               markLine: markLineOpt
           },
           {
               name: 'III',
               type: 'scatter',
               xAxisIndex: 2,
               yAxisIndex: 2,
               data: dataAll[2],
               markLine: markLineOpt
           }
       ]
   };
    myChart.setOption(option);
   </script>

</body>
