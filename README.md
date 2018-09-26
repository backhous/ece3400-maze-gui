# ECE 3400: Maze GUI

![GUI](https://github.com/{user}/{repo}/maze.gif)

## Serial API

For the third lab, you will incorporate a second Arduino into your system.  For clarity, we will refer to this as the Base Station Arduino and to the Arduino on your robot as the Robot Arduino. The Robot Arduino will communicate wirelessly with the Base Station Arduino while your robot explores a maze, sending information about the maze's layout and contents. The Base Station Arduino will communicate with the Maze GUI over a serial connection mediated by a USB cable connecting the Base Station Arduino to a PC running the Maze GUI. This document describes the interface you must implement so that the Maze GUI will understand the messages sent by the Base State Arduino.

### Message Format:

The Arduino can send a message to the GUI just as it prints data to the 
serial monitor of the Arduino IDE. For example:

`Serial.println("0,0,west=true,north=true")`

This message means that at the maze coordinates `(0, 0)` there is a wall to the
west (left) and a wall to the north (top). Maze positions are referenced using 
*raster coordinates*, so the upper left corner of the maze has coordinates
`(0, 0)`.

___The GUI will only process a message that ends with a newline.___ For this
reason, you should use `Serial.println` not `Serial.print` to send messages. 
However, the latter can be used as long as you manually insert a newline `\n` at
end of your message.

You can include as few as zero or infinitely many (not recommended for 
performance reasons) parameters after specifiying the row and column coordinates 
at the beginning of the message.

All of the following are legal messages:

`1,0,north=true`

`2,3,west=false,north=true,south=false`

`0,0,west=false,west=true`

Note that the last message sets the value of `west` twice. The GUI will only
consider the *final* value of `west` sent in the message. `true`, in this 
case.

### Parameters:
There are eight parameters you can set for each cell in the maze. Each parameter
has a limited set of allowed values. The default value is show in the following 
table. All cells start with the default value set for each parameter. For this 
reason, you do not not need to inform the GUI about the absence of walls or the 
absence of treasures, etc. Note that capitalization does not matter. The GUI will
treat all messages as lowercase.

|Parameter   |Allowed Values   |Default Value   |Description|
|---|---|---|---|
|west   |True, False   |False   |Is a wall to the west?|
|north   |True, False   |False   |Is a wall to the north?|
|east   |True, False   |False   |Is a wall to the east?|
|south   |True, False   |False   |Is a wall to the south?|
|robot   |True, False   |False   |Is another robot present?|
|tshape   |Circle, Triangle, Square, None   |None   |What shape treasure is present?|
|tcolor   |Red, Green, Blue, None   |None   |What color treasure is present?|
