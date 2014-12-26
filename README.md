binary-synthesizer
==================

the is the code for my binary synthesizer, I designed, coded, and built while at parsons in NYC.

//This code uses the tone library its included with arduino 18,
//by:Bryant Davis
//created april 2010
//modified may 2010
/*
one sensor controls the primary pitch
the other controls the delay time
the binary section adds to the primary pitch
x   x  x  x  x
160 80 40 20 10
the combonation of these three things will determine the pitch heard
this is based off the theremin code by tom igoe
*/
//constants…this will be for switches
const int switchpin1=2;
const int switchpin2=3;
const int switchpin3=4;
const int switchpin4=5;
const int switchpin5=6;
const int switchpin6=7;
int buttonstate=0;//for switch 1 adds 160
int buttonstate1=0;//for switch 2 adds 80
int buttonstate2=0;//for switch 3 adds 40
int buttonstate3=0;//for switch 4 adds 20
int buttonstate4=0;//for switch 5 adds 10
void setup()
{
Serial.begin(9600);
//setup pins to read
pinMode(switchpin1,INPUT);
pinMode(switchpin2,INPUT);
pinMode(switchpin3,INPUT);
pinMode(switchpin4,INPUT);
pinMode(switchpin5,INPUT);
}
void loop()
{
// get a sensor reading:
int sensorReading = analogRead(0);
// map the results from the sensor reading’s range
// to the desired pitch range:
//originally set to 200-900
//0-1023 sounds like telephone
//20 to 20000 hz is the range of human hearing this can be changed though
int pitch1 = map(sensorReading, 0, 1023, 20, 20000);
//these control the delay time the range is from 0 to 100
int multiply=analogRead(1);
int multiplymap=(multiply, 0,1023,0,100);
//integer for the final pitch heard
int finaltone=pitch1;
//read button
buttonstate=digitalRead(switchpin1);
if(buttonstate==HIGH)
{
//add 160 to finaltone
finaltone=finaltone+160;
}
buttonstate1=digitalRead(switchpin2);
if(buttonstate1==HIGH)
{
//add 60
finaltone=finaltone+60;
}
buttonstate2=digitalRead(switchpin3);
if(buttonstate2==HIGH)
{
//add 40
finaltone=finaltone+40;
}
buttonstate3=digitalRead(switchpin4);
if(buttonstate3==HIGH)
{
//adds 20
finaltone=finaltone+20;
}
buttonstate4=digitalRead(switchpin5);
if(buttonstate4==HIGH)
{
//adds 10
finaltone=finaltone+10;
}
//add this button to turn on crazy mode
//you can control the delay time of the whole program
buttonstate5=digitalRead(switchpin6);
if(buttonstate5==HIGH)
{
crazymode=1;
}
if(buttonstate5==LOW)
{
crazymode=0;
}
// change the pitch, 10 ms duration:
//output from pin8, play this tone value, 10 ms duration
tone(8, finaltone, 10);
// delay(90);
//if crazymode is on then you have variable delay switches don’t work so good here though
if(crazymode==1)
{
delay(multiply);
}
/* for debugging
Serial.println(“analogvalue1: “);
Serial.print( sensorReading );
Serial.print(“multiply ” );
Serial.print(multiply );
Serial.print(“finaltone ” );
Serial.print(finaltone );*/
}
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
in the code you first set up constants for your switches. For example switchpin1=2; means switch 1 is on digital pin 2. Then we set up buttons states for these switches
they are all set to 0 or LOW meaning they are off. Next set up pinModes all the the switches are set up as inputs. In the Loop we are reading the values from the potentiometers and them mapping them to whatever range you want. For the first pot i mapped them to 20-20000hz which is the range of human hearing. The second pot is mapped to a range of 0-100. Then we set the buttonstates to be equal to the readings coming off the pins, if they read HIGH then we do something. Each switch has a numerical value attached to it.
IF the switch is HIGH then we add this value to the pitch.Then we check to see if the last switch is on or off. If it’s on then you are given control over the programs delay time, this will turn the sound on and off depending the on value that is read. Finally we use the tone() function , this is included with arduino 18. We tell it which pin to use for the speaker, what pitch or tone to play, then the duration or how long to play.
I have collected all the schematics and code in a zip file you can download everything here:
http://a.parsons.edu/~davib611/code/Binary_Synth.zip
here is a photo of the synth in its enclosure:
