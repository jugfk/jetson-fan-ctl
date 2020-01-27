# jetson-fan-ctl (Korean Version)
젯슨나노를 위한 오토매직 냉각팬 제어

![image](https://raw.githubusercontent.com/jetsonworld/jetson-fan-ctl/master/01_Images/Waveshare_4pins_PWM_Fan.png)

## 요구 사항 :

### 하드웨어
이를 이해하려면 5V PWM 팬이 필요합니다.

나는 Waveshare의 Jetson Nano 5V PWM (4PIN) 팬을 사용했다.

또한 4A 전원 공급 장치와 함께 전원 잭을 사용하는 것이 좋습니다.

### 소프트웨어
나는 여러분이 jetson nano에서 표준 이미지를 사용한다고 가정하겠습니다.

Python3은 jetson nano에 사전 설치되어 있어야합니다.  
 
(3.5 이상은 괜찮을 것입니다.)을 사용하여 이것을 확인할 수 있습니다  

<code>python3 --version</code> 

    sudo apt install python3-dev


## 설치하는 방법:
run

    ./install.sh

스크립트는 부팅시 자동으로 실행됩니다.

It's a set-it-and-forget-it type thing, unless you want to mess with the fan speeds.

## 사용자 커스터마이징하는 방법:
여러분이 좋아하는 편집기로 /etc/automagic-fan/config.json을 엽니 다 (vi를 사용하고 있습니다):  

    sudo nano /etc/automagic-fan/config.json

다음 줄을 찾을 수 있습니다 :

    {
    "FAN_OFF_TEMP":20,
    "FAN_MAX_TEMP":50,
    "UPDATE_INTERVAL":2,
    "MAX_PERF":1
    }

<code>FAN_OFF_TEMP</code> 팬이 꺼지는 온도 (° C)입니다.  
<code>FAN_MAX_TEMP</code> 팬 속도가 100 % 이상인 온도 (°C)입니다. 
스크립트는이 두 점 사이를 선형으로 보간합니다.

<code>UPDATE_INTERVAL</code> 팬 속도 (초)를 업데이트하는 스크립트에 종종 알려줍니다.  
<code>MAX_PERF</code> 0보다 큰 값은 CPU 및 GPU 클럭 속도를 최대로 설정하여 시스템 성능을 최대화합니다. 

이러한 각 필드에서 정수 (예 : 20) 또는 부동 소수점 숫자 (예 : 20.125)를 사용할 수 있습니다.  
온도센서의 온도 정밀도는 0.5(°C) 이므로 너무 정확하지는 않습니다.

스크립트를 변경하면 다음에 다시 부팅 한 후에 적용됩니다.  
당신은 실행할 수 있습니다.

    sudo service automagic-fan restart

즉시 변경 사항을 적용합니다.

무언가 잘못되었다고 의심되면 다음을 확인하십시오.

    sudo service automagic-fan status


## 출처:
https://github.com/jetsonworld/jetson-fan-ctl/
