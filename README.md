1、硬件：ESP8266、VS1838红外接收头、红外发射头、Arduino、2n2222三极管

2、软件：[Arduino (with ESP8266 support)](https://github.com/esp8266/Arduino)

3、参考库：

​		红外接收：https://github.com/z3t0/Arduino-IRremote

​		红外发射：https://github.com/crankyoldgit/IRremoteESP8266/tree/master/examples

​		ESP web Server：https://github.com/esp8266/ESPWebServer

4、步骤：

（1）利用红外接收头接收遥控器编码，本例用接收的是格力空调YADOF型号遥控器编码（参考：IRremote/IRrecvDumpV2）

![1](D:\桌面\arduino\Gree_YADOF\img\1.jpg)

（2）记录NEC编码信息

（3）利用红外发射头发射出去（参考：IRremoteESP8266/IRsendDemo）

![2](D:\桌面\arduino\Gree_YADOF\img\2.jpg)

5、注意事项：

（1）格力空调有两种遥控器 YADOF 和 YBOF2 ，YADOF编码长度为YBOF2 的两倍，且前一半和YBOF2编码完全一致

（2）利用IRrecvDumpV2接收时，由于原库中参数的选取，只能接收到73位编码，问题在于：

​			a、超过5000us的space被认为中止信号，而实际YADOF编码中有最长40000的space，修改文件/IRremote/IRremoteInt.h 中宏定义位 #define  _GAP  100000

​			b、原库中最多接收编码数设定为 100，修改为300，因为YADOF里包含279位编码

​			c、即便按上面改了还是没用，因为在原库中定义数组长度的变量rawlen为8为无符号整型变量，这样最大上限为255，因此需要将IRremote.h和IRremoteInt.h中的rawlen的定义改为长整型long，这样才能读出遥控器中的279位编码

6、联系方式：Author：Zhang xin feng        Email：xfzhang96@hust.edu.cn

