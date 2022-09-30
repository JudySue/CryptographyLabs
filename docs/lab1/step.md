# 实验步骤

## 1.加密

1. 完成初始化存储函数 `void convertToIntArray(char *str, int pa[4][4])`，按照列存储；
2. 完成字节代换函数 `void subBytes(int array[4][4])`，利用已经给出的函数 `getNumFromSBox`；
3. 实现左移函数 `void leftLoop4int(int array[4], int step)` 和行移位函数 `void shiftRows(int array[4][4])`；
4. 实现列混淆函数 `void mixColumns(int array[4][4])`，利用已经给出的函数 `GFMul`；
5. 实现轮密钥加函数 `void addRoundKey(int array[4][4], int round)`；
6. 实现密钥扩展中的 T 函数 `int T(int num, int round)`；
7. 实现密钥扩展函数 `void extendKey(char *key)`；
8. 读懂 `aes` 函数为完成 `deAes` 函数做准备。

## 2.解密

1. 完成逆字节代换函数 `void deSubBytes(int array[4][4])`，利用已经给出的函数 `getNumFromS1Box`；
2. 实现右移函数 `void rightLoop4int(int array[4], int step)` 和行移位函数 `void deShiftRows(int array[4][4])`；
3. 实现逆列混淆函数 `void deMixColumns(int array[4][4])`，利用已经给出的函数 `GFMul`；
4. 完成 `void deAes(char *c, int clen, char *key)`。

## 3.结果参照

可以参照下图对比密钥扩展和加密结果是否正确。

<center><img src="../assets/4-1.png" width = 800></center>
<center>图 4-1 参考结果</center>

