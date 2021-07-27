# ir-raw-encode-for-haa

## 项目描述

将接受到的原始红外编码成HAA编码

## 转换为 HAA 编码示例

运行main.py   

输入红外编码：
```
3050 -3000 3050 -4400 550 -1600 600 -500 600 -1600 550 -500 600 -550 500 -1650 550 -1600 600 -550 500 -1600 600 -550 500 -550 600 -1600 550 -550 550 -550 550 -550 550 -550 450 -600 550 -500 600 -550 550 -1600 550 -550 550 -550 500 -550 600 -500 550 -550 550 -500 600 -500 550 -550 600 -500 600 -550 450 -550 600 -500 550 -550 550 -1650 500 -1650 600 -550 500 -1600 600 -1600 600 -1450 700 -1600 550 -550 550 -500 550 -1650 550 -550 550 -1600 600 -1600 600 -500 550 -500 600 -500 550 -550 600 -500 550 -550 550 -500 600 -550 550 -500 550 -550 550 -550 550 -500 600 -1600 550 -550 550 -550 550 -550 500 -550 600 -500 500 -550 600 -500 600 -550 500 -550 550 -550 550 -550 500 -550 600 -550 500 -500 600 -550 550 -550 500 -550 600 -500 600 -500 500 -550 600 -550 500 -550 550 -550 550 -550 500 -550 600 -550 550 -550 500 -500 600 -500 550 -550 600 -550 550 -550 500 -500 600 -500 600 -500 550 -550 550 -550 500 -550 600 -550 550 -500 550 -550 550 -500 600 -1600 600 -500 550 -1600 500 -600 550 -550 550 -500 600 -500 600 -550 500 -1600 600 -1600 600 -550 550
```

输出：
```
GcGSGcJxAaC)AkAQAkC)AaAQAkAaAQC<AaC)AkAaAQC)AkAaAQAaAkC)AaAaAaAaAaAaAaAaAGAkAaAQAkAaAaC)AaAaAaAaAQAaAkAQAaAaAaAQAkAQAaAaAkAQAkAaAGAaAkAQAaAaAaC<AQC<AkAaAQC)AkC)AkCoA5C)AaAaAaAQAaC<AaAaAaC)AkC)AkAQAaAQAkAQAaAaAkAQAaAaAaAQAkAaAaAQAaAaAaAaAaAQAkC)AaAaAaAaAaAaAQAaAkAQAQAaAkAQAkAaAQAaAaAaAaAaAQAaAkAaAQAQAkAaAaAaAQAaAkAQAkAQAQAaAkAaAQAaAaAaAaAaAQAaAkAaAaAaAQAQAkAQAaAaAkAaAaAaAQAQAkAQAkAQAaAaAaAaAQAaAkAaAaAQAaAaAaAQAkC)AkAQAaC)AQAkAaAaAaAQAkAQAkAaAQC)AkC)AkAaAa
```


## 捕获红外数据代码，使用 Arduino Uno
```
/*
 * IRremote: IRrecvDump - dump details of IR codes with IRrecv
 * An IR detector/demodulator must be connected to the input RECV_PIN.
 * Version 0.1 July, 2009
 * Copyright 2009 Ken Shirriff
 * http://arcfn.com
 * JVC and Panasonic protocol added by Kristian Lauszus (Thanks to zenwheel and other people at the original blog post)
 * LG added by Darryl Smith (based on the JVC protocol)
 */

/*
 * 在Ken Shirriff的代码基础上新增HAA编码方法
 * 
 * 使用前修改IRremote库代码，修改IRremoteInt.h文件
 * 将RAW_BUFFER_LENGTH调整为300，如果使用的Arduino设备内存更大此处的值可以调的更高，以便接受更大的数据包。
 * 目前已知家庭设备比较大的数据包长度为800。
 * 
 * 项目地址：https://github.com/huanghyw/ir-raw-encode-for-haa
 * 
 */

#include <IRremote.h>
/* 
 *  Default is Arduino pin D11. 
 *  You can change this to another available Arduino Pin.
 *  Your IR receiver should be connected to the pin defined here
 */
int RECV_PIN = 11; 

IRrecv irrecv(RECV_PIN);

decode_results results;

void setup()
{
  Serial.begin(115200);
  irrecv.enableIRIn(); // Start the receiver
}


void dump(decode_results *results) {
  // Dumps out the decode_results structure.
  // Call this after IRrecv::decode()
  int count = results->rawlen;
  if (results->decode_type == UNKNOWN) {
    Serial.print("Unknown encoding: ");
  }
  else if (results->decode_type == DENON) {
    Serial.print("Decoded DENON: ");
  }
  else if (results->decode_type == DISH) {
    Serial.print("Decoded DISH: ");
  }
  else if (results->decode_type == SAMSUNG) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == SHARP) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == ONKYO) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == APPLE) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == BOSEWAVE) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == LEGO_PF) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == MAGIQUEST) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == MAGIQUEST) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == NEC) {
    Serial.print("Decoded NEC: ");
  }
  else if (results->decode_type == SONY) {
    Serial.print("Decoded SONY: ");
  }
  else if (results->decode_type == RC5) {
    Serial.print("Decoded RC5: ");
  }
  else if (results->decode_type == RC6) {
    Serial.print("Decoded RC6: ");
  }
  else if (results->decode_type == PANASONIC) {
    Serial.print("Decoded PANASONIC - Address: ");
    Serial.print(results->address, HEX);
    Serial.print(" Value: ");
  }
  else if (results->decode_type == LG) {
    Serial.print("Decoded LG: ");
  }
  else if (results->decode_type == JVC) {
    Serial.print("Decoded JVC: ");
  }
  else if (results->decode_type == WHYNTER) {
    Serial.print("Decoded Whynter: ");
  }
  Serial.print(" (");
  Serial.print(results->bits, DEC);
  Serial.println(" bits)");
  Serial.print("Raw (");
  Serial.print(count, DEC);
  Serial.print("): ");

  for (int i = 1; i < count; i++) {
    if (i & 1) {
      Serial.print(results->rawbuf[i]*USECPERTICK, DEC);
    }
    else {
      Serial.write('-');
      Serial.print((unsigned long) results->rawbuf[i]*USECPERTICK, DEC);
    }
    Serial.print(" ");
  }
  Serial.println();
}



void loop() {
  if (irrecv.decode(&results)) {
    Serial.println(results.value, HEX);
    dump(&results);
    irrecv.resume(); // Receive the next value
  }
}
```

