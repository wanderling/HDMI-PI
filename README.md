> This is an HDMI to MIPI module I recently designed, which can be used to drive various mobile phone screens as displays.

## What is the use?

Everyone knows that the current mobile phone screen quality is very high, and the price is low (after all, it is backed by the popularity of smart phones, and it is very cheap to buy as a repair accessory). Compared with most desktop monitors, it has very invincible resolution, pixel density, Viewing angle, color reproduction and even refresh rate.

Everyone knows that I have a persistent pursuit of small and exquisite electronic products, but there are almost no mini-displays made with mobile phone screens on the market, so this project is to solve this demand. As for the use of mini HDMI monitors, development boards such as TV boxes, SLR cameras, and Raspberry Pi all have HDMI interfaces. **Isn't the plug-and-play portable high-resolution screen not fragrant?**

## Hardware principle

At present, most mobile phone screens and small high-resolution and high-refresh rate screens are basically MIPI interfaces. Compared with RGB, LVDS, SPI and other interfaces, MIPI is a very powerful high-speed interface. It is divided into two specifications, CSI and DSI. (Yes, it is the DSI reserved on the Raspberry Pi), the number of lanes can be freely configured according to bandwidth requirements, and the transmission rate of each lane exceeds 1Gbps.

HDMI is the most commonly used video interface, and almost all video output devices will have an HDMI interface.。

**So what we need is a hardware module that converts HDMI to MIPI. **There are several schemes to achieve this goal, using FPGA or ASIC chip.

Here is an open source for the FPGA solution: https://hackaday.io/project/364-mipi-dsi-display-shieldhdmi-adapter

He used Spartan-6 FPGA to successfully drive the screen of iPhone4 and accept HDMI signal input. You can refer to it if you are interested.

![](/4.Docs/images/1.jpg)

Because I am not very familiar with FPGAs, I use ASIC-specific IC solutions to design.

#### Toshiba Solution

Toshiba has a TC358870XBG chip that supports 2x4lane screen driver. The input source is HDMI. This is currently a popular solution in AR glasses. The chip is very powerful, but the disadvantage is that the information is extremely scarce. ++It took me a long time to get the original datasheet and related documents, and they were all shared in the warehouse.**

I also designed a test module based on the original evaluation board, and the circuit has been open sourced in the warehouse.


![](/4.Docs/images/2.jpg)

I haven’t written the software of this program yet. Interested students can refer to the documentation for follow-up development. **Students who are progressing are also welcome to submit the code to the warehouse~**

> At present, the firmware code of Toshiba's solution has been basically implemented by [ylj2000](https://github.com/ylj2000) , and its source code has been integrated into this warehouse, thanks to the open source code of [ylj2000](https://github.com/ylj2000) students~
>
> You can go to his warehouse to learn more about:
>
> [ylj2000/HDMI_To_MIPI: A Hdmi to Mipi conversion module based on Toshiba TC358870 (github.com)](https://github.com/ylj2000/HDMI_To_MIPI)

#### Longxun solution

There is also a Longxun solution LT6911 made in China. Compared with the above solution, Longxun has a slightly weaker performance, but the chip has a built-in 51-core MCU, so it can be programmed directly on the chip (Toshiba needs an additional single-chip microcomputer with I2C Configure the chip).

The advantage of this scheme is that the cost is relatively low, and the chip peripheral circuit is more concise. The disadvantage is that the **data is less than that of Toshiba...**

Manufacturers do not open software and hard data, and do not even have a datasheet, so it is almost impossible to personally develop it. However , the omnipotent Wild Iron Man obtained some information from the agent through some special methods, including some source code (the core lib is encapsulated and I can't get it, only the upper-level API). But because I signed the NDA confidentiality agreement, it is difficult for me to share the source code part. I have open sourced the other parts except the source code. If you do DIY, you don’t need the source code. I can provide pre-compiled firmware for everyone to download. Direct copy of the project's classmates' reference.



![](/4.Docs/images/3.jpg)

![](/4.Docs/images/4.jpg)

The final driving effect is as follows, taking a 5.5-inch screen as an example:

![](/4.Docs/images/5.jpg)

## to sum up

I will continue to use this module to try to drive more screens later. Students with development ability can continue to develop on the basis of the Toshiba solution I gave. This solution will have a much higher degree of freedom, and I will continue to complete it when I have time. For this scheme: D

#### Finding information and development is not easy, remember to give the repository stars~~
