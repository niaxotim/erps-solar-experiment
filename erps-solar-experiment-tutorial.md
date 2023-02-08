### @activities true
### @explicitHints true

# ERPS STEM WEEK :: Solar Experiment

## Introduction
### Introduction Step @unplugged
We've been thinking about where the electricity comes from to power our homes, our school, and our kit!  
  
In this tutorial, can you write some simple code to track our solar power storage, and turn a device on and off?

![Solar kit](https://raw.githubusercontent.com/niaxotim/erps-solar-experiment/master/assets/solar.png)

## Seeing the charge on our micro:bit
### Step 1
It would be good if we could see how much charge we have stored in our solar store (*capacitor*) on our micro:bit.  

We can, in fact, show this as a graph using our LEDs!  In our ``||basic:forever||`` block, drag a ``||led:plot bar graph of 0 up to 0||`` block.

#### ~ tutorialhint
```blocks
basic.forever(function () {
    led.plotBarGraph(
    0,
    0
    )
})
```

### Step 2
We need to read the charge level, and this is conected to PIN0 - drag a ``||pins:analog read pin P0||`` block in to the first '0' space in our graph plot.  
  
The value coming from our solar store is an analog signal, hence using this block.  
  
The *range* of numbers that can come from our store is between 0 and 1023, so chang the second '0' to read '1023'.
#### ~ tutorialhint
```blocks
basic.forever(function () {
    led.plotBarGraph(
    pins.analogReadPin(AnalogPin.P0),
    1023
    )
})
```

## Sending data to our computer
### Step 3
Seeing the charge on our micro:bit is cool, but what if we could send that data to our computer as well, and
see a real-time chart?!  Well, we can!

Drag a ``||serial:serial write line ""||`` block underneath our graph block. This *writes* data back to our computer.

#### ~ tutorialhint
```blocks
basic.forever(function () {
    led.plotBarGraph(
    pins.analogReadPin(AnalogPin.P0),
    1023
    )
    serial.writeLine("")
})

```

### Step 4
Our block for writing data to our computer expects a *string*, so we need to convert our analog numbers to strings first.  

This is called *casting*. Drag a ``||text:convert 0 to text||`` block in to the string placeholder.

#### ~ tutorialhint
```blocks
basic.forever(function () {
    led.plotBarGraph(
    pins.analogReadPin(AnalogPin.P0),
    1023
    )
    serial.writeLine(convertToText(0))
})
```

### Step 5
Replace the '0' in our conversion with another ``||pins:analog read pin P0||`` block.

#### ~ tutorialhint
```blocks
basic.forever(function () {
    led.plotBarGraph(
    pins.analogReadPin(AnalogPin.P0),
    1023
    )
    serial.writeLine(convertToText(pins.analogReadPin(AnalogPin.P0)))
})
```


### Step 6
Ideally, we wouldn't get a constant stream of charge data, but maybe a new data point every second.  

Drag a ``||basic:pause||`` block under our serial write line block, and set it to 1 second (1000 milliseconds).

#### ~ tutorialhint
```blocks
basic.forever(function () {
    led.plotBarGraph(
    pins.analogReadPin(AnalogPin.P0),
    1023
    )
    serial.writeLine(convertToText(pins.analogReadPin(AnalogPin.P0)))
    basic.pause(1000)
})
```

### Step 7
Finally, we need to be able to switch our device on and off, using the energy we have stored from the sun.  

Our device is attached using Pin2, and we can use our buttons to control this. Drag a ``||input:on button A||`` block in to your editor.  

This time, we are writing a *digital* signal out, so drag a ``||pins:digital write pin P0 to 0||`` block in to your
button block, and change the pin to P2 the output to '1' - this turns our device on.

#### ~ tutorialhint
```blocks
input.onButtonPressed(Button.A, function () {
    pins.digitalWritePin(DigitalPin.P2, 1)
})
```

### Step 8
Do the same for Button B, but this time, leave the output as '0'. This turns our device off.

#### ~ tutorialhint
```blocks
input.onButtonPressed(Button.A, function () {
    pins.digitalWritePin(DigitalPin.P2, 1)
})
input.onButtonPressed(Button.B, function () {
    pins.digitalWritePin(DigitalPin.P2, 0)
})
```

### Step 9 @unplugged
Connect your second BBC micro:bit and click ``|Download|`` to transfer your code.  
  
Make sure you connect the equipment as shown in the diagram, and then let the capactor charge for a bit. Does your graph change?  

![Solar kit](https://raw.githubusercontent.com/niaxotim/erps-solar-experiment/master/assets/solar.png)


### Step 10 @unplugged
Keeping your micro:bit plugged in to your computer, you should now see a 'Show Data Simulator' button underneath the micro:bit simulator.  

When you click this, you should see the live graph of your charge data!  What happens to it when you turn your device on?  

![Solar kit](https://raw.githubusercontent.com/niaxotim/erps-solar-experiment/master/assets/charge_graph.png)



### Solar Experiment Tutorial Complete @unplugged
Great work! You've now harnessed the power of the sun to run your kit from your micro:bit!  

Way to go on getting one step closer to becoming a sustainable engineer!

![Great job](https://raw.githubusercontent.com/niaxotim/erps-solar-experiment/master/assets/great_job.png)
