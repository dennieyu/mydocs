APACHE Jmeter
=====

[**공식 사이트**](https://jmeter.apache.org)

[**다운로드**](https://jmeter.apache.org/download_jmeter.cgi)

UltimateThreadGroup
=====
   - 동시 사용자 설정
   
<img title="cloud-native" src="./images/jmeter_threads.png" alt="jmeter-threads" width="800px">

   - Threads Schedule 예시
   
```
<?xml version="1.0" encoding="UTF-8"?>
<collectionProp name="ultimatethreadgroupdata">
   <collectionProp name="-1734936043">
      <stringProp name="49">500</stringProp><!-- Start Threads Count : 동시 사용자 수 -->
      <stringProp name="53">5</stringProp><!-- Initial Delay, sec : 초기 지연 -->
      <stringProp name="49">1</stringProp><!-- Startup Time, sec : 500 / 1 초마다 쓰레드 단계적으로 증가 -->
      <stringProp name="48577203">30000</stringProp><!-- Hold Load For, sec : 500분 동안 유지 -->
      <stringProp name="53">5</stringProp><!-- Shutdown Time : 5초 동안 단계적으로 동시 사용자 제거 -->
   </collectionProp>
</collectionProp>
```

ConstantThroughputTimer
=====
   - 분당 요청 수 설정

<img title="cloud-native" src="./images/jmeter_throughput1.png" alt="jmeter-throughout" width="800px">

   - Throughput 설명

<img title="cloud-native" src="./images/jmeter_throughput2.png" alt="jmeter-throughout" width="800px">

   - Throughput 예시

```
<?xml version="1.0" encoding="UTF-8"?>
<ConstantThroughputTimer guiclass="TestBeanGUI" testclass="ConstantThroughputTimer" testname="Constant Throughput Timer" enabled="true">
   <intProp name="calcMode">0</intProp>
   <doubleProp>
      <name>throughput</name>
      <value>6000.0</value><!-- 분단위, 초당 100개를 의미 -->
      <savedValue>0.0</savedValue>
   </doubleProp>
</ConstantThroughputTimer>
```
