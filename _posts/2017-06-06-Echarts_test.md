---
layout: post
title: Echarts用法
category: blog
description: Echarts在markdown中示例
---


<body>
    
   --- 
 南昌理工学院8220     1.会计  2动漫制作技术      3计算机应用技术     4市场营销     5金融管理     6电子商务
 <br>
江西应用科技学院8240     1会计     2计算机应用技术     3市场营销     4金融管理     5旅游管理     6电子商务<br>
南昌师范学院 8207     1会计     2旅游管理 <br>
九江学院8217     1会计     2广告设计与制作     3酒店管理     4旅游管理     5市场营销     6电子商务<br>
南昌工学院 8237     1文秘     2会计     3动漫制作技术     4计算机网络技术     5市场营销     6电子商务<br>
江西理工大学8228     1财务会计类    <br>
武昌工学院 3553     1会计     2广告设计与制作    3计算机应用技术     4市场营销     5金融管理     6电子商务<br>
上饶师范学院8279     1财务会计类     2教育类<br>
江苏财经职业技术学院6309     1会计     2财务管理     3计算机应用技术     4金融管理     5电子商务     6工商企业管理<br>
江苏农林职业技术学院6331     1文秘     2数字媒体应用技术     3计算机应用技术     4酒店管理     5财务管理     6市场营销<br>
厦门农业职业学院6353     1广告设计与制作     2会计     3计算机网络技术     4市场营销     5旅游管理     6电子商务    <br>
江西太豪动漫职业学院8649     1数字媒体艺术设计     2艺术设计     3计算机应用技术     4市场营销     5财务管理     6电子商务 <br>

江西科技学院8219     1会计     2数字媒体艺术设计     3财务管理     4计算机应用技术     5市场营销     6电子商务     （学费贵）<br>
---
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
    
   <table>
     <tr>
       <th>
            <div id="chart1" style="width: 300px;height:280px;"></div>
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
                             text: '图1',
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
                             splitNumber:1 
                         },
                         yAxis: {
                             type: 'value',
                             min: 0,
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
        </th>
        <th>
            <div id="chart2" style="width: 300px;height:280px;"></div>
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
                             text: '图2',
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
                             splitNumber:1 
                         },
                         yAxis: {
                             type: 'value',
                             min: 0,
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
        </th>
        <th>
            <div id="chart3" style="width: 300px;height:280px;"></div>
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
                             text: '图3',
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
                             splitNumber:1 
                         },
                         yAxis: {
                             type: 'value',
                             min: 0,
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
        </th>
      </tr>
    <table>
</body>
