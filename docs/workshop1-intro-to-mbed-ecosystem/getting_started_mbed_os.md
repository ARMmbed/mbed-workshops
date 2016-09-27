# First applications with mbed OS

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

```
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
```

Notice the `printf()`; you can enable this by uncommenting the line (remove the ‘//’). Printf()s print to the terminal, so you can use them to get debug information. We recommend using [CoolTerm](http://freeware.the-meiers.org/) as it works the same on Windows, Linux and OS X. [Here is a handy video on how to use CoolTerm](https://www.youtube.com/watch?v=jAMTXK9HjfU) to connect to your board and view the printf statements. 

### Ticker 
Tickers and timers are another way of creating a time interval. These methods are somewhat better than busy wait, because they allow other code to run while you are waiting. It is even possible, though non-trivial, to sleep during the wait period: 

```
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

```

### Thread 
Threads are the most efficient way to blink an LED. During the waiting period it is possible to take advantage of the mbed OS optimizations to automatically conserve power and deal with other tasks. While this is not the most visually appealing method, nor the simplest, it is the preferred way for large scale deployments:

```
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
```

### Blinky challenge
Now that you have gotten the LED to blink, try using a different LED. LED0-4 should be valid options on all boards. Some boards will have tri-color LEDs, so if you turn on multiple LEDs at once you can get different colors. Try turning on and off the various LEDs. Try creating a cool pattern. Try making the blink pattern random. 

## Example 2 - Button Blinky
Now that you have used a DigitalOut pin to drive the LED, let’s try using a DigitalIn pin from the button to control the application. There are two ways to read input data: we can either constantly poll the button in a busy wait, or set an interrupt to trigger when pressed. We’ll explore these methods below. 

### Busy wait button
We can wait for digital input the same way we waited for time to pass - using a `while()` loop. In the example below the digital input is  a button press, which causes the application to flash the LED and then wait for 1 second. 

In the code below you may need to change the `SW1` pin, as the button on your board may be called something else. Please refer to the pinmap on the [boards page](https://developer.mbed.org/platforms/). 

```
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
```

In the code above we constantly poll the button to see if it has a value that matches ‘button_press’. If it matches, we toggle the LED and wait 1 second. 

`button_press` is used to denote what value the switch uses to represent the state *pushed*. Most switches are by default open (unpressed), so they will read as 0 while pressed. If you see your LED blinking without the button being pressed - try changing `button_press`  to `1`.


### Interrupt button
An alternative way to poll the button is to use an interrupt. Interrupts let you say ‘when that pin changes value, call this function’. In other words, we can tell the MCU to call a function when the button is pressed. In our case, that function toggles the LED. 

```
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
```

In the code above we have a heartbeat function that runs on LED2, which lets you see that your code is running. Then we connect an InterruptIn object to the button and set it so that when the button rises from 0 to 1 the toggle function is called; the function toggles LED1. This way we can turn the LED on and off as needed, without needing to “waste” our time waiting or actively polling an inactive button. We (or rather - the MCU) are free to move on to other things . Interrupt driven programming is one of the fundamental paradigms of microcontroller programming. 

### Button challenge
Now that you understand how to blink an LED and read button presses, try creating a game where you have to press the button when the LED is on. A successfully timed press lights up the next LED on the board (again, LED1-4 should be valid options). Think of the LEDs as levels, and to advance you have to pass the previous level. 

