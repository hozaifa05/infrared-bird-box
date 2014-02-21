Infrared Bird Box
=================

A bird box with a Raspberry Pi infrared camera inside

[![image](./images/cover.jpg)](http://www.gardman.co.uk/wild-bird-care "Wild Bird Care | Gardman")

This project will not only teach you about electronics and programming but can help support the bird population in your area.  Having a camera inside a nesting box can be tremendously rewarding, however with the Raspberry Pi you can share the nesting box with the world by video streaming the content to the Internet.  Watch as your birds gain their own Internet following!

This resource will walk you through the technical hurdles to allow you to have a working live webcam inside your bird box.  However it does not cover the DIY challenges required to protect your equipment from the elements.  Overcoming those is your own responsibility and will be quite a fun and motivating activity in its own right.

##Lesson objective
* place holder

##Lesson outcome
*	place holder

##Time
*	2-3 hours

##Requirements
*	Raspberry Pi
*	Micro USB power adapter
*	An SD Card with Raspbian already set up through NOOBS
*	USB Keyboard
*	USB Mouse
*	HDMI cable
*	Ethernet cable
*	LAN with Internet connection
*	A Monitor or TV
*	Raspberry Pi NoIR Camera Board - has a **black** circuit board (try [CPC](http://cpc.farnell.com/jsp/search/productdetail.jsp?sku=SC13223 "RPI NOIR CAMERA BOARD - RASPBERRY-PI"))
*	**Female** to **Female** jumper wires, at least 3 (try [Pimoroni](http://shop.pimoroni.com/collections/components "Components - Pimoroni"))
*	220 Ohm Resistor, get several in case of breakages (try [Pimoroni](http://shop.pimoroni.com/collections/components "Components - Pimoroni"))
*	Infrared LED 5mm 890nm, get several in case of breakages (try [RS](http://uk.rs-online.com/web/p/ir-leds/6997663/ "Buy IR LEDs Infrared LED 5mm 890nm"))
* Bird Box (try [B&Q](http://www.diy.com/nav/garden/pet-bird-care/bird-care/nesting_boxes/Gardman-Wild-Bird-Nest-Box-9374965 "Gardman Wild Bird Nest Box"))

##Optional extras
If you want to be able to turn the Infrared LED on and off in code.
* ULN2003 Transistor Array (try [RS](http://uk.rs-online.com/web/p/darlington-transistors/6868209 "Buy Darlington Transistors ULN2003"))
* Breadboard (try [Pimoroni](http://shop.pimoroni.com/products/solderless-breadboard-830-point "Solderless Breadboard - 830 point - Pimoroni"))
*	**Male** to **Female** jumper wires, at least 3 (try [Pimoroni](http://shop.pimoroni.com/collections/components "Components - Pimoroni"))

##Introduction

To begin with pupils should appreciate that garden birds are very choosy about where they build their nest.  The bird box will need to be located out of any predator's reach, away from any prevailing winds and nowhere near a bird table or feeder.

Once a bird has moved in the box must not be disturbed until they have finished breeding (usually between October and January in the UK).  If something goes wrong you can't just open the box and fiddle with your wires or adjust the camera as this will traumatise the birds and could cause eggs or hatchlings to be abandoned.

A requirement of the system is to see the birds in total darkness.  A light inside the bird box could attract insects and predators and therefore no birds would select it as a nesting site.  It is possible though to illuminate the inside of the bird box with a kind of light that is invisible to animals and humans but *is* visible to a camera. This is commonly known as night vision.  Night vision works by using a spectrum of light called [Infrared](http://en.wikipedia.org/wiki/Infrared "Infrared - Wikipedia, the free encyclopedia") which has a longer wavelength than visible light.  Notice that IR is to the right hand side of the visible spectrum of light below.

![image](./images/spectrum.jpg "Electromagnetic spectrum")

Take this night vision surveillance camera below for example.  Around the camera lens there are lots of infrared LEDs (light emitting diodes).  These emit infrared light which will then bounce off various objects and return to the camera lens allowing it to create an image.

![image](./images/surveillance.jpg "Surveillance camera")

The image will look black and white (greyscale) though because there are no wavelengths of light from the visible spectrum being detected.  However a black and white image is good enough to allow you to watch what is happening inside a bird box and it doesn't disturb or interfere with the birds in any way.

![image](./images/pinoirada.jpg "Pi NoIR camera")

Above is the special version of the Raspberry Pi camera board called Pi NoIR.  It's essentially identical the normal green camera but it has no infrared filter.  Meaning that it lets in infrared light.  This camera combined with an infrared light source will give you night vision.  It's also small and won't be too intrusive when mounted on the inside of a bird box.

## Step 1: Setting Up your Pi
First check that you have all the parts you need to get your Raspberry Pi set up and working.

- Raspberry Pi
- Micro USB power adapter
- An SD Card with Raspbian already set up through NOOBS
- USB Keyboard
- USB Mouse
- HDMI cable
- A Monitor or TV

**Activity Checklist**

1.	Place the SD card into the slot of your Raspberry Pi. It will only fit one way so be careful not to break the card. 
2.	Next connect the HDMI cable from the monitor (or TV) to the HDMI port on the Pi and turn on your monitor. 
3.	Plug the USB keyboard and mouse into the USB slots on the Pi.
4.	Plug in the micro USB power supply and you should see some text appear on your screen.
5.  When prompted to login type:

    ```
    Login: pi
    Password: raspberry
    ```

##Step 2: Setting up the Camera Board

Firstly set up the Pi NoIR camera board without touching the bird box, test it first and we'll come to putting everything into the bird box later on.  Follow the official instructions [here](http://www.raspberrypi.org/camera "Camera | Raspberry Pi") and stop once you have successfully used a few of the example commands.

If you have not done so already you can test the camera video preview using the following command.

`raspivid -t 0`

You'll notice that everything looks a little strange.  This is because you're looking at a combination of visible light and infrared light.  A quick test is to turn the lights off and aim a TV remote control at your face (just press the buttons).  You should see your face illuminated in the darkness!

Press `Ctrl - C` when you want to exit.

##Step 3: Wiring up the Infrared LED

The intention is to have a single Infrared LED illuminating the inside of the bird box to allow the Pi NoIR camera to see something.  The 890nm IR LED is an identical component to the ones found inside TV remote controls.  The only difference being that we're going to keep it on constantly to facilitate the live stream.

First check that you have all the required parts to do this.
* **Female** to **Female** jumper wires, at least 3
* 220 Ohm Resistor
* Infrared LED 5mm 890nm

You should do this with the Raspberry Pi turned off and unplugged from the mains for safety.  Use the following command to shut down the Pi.

`sudo halt`

Wait for the ACT (activity) LED to stop blinking before turning off the power.

If you've wired up an LED to the Pi GPIO pins before then please note that *this* LED needs to be done slightly differently.  An Infrared LED requires more current than the general purpose pins can provide.  It needs to be connected directly to the 5 volt supply of the Raspberry Pi with the 220 ohm resistor inline (without the resistor the current will be too high and the LED will burn out after about ten seconds).

Ensure that you have the correct type of resistor, it needs to be 220 ohms *not* 220K ohms (220 thousand).  Please refer to the [electronic colour code](http://en.wikipedia.org/wiki/Electronic_color_code "Electronic color code - Wikipedia, the free encyclopedia") system for further guidance.  This is what it the resistor should look like:

![image](./images/220ohm.JPG "220 Ohm resistor")

The diagram below shows how the LED should be wired up.  You'll notice that the LED has two legs.  One slightly longer than the other.  The longer of the two is called the **anode** and the shorter is the **cathode**.  The LED needs power to flow into the anode and out of the cathode, if you get the polarity wrong then nothing will happen.

Use the **female** to **female** jumper wires to make the following connections.

* Connect the anode (long leg) to +5 volts which is pin 2 on the Pi
* Connect the cathode (short leg) to the 220 ohm resistor
* Connect the other side of the resistor to ground which is pin 6 on the Pi

This will allow power to flow from the Pi into the LED and back to ground through the resistor.  The resistor will limit the current to about 100 mA so that the LED never burns out.

![image](./images/solderless-led.png "IR LED wiring diagram")

Next turn the Raspberry Pi back on and log in as usual.  You'll quickly notice that the LED doesn't appear to be working... *it is working*.  Your human eyes can't see it though, but the Pi NoIR camera can.  Turn on the camera preview with this command.

`raspivid -t 0`

Hold the LED in front of the camera and it will look like this:

![image](./images/ir-led.jpg "IR LED as seen by Pi NoIR camera")

If the LED does not appear to be lit then you have most likely got the polarity of the anode and cathode wrong.  Double check your wiring against the diagram above.  Try turning out the lights and aiming the LED at yourself (don't look directly into it as infrared light can still cause harm to your eyes).  You'll see from the Pi NoIR camera preview that it will illuminate you quite well.

Press `Ctrl - C` when you want to exit.

##Step 4: Adjusting the camera focus

Bird boxes tend to be quite small in size and because of this you will probably need to adjust the focus on the Pi NoIR camera.  Otherwise you're only going to see blurry images of birds.  It will depend on the bird box you have chosen however if you're using the [Gardman](http://www.diy.com/nav/garden/pet-bird-care/bird-care/nesting_boxes/Gardman-Wild-Bird-Nest-Box-9374965 "Gardman Wild Bird Nest Box") one suggested by this guide (also recommended by [British Trust for Ornithology](http://www.bto.org/ "Welcome to the BTO | BTO - British Trust for Ornithology")) then you definitely will have to adjust the camera focus.  This is because the distance from the roof of the bird box to the base is too short.

Try putting some car keys into the bird box and, with the roof open (remove the screw), hold the camera at the approximate height of the roof and see how the camera preview looks.  The keys will probably not be in focus.  Use the following command to start the camera preview.

`raspivid -t 0`

Press `Ctrl - C` when you want to exit.

The Raspberry Pi NoIR camera does have a lens that can rotate to adjust the focus however it's sold as a fixed focus camera.  The camera actually ships with three blobs of glue to hold the rotatable lens in place.  Look at the image below.  The letters *A*, *B* and *C* mark the location of the glue.

![image](./images/pi-noir-glue.jpg "Pi NoIR glue location")

To be able to rotate the lens to adjust the focus you will need to manually dig out these blobs of glue.  This is actually a lot easier than it sounds and only takes about five minutes.  You will need a sharp tool like a needle, a scalpel or a dental pick.  Doing this under a low powered microscope can also help a lot.  It's advisable to completely disconnect the camera from the Raspberry Pi when you do this.

Children should do this with adult supervision for safety, especially if a scalpel is being used.

Resign yourself to the fact that the camera will end up looking a little scruffy after you have done this, but it doesn't really matter since it's going to live on the inside of a bird box without anyone looking at it.  See below for a comparison.

![image](./images/pi-noir-before-after.jpg "Pi NoIR before and after")

Once you're satisfied that you have all of the glue out you can take a pair of tweezers and firmly grip the inner section of the camera as shown below.  You should then be able to rotate it left and right.  Carefully rotate it left a few turns.  Now reconnect the camera to the Raspberry Pi and check to see how the keys look.

You may wish to put something under the keys at this point to simulate the height of a nest, to make doubly sure that the birds will be in focus.  Once birds move in you can't come back and adjust the camera if you've got the focus wrong.

![image](./images/pi-noir-tweezers.jpg "Pi NoIR with tweezers")

Be careful not to rotate too far left otherwise the lens will actually pop out and then it can be a bit tricky to get it back in and on the thread.  If this does happen just put it back in gently and rotate right until it catches.  Once the required focus has been found you don't need to re-glue it.  It won't move on its own even if it gets a few bumps and knocks.

##Step 5: Installing the camera and LED into the Bird Box

This part of the guide is going to be quite  [Blue Peter](http://www.bbc.co.uk/cbbc/shows/blue-peter "BBC - CBBC - Blue Peter").  This is a famous children's TV show in Britain which often involves making things out of cardboard toilet rolls, sticky back plastic and empty plastic bottles.  The idea here is simply to demonstrate what has to be achieved with installing the camera and it will then be up to you to come up with a more permanent solution (a tremendously fun group activity in itself).

The following instructions are for the [Gardman](http://www.diy.com/nav/garden/pet-bird-care/bird-care/nesting_boxes/Gardman-Wild-Bird-Nest-Box-9374965 "Gardman Wild Bird Nest Box") bird box.

1.  Firstly place your finger on the roof above approximately the centre of the main body of the bird box.

    ![image](./images/bb-install-1.jpg "")
2.  Lift up the roof and place your thumb directly below your finger so that you're pinching the lid as shown.

    ![image](./images/bb-install-2.jpg "")
3.  Your thumb is now where the camera needs to be.  Take a pen and mark this spot with a cross.

    ![image](./images/bb-install-3.jpg "")
4.  Cut out a rectangle of cardboard approximately 4 cm x 2 cm and fold it over length-ways.  Use some tape to secure it to the underside of the roof so that its a few millimetres below the cross.  This is going to be used to compensate for the angle of the roof so that the camera board points directly down the middle of the bird box.

    ![image](./images/bb-install-4.jpg "")
5.  Next take the Pi NoIR camera board and slide the flex down between the roof hinge and the back wall.  Do this with the tin connectors facing away from the back wall.  If you want to you could remove the two middle staples holding the hinge in place.  This will make the flex exit the bird box more neatly.

    ![image](./images/bb-install-5.jpg "")
6.  Take some tape and put it across the top of the Pi NoIR camera board as shown.  Do not cover the camera lens.

    ![image](./images/bb-install-6.jpg "")
7.  Secure the camera in place so that the central lens is directly over the cross that you drew earlier.  The camera should sit at an angle.

    ![image](./images/bb-install-7.jpg "")
8.  Close the lid and inspect the camera angle from the side, it needs to point directly at the centre of the base.  If it doesn't look right from this point of view then go back and adjust it until you're happy.

    ![image](./images/bb-install-8.jpg "")
9.  Secure the infra LED to the underside of the roof but not too close to the camera otherwise you'll see a lot of glare on the video.  The LED can go anywhere but it can help to bend the legs by 90 degrees as shown and secure it to the roof that way.  You may also wish to blank off the end of the LED with Tipp-Ex or by filing it down with a nail file.  This will prevent any spotlight effect on the video and create a more diffuse light effect.

    ![image](./images/bb-install-9.jpg "")

###Advice 


