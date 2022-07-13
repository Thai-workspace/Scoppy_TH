> หากคุณกำลังมองหา Scopy Oscilloscope โดย Analog Devices คุณสามารถค้นหาได้ [here](https://wiki.analog.com/university/tools/m2k/scopy/oscilloscope).

# Scoppy
Scoppy เป็นออสซิลโลสโคปและตัววิเคราะห์ลอจิกที่ขับเคลื่อนโดยโทรศัพท์/แท็บเล็ต Android และ Raspberry Pi Pico Pico วัดสัญญาณและรูปคลื่นจะแสดงบนอุปกรณ์ Android ไม่จำเป็นต้องเขียนโปรแกรมใดๆ และทั้งแอปและเฟิร์มแวร์สามารถดาวน์โหลดได้ฟรี ([เฟิร์มแวร์](https://github.com/fhdm-dev/scoppy-pico) เป็นโอเพ่นซอร์ส) การติดตั้งทำได้ง่ายมากและใช้เวลาเพียงไม่กี่นาที

เป้าหมายของโครงการ Scoppy คือการให้สามเณรอิเล็กทรอนิกส์และมือสมัครเล่นและนักเรียน STEM เข้าถึงออสซิลโลสโคปราคาถูกพิเศษซึ่งเป็นประโยชน์สำหรับการดูสัญญาณแรงดันไฟฟ้าต่ำและความถี่ต่ำ Scoppy ยังเป็นเครื่องวิเคราะห์ลอจิกด้วยอัตราการสุ่มตัวอย่าง 25MS/s

## สิ่งที่คุณต้องการ
* อุปกรณ์ Android ที่ใช้ Android เวอร์ชัน 6.0 (Marshmallow) ขึ้นไป อุปกรณ์ต้องรองรับ USB OTG (On-The-Go) ด้วย - โทรศัพท์/แท็บเล็ตที่ทันสมัยส่วนใหญ่รองรับ (หากคุณไม่เห็นแอปเมื่อเรียกดู Play Store แสดงว่าอุปกรณ์ของคุณอาจไม่รองรับคุณสมบัตินี้)
* อะแดปเตอร์/สายเคเบิล USB OTG ที่เข้ากันได้กับโทรศัพท์/แท็บเล็ตของคุณ (มีให้ในราคาไม่กี่ดอลลาร์)
* บอร์ด Raspberry Pi Pico

> สำคัญ
> โปรดใช้แอปเวอร์ชันล่าสุด (v1.018) และเฟิร์มแวร์ (v10) เฟิร์มแวร์เวอร์ชันเก่าอาจไม่ทำงานกับแอปเวอร์ชันล่าสุดและในทางกลับกัน

## Quick Start

### 1. ติดตั้งแอพ Scoppy Android
ติดตั้ง [แอป Scoppy Android](https://play.google.com/store/apps/details?id=xyz.fhdm.scoppy) จาก Play Store

### 2. ติดตั้งเฟิร์มแวร์ลงใน Pico . ของคุณ

ดาวน์โหลดเฟิร์มแวร์ลงในคอมพิวเตอร์ของคุณ มันอยู่ที่นี่: [pico-scoppy-v10.uf2](https://fhdm-dev.github.io/downloads/scoppy-pico-v10.uf2) หรือคุณสามารถ [สร้างไฟล์ uf2] (https://github.com/fhdm-dev/scoppy-pico) จากแหล่งที่มา

กดปุ่มบูทเซลบน Pico ของคุณและเชื่อมต่อกับคอมพิวเตอร์ของคุณ คัดลอกไฟล์ uf2 ไปยัง Pico ของคุณ ไฟ LED ออนบอร์ดควรเริ่มกะพริบ

### 3. เชื่อมต่อ Pico กับโทรศัพท์/แท็บเล็ตของคุณ
ต่ออะแดปเตอร์/สายเคเบิล OTG เข้ากับอินพุต USB ของอุปกรณ์ Android ปลายอีกด้านเชื่อมต่อกับสาย USB ที่คุณเชื่อมต่อกับ Pico ของคุณ เมื่อเชื่อมต่อแล้ว Android อาจขอให้คุณอนุญาตให้ Scoppy ใช้อุปกรณ์ USB

### 4. เริ่ม Scoppy!
แนบเอาต์พุต +ve ของแหล่งสัญญาณของคุณเข้ากับ GPIO26 ของ Pico และต่อกราวด์เข้ากับ gnd ซึ่งจะช่วยให้คุณสามารถวัดสัญญาณระหว่าง 0V ถึง 3.3V แน่นอนว่าแรงดันสัญญาณควรอยู่ภายในช่วงที่อนุญาตของพิน ADC ของ RP2040 ดูหัวข้อ 5.2.3 ของแผ่นข้อมูล RP2040 สำหรับข้อมูลเพิ่มเติม สำหรับช่อง 2 ให้เชื่อมต่อสัญญาณกับ GPIO27

> คุณอาจต้องการใส่ตัวต้านทานจำกัดกระแส (เช่น 100R) ระหว่างแหล่งสัญญาณและ pico ADC (GPIO26/27) เพื่อจำกัดกระแสผ่านไดโอด Pico ESD ในกรณีที่คุณใช้แรงดันไฟฟ้าที่สูงกว่า 3.3V โดยไม่ได้ตั้งใจ

หากคุณไม่มีแหล่งสัญญาณที่เหมาะสม คุณสามารถดูสัญญาณทดสอบบน GPIO 22 ได้โดยเชื่อมต่อโดยตรงกับพิน ADC (GPIO 26 และ 27) GPIO 22 เป็นคลื่นสี่เหลี่ยม 1kHz ที่มีรอบการทำงาน 50%

## ตัววิเคราะห์ลอจิก
หากต้องการใช้ Scoppy เป็นเครื่องมือวิเคราะห์ลอจิก ให้แตะปุ่มเมนู จากนั้นแตะปุ่มโหมด แล้วแตะ 'ตัววิเคราะห์ลอจิก' อินพุตตัววิเคราะห์ลอจิกคือ GPIO 6 ถึง 13 โปรดอย่าลืมใช้แรงดันไฟฟ้าระหว่าง 0 ถึง 3.3V กับพินเหล่านี้เท่านั้น

## คำแนะนำในการติดตั้งและการใช้งานโดยละเอียด
ดู[เอกสารประกอบ](https://oscilloscope.fhdm.xyz/)

## กระดานสนทนา/กระดานสนทนา
ไปที่ส่วน [การสนทนา](https://github.com/fhdm-dev/scoppy/discussions) ของที่เก็บนี้เพื่อ ... หารือเกี่ยวกับ Scoppy ตัวอย่างเช่น ถามและตอบคำถาม ให้คำติชม ขอคุณสมบัติ รายงานข้อบกพร่อง แบ่งปันการออกแบบส่วนหน้าของคุณ หรือแสดงความคิดเห็นเกี่ยวกับอะไรก็ได้ที่เกี่ยวข้องกับ Scoppy, Oscilloscopes, Logic Analyzers หรืออุปกรณ์อิเล็กทรอนิกส์โดยทั่วไป

## Measuring different voltage ranges (oscilloscope mode)
To remove the 0-3.3V input voltage limitation (and do whatever signal conditioning magic takes your fancy) you’ll need to add an [analog front end](https://oscilloscope.fhdm.xyz/wiki/Analog-Front-End). This can be as simple as a voltage divider or as complex as you want it to be. The [Documentation](https://oscilloscope.fhdm.xyz/) contains some [examples](https://oscilloscope.fhdm.xyz/wiki/Analog-Front-End-Examples) of simple and cheap AFE designs and you are encouraged to share your own front end designs and ideas with other Scoppiers. Just head to the [forum](https://github.com/fhdm-dev/scoppy/discussions).
   
[Here's](https://github.com/fhdm-dev/scoppy/discussions/63) an example of a two channel, super-cheap front end that is easy to build and uses readily available components. 

![Two channel front end](https://user-images.githubusercontent.com/52391579/174912584-056eced0-f1bc-4d36-8f70-f12cc540e6ca.jpg)

## Tips
* If the traces or grid lines look too narrow then you can change the width in Settings (tap Menu to see the Settings option)
* Long-pressing most of the control buttons will set the corresponding setting to a default value eg. long-pressing the horizontal position button will reset the horizontal position back to zero. Long-pressing the trigger level button will set the trigger level to the centre of the waveform.
* Long-pressing any of the +/- buttons will continuously change the corresponding value. The longer you press it the faster the value will change.
* Tap the GND indicator (the right pointing arrow on the left of the screen) to change the selected channel. The selected channel is the one that responds to vertical swiping/zooming and tapping the vertical scale and position buttons.


## Quirks
* If the screen turns off or the app is no longer in the foreground, the run mode will change to STOPPED (to prevent draining the battery). You will need to tap RUN to restart the scope.
* The OFF trigger mode prevents all triggering and Scoppy will set the horizonal position so that it is displaying the most recent samples (it normally tries to find a trigger point near the centre of the sample record). This in combination with a long Time/Div setting is equivalent to roll mode on many 'scopes. 

## Troubleshooting
* If your phone has a Micro-USB connecter then check that the Micro-USB plug of the OTG cable/adapter is plugged into the phone and not into the Pico!
* If the Pico doesn't seem to be connecting try the following:
    * tap STOP and then RUN
    * OR
    * unplug the USB cable and plug it back in
* If it's still not working then it's possible that your phone/tablet doesn't support USB OTG. You can test this by attaching a USB thumb drive to the OTG cable/adapter. You should be able to browse the files on the drive.
* Some diagnostic information is also writtern to the Pico UART on GPIO 0 & 1

## Specifications and features (oscilloscope)
* Max. Sampling Rate: 500kS/s (shared between channels)
* Time/Div: 5us - 20secs
* Memory depth depends on sampling rate. It ranges between 2kpts (shared between channels) and 20kpts in Run mode and up to 100kpts for Single shot captures.
* 2 channels
* Auto and Normal triggering
* Cursors
* X-Y Mode
* FFT

## Specifications (logic analyzer)
* Max. Sampling Rate: 25MS/s (per channel)
* Time/Div: 50ns - 100ms
* 8 channels

## Known Bugs
* When long-pressing the + or - buttons, moving your finger laterally will have the same effect as lifting your finger off the button. The only workaround is to keep your finger stready when long-pressing these buttons.

## Links
* [Demonstration of Scoppy](https://www.youtube.com/watch?v=8ldxmyujHK8&t=4523s) on the DroneBot Workshop channel
* Review of [Scoppy on YouTube by @Gabinete de Tecnologia](https://youtu.be/qqPxLXTxoTA)
* An article on [Hackaday](https://hackaday.com/2021/06/26/raspberry-pi-pico-oscilloscope/), including many scathing reviews in the comments section. If you hate Scoppy and/or its developer then this would be a great place to vent your anger!

## Tutorials/Experiments
* Here are [some tutorials and experiments](https://github.com/fhdm-dev/scoppy-experiments) demonstrating how to use Scoppy with a variety of circuits.

## Advertising and in-app purchase
The free (zero cost) version of the app is limited to one channel. A single banner ad may be displayed at the top of the screen. To enable the extra channel(s) and remove all advertising, a small in-app purchase is required (approx. US$1 for a yearly subscription or US$2 for a lifetime purchase - exact price depends on your location).

## Gallery
![Scoppy Oscilloscope App](images/scoppy-v2-running-2ch.jpg)
Screenshot

![Scoppy Development](images/phone-breadboard-pico-afe.jpg)
Scoppy app on a Nokia 2.1

![Scoppy Logic Analyser](images/logic-analyzer-demo.jpg)
Logic Analyzer mode

![Scoppy FFT](images/screenshot_fft-square.jpg)
FFT of a square wave

![Scoppy FFT Both Channels](images/screenshot_fft-2ch.jpg)
FFT showing both channels and the YT (scope) window

![Scoppy XY + YT](images/screenshot_xy-yt.jpg)
X-Y and YT displayed simultaneously


