# ECE 3400: Maze GUI

## Serial API

### Message Format:

Your "base station" Arduino will communicate with the Maze GUI over a serial 
connection mediated by the USB cable used to connect your Arduino to the PC 
running the Maze GUI, just like the serial connection used to communicate 
between your Arduino and the Arduino IDE.

The Arduino can send a message to the GUI just as it prints data to the 
serial monitor of the Arduino IDE. For example:

`Serial.println("0,0,left_wall=true,top_wall=top")`

This message means that at the maze coordinates `(0, 0)` there is a wall to the
left and a wall to the top. Maze positions are referenced using 
*raster coordinates*, so the upper left corner of the maze has coordinates
`(0, 0)`.

___The GUI will only process a message that ends with a newline.___ For this
reason, you should use `Serial.println` not `Serial.print` to send messages. 
However, the latter could be used to send multiple messages to the base station 
with a single command if you insert a new line between the messages manually.

You can include as few as zero or infinitely many (not recommended for 
performance reasons) parameters after specifiying the row and column coordinates 
at the beginning of the message.

All of the following are legal messages:

`1,0,top_wall=true`

`2,3,left_wall=false,top_wall=true,bottom_wall=false`

`0,0,left_wall=false,left_wall=true`

Note that the last message sets the value of `left_wall` twice. The GUI will only
consider the *final* value of `left_wall` send in the message, so `true` in this 
case.

### Parameters:
There are eight parameters you can set for each cell in the maze. The possible
values for each parameter is noted in brackets. The default value for a cell is 
the last value in brackets. All cells in the maze start with the default value 
for the given parameter. For this reason, you do not not need to inform the GUI
about the absence of walls or the absence of treasures.

- `left_wall [True, alse]`
- `top_wall [True, False]`
- `right_wall [True, False]`
- `bottom_wall [True, False]`
- `other_robot [True, False]`
- `treasure_shape [Circle, Triangle, Square, None]`
- `teasure_color [Blue, Green, Red, None]`
