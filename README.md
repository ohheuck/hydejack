

# Introduction

Oh-Heuck Kwon 

Student 

First grade 

Department of Electronic Engineering 

KyungHee University


> You can contact me by <kwonoh3842@khu.ac.kr> or 01097713736



## Adventure design

[![Lego color sorter](http://img.youtube.com/vi/54u4IRjY2-E/0.jpg)](https://youtu.be/54u4IRjY2-E?t=0s) 


LEGO COLOR SORTER

Prof : Jong-Han Kim   
Major : Department of Electronic Engineering   
Producer1 : Oh-Heuck Kwon   
Producer2 : Min-He Kim   
Production period : 2nd semester of 2020   

A brief introduction : We have created a machine that categorizes Lego by color and counts how many colors each have. The color sensor recognizes the color of the Lego as it passes the conveyor belt, and then counts it on the LCD monitor. After 1900 microseconds of detection, the servo motor at the end of the conveyor belt rotates left or right depending on the color and classifies the same color. We made it based on the Arduino we learned in class. And the conveyor belt is made from 3D printing.


     #include <LiquidCrystal_I2C.h>
      LiquidCrystal_I2C lcd(0x27,16,2);

     #include <Wire.h>

     #include "Adafruit_TCS34725.h"
     Adafruit_TCS34725 tcs = Adafruit_TCS34725(TCS34725_INTEGRATIONTIME_50MS, TCS34725_GAIN_4X);

     #include <Servo.h>

     Servo myservo;
     int angle = 0; 
     int buttonstate = 0;
     int lastbuttonstate = 0;
     int count = 0;
     int num1 = 0;
     int num2 = 0;
     int num3 = 0;
     void setup() {
       Serial.begin(9600);
       if (tcs.begin())
       {
         Serial.println("Found sensor");      // 디버깅 용
       }
       else
       {
         Serial.println("No TCS34725 found ... check your connections");
       }
       myservo.attach(9);
       pinMode(7,INPUT);
       lcd.begin();
       lcd.print("Lego count");
       lcd.setCursor(0,1);
       lcd.print("R.");
       lcd.setCursor(5,1);
       lcd.print("B.");
       /*
       lcd.setCursor(10,1);
       lcd.print("3.");
       */
       lcd.backlight();
     }    

     void loop() {
       buttonstate = digitalRead(7);
       if (buttonstate!= lastbuttonstate)
       {
         count++;
         lastbuttonstate = buttonstate;
       }
       if (count%4==2)
       {
           uint16_t clear, red, green, blue;
           tcs.getRawData(&red, &green, &blue, &clear);
           delay(1);
           int r = map(red,0,21504,0,1025);
           int g = map(green,0,21504,0,1025);
           int b = map(blue,0,21504,0,1025);
           delay(500);
      
           Serial.print("   R: "); 
           Serial.print(r);        // 시리얼 모니터에 빨간색 값 출력 
           Serial.print("   G: "); 
           Serial.print(g);        // 시리얼 모니터에 초록색 값 출력 
           Serial.print("   B: "); 
           Serial.println(b);      // 시리얼 모니터에 파란색 값 출력
      
           //delay(1000);
           if (r>g && r>b)
           {
             num1++;
             lcd.setCursor(2,1);
             lcd.print(num1);
             delay(1900);
             for(angle = 90; angle < 140; angle++)
             {
              myservo.write(angle);             
              delay(15);
             }
             for(angle = 140; angle >90; angle--)
             {
              myservo.write(angle);              
              delay(15);
             }


             delay(1);
           }
           /*

           else if (g>r && g>b)
           {
             num2++;
             delay(3);
             lcd.setCursor(7,1);
             lcd.print(num2);
             delay(1);
           }
           */
           else if (g>r && g>=b &&  g-r>=8 )
           {
             num2++;
             lcd.setCursor(7,1);
             lcd.print(num2);
             delay(1900);
             for(angle = 90; angle>40; angle--)
             {
               myservo.write(angle);             
               delay(15);
             }
             for(angle = 40; angle<90; angle++)
             {
               myservo.write(angle);             
               delay(15);
             }
             delay(1);
           }
       }

     }



## Embedded system design
I'm going to take a class in the third grade.



[blog]: https://hydejack.com/blog/
[portfolio]: https://hydejack.com/projects/
[resume]: https://hydejack.com/resume/
[download]: https://hydejack.com/download/
[welcome]: https://hydejack.com/
[forms]: https://hydejack.com/forms-by-example/

[features]: https://hydejack.com/#features
[news]: https://hydejack.com/#build-an-audience
[syntax]: https://hydejack.com/#syntax-highlighting
[latex]: https://hydejack.com/#beautiful-math
[dark]: https://hydejack.com/blog/hydejack/2018-09-01-introducing-dark-mode/
[search]: https://hydejack.com/#_search-input
[grid]: https://hydejack.com/blog/hydejack/

[lic]: LICENSE.md
[pro]: licenses/PRO.md
[docs]: https://hydejack.com/docs/
[ofln]: https://hydejack.com/docs/advanced/#enabling-offline-support
[math]: https://hydejack.com/docs/writing/#adding-math

[kit]: https://github.com/hydecorp/hydejack-starter-kit/releases
[src]: https://github.com/hydecorp/hydejack
[gem]: https://rubygems.org/gems/jekyll-theme-hydejack
[buy]: https://gum.co/nuOluY
[nfy]: https://app.netlify.com/start/deploy?repository=https://github.com/hydecorp/hydejack-starter-kit
[dtn]: https://www.netlify.com/img/deploy/button.svg

[gpss]: https://developers.google.com/speed/pagespeed/insights/?url=https://hydejack.com/
[hy-push-state]: https://hydecorp.github.io/hy-push-state/
[hy-drawer]: https://hydecorp.github.io/hy-drawer/
[rouge]: http://rouge.jneen.net
[katex]: https://khan.github.io/KaTeX/
[mathjax]: https://www.mathjax.org/
[tinyletter]: https://tinyletter.com/
[install]: install.md
