
# RobotC Study Guide

## Loops and Conditionals
- While:
    `while (condition) {}`
    -    Repeats code inside brackets until condition is false
    -    Condition:
        -    ex: 1 == 1, SensorValue(button) == 1
-    If:    
`if (condition)`
    - Runs code inside brackets if condition is true
-  If/Else:
```
if (condition) // if red
{

} else if (condition) // if blue
{

} else if (condition) // if green
{

} else { // runs when everything else is false

}
```

## Variables

- Variables:
    - int:
        -  whole numbers +/-
    - bool:
        -  true/false
    - float:
        -  decimal numbers
-  type name = value;
    - int count = 0;
    - count = count + 10;
    - max = count;

### Loop Using Variables
- I want to loop a flashing LED 5 times
```
int count = 0;
while (count < 5) {

    // TURN LED OFF AND ON
    count = count + 1;
}
```

## Functions
```
void LEDOn();
task main()
{
    // START OF CODE STUFF
    turnLEDOff(green);
    LEDOn(); // Call function
    turnLEDOff(green);
    LEDOn();
}

void LEDOn() // Define function
{
    wait(2);
    turnLEDOn(green);
    startMotor(left);
}
```
- Pattern to follow:
    1. Declaration: tell computer the function exists (must exist before task main)
    2. Call: tell the computer to run that code
    3. Define: what code to run

## Keywords and Methods
- To turn on a motor:
    - `startMotor(motorName, speed); // speed ranges from +127 to -127`
- To stop a motor:
    - `stopMotor(motorName);`
- Wait for a set amount of time:
    - `wait(seconds);`
- Wait until bump switch is pressed
    - `untilBump(name);`
- Wait until potentiometer value is > 100
    - `untilPotentiometerGreaterThan(100, name);` 
- Set servo to go to a specific position:
    - `setServo(servoName, position); // position ranges between +127 to -127`
- To get the value of a sensor:
    - `SensorValue(sensorName);`
    - examples:
        - `int distance = SensorValue(sonar);`
        - `if (SensorValue(sonar) > 10) {}` 

## Curly Brackets
- Curly brackets are used to group a block of code
```
while (true)
{
    turnLEDOn(green);
    startMotor(leftMotor, 63);
}
setServo(servo, 120);
```

```
if (SensorValue(bumpSwitch) == 1)
{
    turnLEDOn(green);
    startMotor(leftMotor, 63);
} else 
{
    setServo(servo, 120);
}
```

## Timers
- If you want to toggle an LED for 20 seconds
    - There are 4 internal timers titled T1, T2, T3, T4
    - Timers count in milliseconds (add 3 zeros)\
```
task main()
{
    ClearTimer(T1); // resets timer to 0
    while (time1(T1) < 20000) {
        turnLEDOn(green);
        wait(0.5);
        turnLEDOff(green);
        wait(0.5);
    }
}
```

## Boolean Operators
|Symbol| Definition | Example |
|--|--|--|
| && | AND | true && false: **false** |
| == | Equal to | 1 == 1: **true**, 1 == 2: **false** |
| != | Not equal to | 1 != 1: **false**, 1 != 5: **true**|
| \|\| | OR | true \|\| false: **false**, true \|\| true: **true** 

- \>: GREATER THEN
- <: LESS THEN
- \>=: GREATER THEN OR EQUAL TO
- <=: LESS THEN OR EQUAL TO

## Code Examples
- Variables & Timers:
```
// Create a program to add 1 to a counter variable once a second for 20 seconds
task main()
{
    int counter; // declare counter variable
    ClearTimer(T1); // resets timer to 0
    while (time1(T1) < 20000) // run for 20 seconds
    {
        counter = counter + 1; // Add one to counter
        wait(0.5); // wait 1 second so we only loop once a second
    }
}
```
- [Functions](#Functions)
- While If Else
```
// Create a program that if the sonar sensor value is high (far away)
// while the bump switch is held the LED will turn on
task main()
{
    while (true) // infinite loop
    {
        while (SensorValue(bumpSwitch) == 1) // Loops while bump switch is pressed
        {
            if (SensorValue(sonar) > 50)
            {
                turnLEDOn(green);
            }
            else
            {
                turnLEDOff(green);
            }
        }
    }
}
```

> Written with [StackEdit](https://stackedit.io/).
