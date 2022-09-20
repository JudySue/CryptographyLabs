# 实验步骤

## 加密

&emsp;&emsp;Step1.完成初始化存储函数 void convertToIntArray(char *str, int pa[4][4])，按照列存储；
&emsp;&emsp;Step2.完成字节代换函数 void subBytes(int array[4][4])，利用已经给出的函数getNumFromSBox()；
&emsp;&emsp;Step3.实现左移函数void leftLoop4int(int array[4], int step)和行移位函数void shiftRows(int array[4][4])；
&emsp;&emsp;Step4.实现列混淆函数void mixColumns(int array[4][4])，利用已经给出的函数GFMul(int n, int s)；
&emsp;&emsp;Step5.实现轮密钥加函数void addRoundKey(int array[4][4], int round)；
&emsp;&emsp;Step6.实现密钥扩展中的T函数int T(int num, int round)；
&emsp;&emsp;Step7.实现密钥扩展函数void extendKey(char *key)；
&emsp;&emsp;Step8.读懂aes函数为完成deaes函数做准备。

## 解密

&emsp;&emsp;Step1.完成逆字节代换函数 void deSubBytes(int array[4][4])，利用已经给出的函数getNumFromS1Box()；
&emsp;&emsp;Step2.实现右移函数void rightLoop4int(int array[4], int step)和行移位函数void deShiftRows(int array[4][4])；
&emsp;&emsp;Step3.实现逆列混淆函数void deMixColumns(int array[4][4])，利用已经给出的函数GFMul(int n, int s)；
&emsp;&emsp;Step4.完成void deAes(char *c, int clen, char *key)

## 结果参照
&emsp;&emsp;可以参照下图对比密钥扩展和加密结果是否正确。

<center><img src="../assets/4-1.png" width = 800></center>
<center>图4-1 参考结果</center>

