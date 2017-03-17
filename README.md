# STM32 uart-printf

## 项目说明

在开发单片机程序时，经常使用串口打印来追踪程序执行。而本方法就是讲 C语言中的 printf 函数的输出重定向到串口，即通过串口来输出打印内容。

## 使用说明

- 1、项目中包含的例子，均通过文件名来表示 STM32 的单片机型号，不同型号在代码上有一些区别。
- 2、本历程基于 STM32 官方库函数工程项目模板文件修改而来，且在 STM32L432 Nucleo-32 开发板测试成功。
- 3、为了上传方便，删除了工程项目模板文件中对 keil 和 sw4stm32 开发工具的支持，仅保留了 IAR 开发平台项目工程。

## 演示

使用 printf 函数将 MCU 的设备 ID ，flash 容量大小，封装方式打印出来，代码和结果如下：

![uart-printf](http://github.com/cyang812/STM32-uart-printf/raw/master/code.png)

![uart-printf](https://github.com/cyang812/STM32-uart-printf/raw/master/DEMO.png)


## 移植步骤

- 1、若单片机的型号与 github 库中一致，则只需要将代码克隆到本地，并将 STM32 uart-printf -> STM32L432KC 中的 Templates 替换掉 STM32库函数中的工程模板。该工程模板的路径例如：
    ```c
    D:\en.stm32cubel4\STM32Cube_FW_L4_V1.7.0\Projects\STM32L432KC-Nucleo\Templates
    ```
    STM32库函数可以在STM32官网下载，例如上述文件的下载地址为：
    [STM32CubeL4](http://www.st.com/content/st_com/en/products/embedded-software/mcus-embedded-software/stm32-embedded-software/stm32cube-embedded-software/stm32cubel4.html)

- 2、根据硬件 uart RX TX 的连线情况，在 main.h 中修改对应的 GPIO 管脚。

- 3、若单片机的型号与 github 库中不一致，则可参考库中如下几个文件中的函数进行移植：
    ```c
    main.c  -> USART2_UART_Init(); + PUTCHAR_PROTOTYPE{}
    main.h  -> /* Definition for USARTx clock resources */
    stm32l4xx_hal_msp.c -> HAL_UART_MspInit();
    ```
