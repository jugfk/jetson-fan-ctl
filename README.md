# jetson-fan-ctl
젯슨나노를 위한 오토매직 냉각팬 제어

## 요구 사항 :

### 하드웨어
이를 이해하려면 5V PWM 팬이 필요합니다.
나는 Waveshare의 Jetson Nano 5V PWM 팬을 사용했다.

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

The script will automatically run at boot time.

It's a set-it-and-forget-it type thing, unless you want to mess with the fan speeds.

## How to customize:
open /etc/automagic-fan/config.json with your favorite editor (I'm using nano):  

    sudo nano /etc/automagic-fan/config.json

you will find the following lines:

    {
    "FAN_OFF_TEMP":20,
    "FAN_MAX_TEMP":50,
    "UPDATE_INTERVAL":2,
    "MAX_PERF":1
    }

<code>FAN_OFF_TEMP</code> is the temperature (°C) below which the fan is turned off.  
<code>FAN_MAX_TEMP</code> is the temperature (°C) above which the fan is at 100% speed.  
The script interpolates linearly between these two points.

<code>UPDATE_INTERVAL</code> tells the script how often to update the fan speed (in seconds).  
<code>MAX_PERF</code> values greater than 0 maximize system performance by setting the CPU and GPU clock speeds to the maximum. 

You can use either integers (like 20) or floating point numbers (like 20.125) in each of these fields.  
The temperature precision of the thermal sensors is 0.5 (°C), so don't expect this to be too precise.

Any changes in the script will be will be applied after the next reboot.  
You can run

    sudo service automagic-fan restart

to apply changes immediately.

If you suspect something went wrong, please check:

    sudo service automagic-fan status


## 출처:
https://github.com/jetsonworld/jetson-fan-ctl/
