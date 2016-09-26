# Getting started with the ARM mbed ecosystem

## Introduction

The purpose of this workshop is to help users get started with the ARM mbed ecosystem and tools. The entry point for the tools is [http://developer.mbed.org](https://developer.mbed.org/). There you will find mbed enabled boards, component libraries, a web-hosted IDE and all relevant documentation for the ARM mbed ecosystem. The mbed tools are designed to work on all operating systems (Linux, Mac and Windows). The tools are free and the software is available under the commercially friendly Apache 2.0 license.

In this document we are going to go over the various tools and services that make up the ARM mbed ecosystem, as well as some key code examples that demonstrate how to get started with these tools. 

Please note that there is also a [YouTube playlist for getting started with mbed](http://www.youtube.com/playlist?list=PLiVCejcvpsetJ1n9nRXzLWvE4dp4RwGOf).

This document is best viewed as a digital document. Here is a permalink to the document in case you are viewing it offline.






## mbed ecosystem overview
The mbed ecosystem covers a wide range of tools, services, example code and documentation, which help you develop hardware and software for ARM microcontrollers. The mbed Hardware Development Kit (HDK), mbed Software Development Kit (SDK) and various tools and services make up the core of the mbed ecosystem. 

### The Hardware Development Kit
The [mbed HDK](https://docs.mbed.com/docs/mbed-hardware-development-kit/en/latest/) is a collection of resources to assist in the design and development of custom hardware. The designs in the HDK provide an entry point and purposeful tradeoffs between hardware and software optimizations. The tradeoffs made in the HDK echo through the SDK and the boards in the mbed ecosystem. If you are considering making a board using the HDK please use the exact design, as changing anything in the HDK design will have an effect further up the stack in the SDK. 

The full HDK can be found here: [https://github.com/armmbed/mbed-hdk](https://github.com/armmbed/mbed-hdk). 

#### DAPLink
The reference layout files for [DAPLink](https://github.com/mbedmicro/DAPLink) can be found in the mbed HDK. DAPLink provides our solution for programming and debugging mbed-enabled microcontrollers. mbed devices plugged into a computer appear as a mass storage device, and DAPLink enables this functionality. As a result, you can drag and drop compiled binaries to the device. 

#### Other layout files
The HDK also contains a myriad of mbed reference designs. Going forward the mbed HDK is going to be the place to find the layout files for all reference designs, projects, and the like. 

### The Software Development Kit
The mbed Software Development Kit (SDK) contains all of the software that makes up the core of the mbed ecosystem. At the heart of the SDK is mbed OS, along with various peripheral, networking interface and connectivity APIs. The biggest thing to note is that all APIs are now thread safe. 

For traditional microcontroller API examples see: mbed_example
For mbed OS System examples [see here](https://developer.mbed.org/teams/mbed-os-examples/).

#### mbed OS API
mbed OS is at the core of the mbed SDK; all other APIs either use mbed OS directly or are focused on being compatible with mbed OS. The core of mbed OS is based on the Keil RTX v5 RTOS. mbed OS provides RTOS-like functionality to all other APIs in the SDK, meaning mbed OS can perform task management, which allows your software to utilize the processor efficiently, switching between tasks as needed. Threads are the primary enabler of task management. 

The mbed OS API reference [can be found here](https://docs.mbed.com/docs/mbed-os-api-reference).

#### Peripheral API
The mbed OS v5 peripheral APIs cover functionality like SPI, UART, I2C and PWM. These ‘classic’ APIs do not require the RTOS component of mbed OS to operate, though they are part of mbed OS. As a result, all the peripheral APIs are thread safe. 

The complete list of APIs [can be found here](https://docs.mbed.com/docs/mbed-os-api-reference/en/5.1/APIs/io/inputs_outputs/).

#### NSAPI
The [Network Socket API (NSAPI)](https://docs.mbed.com/docs/mbed-os-api-reference/en/5.1/APIs/communication/network_sockets/) is the base connectivity API that provides an identical socket-like interface across all IP connectivity protocols. By using the NSAPI you can use the exact same application code for Ethernet, Wifi, Cellular and so on. This means you can create your code using Ethernet, for example, and then easily switch to WiFi by adding the WiFi library and changing the NSAPI connect call - you are not heavily invested in any one technology, so you’re free to try them all.

The connect function is the only function that changes by technology. This is because Ethernet doesn't need any connectivity options, so it’s a simple call: eth.connect(), whereas WiFi requires an SSID and password, so it looks like this: wifi.connect(ssid,pw). 

#### Other APIs
APIs like Bluetooth Low Energy (BLE) have already been pulled into the mainline SDK. In the future, APIs like LoRA, Thread and NFC may also be mainlined. Until then, they are separate libraries that you can pull in as needed. 

### mbed CLI
The mbed command line interface (CLI) is the primary tool used to build mbed OS 5 projects and is at the heart of the mbed ecosystem. mbed CLI is a Python command line utility that runs on Windows, Mac OS X and Linux. Whether you want to build a project locally (mbed compile), run tests associated with a project (mbed test), or export a project to different IDEs (mbed export), mbed CLI has you covered. In addition to traditional code management, mbed CLI also works with git and Mercurial back ends, so if you want to use your code on mbed or on GitHub, everything works!

mbed CLI is the back end utility the mbed team uses internally. We have open-sourced it for public use in an effort to make the online/ <-> offline transition easier. If you would like to install mbed CLI we’ve made an How To video: 

<span class="images">[![Video tutorial](http://img.youtube.com/vi/cM0dFoTuU14/0.jpg)](https://www.youtube.com/watch?v=cM0dFoTuU14)</span>

For more information on using mbed CLI see the Handbook pages for [Blinky on mbed CLI]( https://docs.mbed.com/docs/mbed-os-handbook/en/5.1/getting_started/blinky_cli/) or the [full mbed CLI guide](https://docs.mbed.com/docs/mbed-os-handbook/en/5.1/dev_tools/cli/).

#### Going offline


To take your code from the online environment to your local computer, you can use either mbed CLI or the mbed Online Compiler:

* In mbed CLI: use the command  `mbed import http://www.link.to/your/code` Once you have your code on your computer you can use mbed CLI `mbed export` to generate project files for your code in different IDEs. 

* In the mbed Online Compiler: right click on your project and select ‘Export to IDE’. 

We recommend using the mbed CLI route, because it preserves your commit history, unlike the export from the online compiler which only exports a specific revision of your code. 

For more details, see this video: 

<span class="images">[![Video tutorial](http://img.youtube.com/vi/PI1Kq9RSN_Y/0.jpg)](https://www.youtube.com/watch?v=PI1Kq9RSN_Y)</span>

### Online resources
mbed has a large number of resources hosted online for your convenience. From the Online Compiler and developer community on developer.mbed.org, through the large number of docs on docs.mbed.com, to the forums for community support, there is something for anything you need to develop embedded systems. 

#### Documentation
The documentation section of the website is the index for all docs hosted on [http://docs.mbed.com](http://docs.mbed.com). Any user can create docs for their project and publish them. The Documentation section contains all of the docs for the official mbed APIs and relevant example code. 



#### The mbed Online Compiler
The mbed Online Compiler hosted at [developer.mbed.org/compiler](developer.mbed.org/compiler) allows you to compile and edit your projects. You can also publish your code, which makes it available to others by adding an ‘Import’ button to your project’s page. The compiler does not include a debugger, so a common use case is to start your project in the compiler and then export to an offline compiler like Keil or IAR for debugging. 



Here is a video on getting started with the mbed Online Compiler: 

<span class="images">[![Video tutorial](http://img.youtube.com/vi/L5TcmFFD0iw/0.jpg)](https://www.youtube.com/watch?v=L5TcmFFD0iw)</span>

#### The Boards page
The [Boards page](http://developer.mbed.org/platforms) contains a list of every board officially supported in the mbed ecosystem. There are links on each board’s page to add the board to your compiler, buy the board, view pinout diagrams, and install firmware updates and bug fixes. It is important that you look at the board page to learn the pin names and check for firmware updates.


If you want to compile code for a board you should go to its board page and click the Add to Compiler button. That’s it! Now when you are in the compiler you can compile code for the board you selected.
<span class="tips"> Tip: Make sure you are logged in to do this.</span>

#### Components database
[The components database](https://developer.mbed.org/components/) is a list of software libraries and reference docs for hardware peripherals and sensors. Each component has a library and code example associated with it; you can use the import functionality described above to add code and libraries for these components to your compiler. Combined with documentation, this makes it easy to begin using a part you are not familiar with. The goal of the components database is to speed up development by sharing code, so you don't have to waste time rewriting a driver that someone else has already created. 



#### Code examples
You can find code examples for existing components in the components database or by using the search function. The mbed_examples team page has great sample projects demonstrating the mbed APIs.



#### Forums
The [forum](https://forums.mbed.com/) is an excellent place to ask questions about anything and get a quick response from the community. It is mostly moderated by community members and is a source for tips, tricks and advice for all things mbed. 


## Creating an mbed account

1. Go to [https://developer.mbed.org/account/login/](https://developer.mbed.org/account/login/ ) and sign up for an account. Alternatively, you can open the `mbed.html` file that is on every mbed development board. 


1. Fill in your information. The username you choose here will be what the community sees on your code and all comments you make.
 

## Example 1 - Blinky
There are multiple ways to blink an LED. Let's explore the three main ones:

1. [Busy wait](#busy-wait)
1. [Ticker](#ticker)
1. [Threads](#thread) 

### Busy wait
Busy wait is a method that will block the processor for a period of time. This is an effective way to create time delays, but it’s rather inefficient because it wastes processor time and keeps the processor running at full power for the duration of the wait:


#include "mbed.h"

DigitalOut myled(LED1);

int main() {
    while(1) {
        myled = 1;
        // printf("LED On\r\n");
        wait(0.2);
        myled = 0;
        // printf("LED Off \r\n");
        wait(0.2);
    }
}

Notice the `printf()`; you can enable this by uncommenting the line (remove the ‘//’). Printf()s print to the terminal, so you can use them to get debug information. We recommend using [CoolTerm](http://freeware.the-meiers.org/) as it works the same on Windows, Linux and OS X. [Here is a handy video on how to use CoolTerm](https://www.youtube.com/watch?v=jAMTXK9HjfU) to connect to your board and view the printf statements. 

### Ticker 
Tickers and timers are another way of creating a time interval. These methods are somewhat better than busy wait, because they allow other code to run while you are waiting. It is even possible, though non-trivial, to sleep during the wait period: 


#include "mbed.h"
 
Ticker flipper;
DigitalOut led1(LED1);
DigitalOut led2(LED2);
 
void flip() {
    led2 = !led2;
}
 
int main() {
    led2 = 1;
    flipper.attach(&flip, 2.0); // call flip function every 2 seconds 


    // spin in a main loop. flipper will interrupt it to call flip
    while(1) {
        led1 = !led1;
        wait(0.2);
    }
}


### Thread 
Threads are the most efficient way to blink an LED. During the waiting period it is possible to take advantage of the mbed OS optimizations to automatically conserve power and deal with other tasks. While this is not the most visually appealing method, nor the simplest, it is the preferred way for large scale deployments:


#include "mbed.h"
#include "rtos.h"
 
DigitalOut led1(LED1);
DigitalOut led2(LED2);
 
void led2_thread(void const *args) {
    while (true) {
        led2 = !led2;
        Thread::wait(1000);
    }
}
 
int main() {
    //Create a thread to execute the function led2_thread
    Thread thread(led2_thread);
    //led2_thread is executing concurrently with main at this point
    
    while (true) {
        led1 = !led1;
        Thread::wait(500);
    }
}

### Blinky challenge
Now that you have gotten the LED to blink, try using a different LED. LED0-4 should be valid options on all boards. Some boards will have tri-color LEDs, so if you turn on multiple LEDs at once you can get different colors. Try turning on and off the various LEDs. Try creating a cool pattern. Try making the blink pattern random. 

## Example 2 - Button Blinky
Now that you have used a DigitalOut pin to drive the LED, let’s try using a DigitalIn pin from the button to control the application. There are two ways to read input data: we can either constantly poll the button in a busy wait, or set an interrupt to trigger when pressed. We’ll explore these methods below. 

### Busy wait button
We can wait for digital input the same way we waited for time to pass - using a `while()` loop. In the example below the digital input is  a button press, which causes the application to flash the LED and then wait for 1 second. 

In the code below you may need to change the `SW1` pin, as the button on your board may be called something else. Please refer to the pinmap on the [boards page](https://developer.mbed.org/platforms/). 


#include "mbed.h"
#include "rtos.h"
 
DigitalIn button(SW1); // Change to match your board
DigitalOut led(LED1);

#define button_press 0

int main() {
    while(1) {
        if(button_press == button){
           led = !led;
           wait(1);
       }
    }
}

In the code above we constantly poll the button to see if it has a value that matches ‘button_press’. If it matches, we toggle the LED and wait 1 second. 

`button_press` is used to denote what value the switch uses to represent the state *pushed*. Most switches are by default open (unpressed), so they will read as 0 while pressed. If you see your LED blinking without the button being pressed - try changing `button_press`  to `1`.


### Interrupt button
An alternative way to poll the button is to use an interrupt. Interrupts let you say ‘when that pin changes value, call this function’. In other words, we can tell the MCU to call a function when the button is pressed. In our case, that function toggles the LED. 


#include "mbed.h"
 
InterruptIn button(SW1);
DigitalOut led(LED1);
DigitalOut heartbeat(LED2);
 
void toggle() {
    led = !led;
}
 
int main() {
    button.rise(&toggle);  // call toggle function on the rising edge
    while(1) {           // wait around, interrupts will interrupt this!
        heartbeat= !heartbeat;
        wait(0.25);
    }
}

In the code above we have a heartbeat function that runs on LED2, which lets you see that your code is running. Then we connect an InterruptIn object to the button and set it so that when the button rises from 0 to 1 the toggle function is called; the function toggles LED1. This way we can turn the LED on and off as needed, without needing to “waste” our time waiting or actively polling an inactive button. We (or rather - the MCU) are free to move on to other things . Interrupt driven programming is one of the fundamental paradigms of microcontroller programming. 

### Button challenge
Now that you understand how to blink an LED and read button presses, try creating a game where you have to press the button when the LED is on. A successfully timed press lights up the next LED on the board (again, LED1-4 should be valid options). Think of the LEDs as levels, and to advance you have to pass the previous level. 

## Other useful things

### Firmware update
If you have a problem with an out-of-the-box board, old firmware is a common culprit. To update the firmware for your board go to the [Boards page](http://developer.mbed.org/platforms/), select your board and follow the instructions there, or view the firmware update video:

<span class="images">[![Video tutorial](http://img.youtube.com/vi/SSRCJgzeEek/0.jpg)](https://www.youtube.com/watch?v=SSRCJgzeEek)</span>
<span class="tips"> Tip: If you are experiencing trouble connecting to your mbed board, update both the target firmware and the interface chip firmware.</span>

### Blog
The blog at [http://blog.mbed.com](http://blog.mbed.com) is a useful resource for keeping up to date on the latest mbed news, events, and offerings. This is the official public information channel, so make sure to subscribe to keep up to date on the mbed ecosystem. 

#### Support email
Before you reach out to the mbed team directly, please make sure to check the forums and Google. If you are unable to answer your question through the usual means, please feel free to email [support@mbed.com](mailto:support@mbed.com) for direct contact with the team. 