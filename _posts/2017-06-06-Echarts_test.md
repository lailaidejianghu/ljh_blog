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
    
    
   <!--div id="main1" style="width: 600px;height:400px;"></div>
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
   </script-->

   <div id="chart1" style="width: 600px;height:400px;"></div>
    <script type="text/javascript"> 
      var myChart = echarts.init(document.getElementById('chart1'));
      var data =[ [0,2.6],
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
         ];
            // See https://github.com/ecomfe/echarts-stat
            var myRegression = ecStat.regression('polynomial', data, 1);
            myRegression.points.sort(function(a, b) {
                return a[0] - b[0];
            });
            option = {
                tooltip: {
                    trigger: 'axis',
                    axisPointer: {
                        type: 'cross'
                    }
                },
                title: {
                    text: '18 companies net profit and main business income (million)',
                    subtext: 'By ecStat.regression',
                    sublink: 'https://github.com/ecomfe/echarts-stat',
                    left: 'center',
                    top: 16
                },
                xAxis: {
                    type: 'value',
                    splitLine: {
                        lineStyle: {
                            type: 'dashed'
                        }
                    },
                    splitNumber: 20
                },
                yAxis: {
                    type: 'value',
                    min: -40,
                    splitLine: {
                        lineStyle: {
                            type: 'dashed'
                        }
                    }
                },
                grid: {
                    top: 90
                },
                series: [{
                    name: 'scatter',
                    type: 'scatter',
                    label: {
                        emphasis: {
                            show: true,
                            position: 'right',
                            textStyle: {
                                color: 'blue',
                                fontSize: 16
                            }
                        }
                    },
                    data: data
                }, {
                    name: 'line',
                    type: 'line',
                    smooth: true,
                    showSymbol: false,
                    data: myRegression.points,
                    markPoint: {
                        itemStyle: {
                            normal: {
                                color: 'transparent'
                            }
                        },
                        label: {
                            normal: {
                                show: true,
                                position: 'left',
                                formatter: myRegression.expression,
                                textStyle: {
                                    color: '#333',
                                    fontSize: 14
                                }
                            }
                        },
                        data: [{
                            coord: myRegression.points[myRegression.points.length - 1]
                        }]
                    }
                }]
            };
      myChart.setOption(option);
   </script>

      
   <div id="chart2" style="width: 600px;height:400px;"></div>
    <script type="text/javascript"> 
      var myChart = echarts.init(document.getElementById('chart2'));
      var data = [
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
          ];
            // See https://github.com/ecomfe/echarts-stat
            var myRegression = ecStat.regression('polynomial', data, 2);
            myRegression.points.sort(function(a, b) {
                return a[0] - b[0];
            });
            option = {
                tooltip: {
                    trigger: 'axis',
                    axisPointer: {
                        type: 'cross'
                    }
                },
                title: {
                    text: '18 companies net profit and main business income (million)',
                    subtext: 'By ecStat.regression',
                    sublink: 'https://github.com/ecomfe/echarts-stat',
                    left: 'center',
                    top: 16
                },
                xAxis: {
                    type: 'value',
                    splitLine: {
                        lineStyle: {
                            type: 'dashed'
                        }
                    },
                    splitNumber: 20
                },
                yAxis: {
                    type: 'value',
                    min: -40,
                    splitLine: {
                        lineStyle: {
                            type: 'dashed'
                        }
                    }
                },
                grid: {
                    top: 90
                },
                series: [{
                    name: 'scatter',
                    type: 'scatter',
                    label: {
                        emphasis: {
                            show: true,
                            position: 'right',
                            textStyle: {
                                color: 'blue',
                                fontSize: 16
                            }
                        }
                    },
                    data: data
                }, {
                    name: 'line',
                    type: 'line',
                    smooth: true,
                    showSymbol: false,
                    data: myRegression.points,
                    markPoint: {
                        itemStyle: {
                            normal: {
                                color: 'transparent'
                            }
                        },
                        label: {
                            normal: {
                                show: true,
                                position: 'left',
                                formatter: myRegression.expression,
                                textStyle: {
                                    color: '#333',
                                    fontSize: 14
                                }
                            }
                        },
                        data: [{
                            coord: myRegression.points[myRegression.points.length - 1]
                        }]
                    }
                }]
            };
      myChart.setOption(option);
   </script>

   <div id="chart3" style="width: 600px;height:400px;"></div>
   <script type="text/javascript"> 
      var myChart = echarts.init(document.getElementById('chart3'));
      var data = [
           [0,30],
           [1,10],
           [1.5,1],
           [3,16],
           [4,18],
           [5,19],
           [6,19.5],
           [7,21],
           [8,24],
           [9,27],
           [10,10]
            ];
            // See https://github.com/ecomfe/echarts-stat
            var myRegression = ecStat.regression('polynomial', data, 5);
            myRegression.points.sort(function(a, b) {
                return a[0] - b[0];
            });
            option = {
                tooltip: {
                    trigger: 'axis',
                    axisPointer: {
                        type: 'cross'
                    }
                },
                title: {
                    text: '18 companies net profit and main business income (million)',
                    subtext: 'By ecStat.regression',
                    sublink: 'https://github.com/ecomfe/echarts-stat',
                    left: 'center',
                    top: 16
                },
                xAxis: {
                    type: 'value',
                    splitLine: {
                        lineStyle: {
                            type: 'dashed'
                        }
                    },
                    splitNumber: 20
                },
                yAxis: {
                    type: 'value',
                    min: -40,
                    splitLine: {
                        lineStyle: {
                            type: 'dashed'
                        }
                    }
                },
                grid: {
                    top: 90
                },
                series: [{
                    name: 'scatter',
                    type: 'scatter',
                    label: {
                        emphasis: {
                            show: true,
                            position: 'right',
                            textStyle: {
                                color: 'blue',
                                fontSize: 16
                            }
                        }
                    },
                    data: data
                }, {
                    name: 'line',
                    type: 'line',
                    smooth: true,
                    showSymbol: false,
                    data: myRegression.points,
                    markPoint: {
                        itemStyle: {
                            normal: {
                                color: 'transparent'
                            }
                        },
                        label: {
                            normal: {
                                show: true,
                                position: 'left',
                                formatter: myRegression.expression,
                                textStyle: {
                                    color: '#333',
                                    fontSize: 14
                                }
                            }
                        },
                        data: [{
                            coord: myRegression.points[myRegression.points.length - 1]
                        }]
                    }
                }]
            };
      myChart.setOption(option);
   </script>
</body>