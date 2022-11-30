# Wireless Networking Setup Example for Raspberry Pi Pico W

This repository contains a demo [MicroPython](https://micropython.org/) application that can be used as a start point for any project where you want the user to be able to easily configure wifi connection on a [Raspberry Pi Pico W](https://www.raspberrypi.com/products/raspberry-pi-pico/).  The demo makes use of Pimoroni's [Phew!](https://github.com/pimoroni/phew) webserver and templating library - a copy of this is contained in this repository in the `phew` folder.

The demo works by first exposing a captive wifi access point.  The user uses a device such as their phone, tablet or laptop to connect to that access point, and is presented with a web page asking them to input their wifi network SSID and password.

These credentials are saved as a file on the Pi Pico W which then reboots and attempts to connect to the network.  If a connection to the network is made, the device runs your application.  If the supplied wifi credentials were incorrect, it goes back into access point mode and the user can try to enter updated credentials.

In this demonstration, the application that the device runs presents a simple web front end with a button on it that the user can use to toggle the Pi Pico W's onboard LED.  The user accesses the front end by browsing to the device's IP address.  When the device successfully connects to the network, it logs the IP address to the console using a `print` statement.  Ideally it should show this on a connected display so that the user knows which IP address to use in order to connect to the application's front end.  If your application doesn't rely on a web front end, then this bit of information doesn't necessarily need to be communicated to the user. 

I created this demo after reading Kevin McAleer's article about how to set up an access point with Phew! ([read on Kev's website](https://www.kevsrobots.com/blog/phew-access-point.html)).

## Shopping List

To follow along, you'll need some things that cost money, and others that you may already have or which are free:

* A laptop or desktop computer (could be a Mac, Windows or even a regular Raspberry Pi) to run a code editor on and install files to the Pi Pico W from.
* A [Raspberry Pi Pico W](https://shop.pimoroni.com/products/raspberry-pi-pico-w?variant=40059369619539) (it must be the W version, other versions don't have wifi!)
* A cable to connect the Raspberry Pi Pico W to your development machine.  It will need a micro USB connection at the Pico end, and either a USB A or C at the other end.  For example [something like this](https://shop.pimoroni.com/products/usb-a-to-microb-cable-black?variant=31241639498).  Make sure your cable provides both data and charging.  A charge only cable won't work when it comes to copying files to the Pi Pico W.
* A copy of the MicroPython runtime for the Pi Pico W.  You can download the latest .uf2 file [here](https://micropython.org/download/rp2-pico-w/rp2-pico-w-latest.uf2).  Just save it somewhere on your machine for now.
* A code editor that can connect to the Pi Pico W and copy files to it.  I use [VS Code](https://code.visualstudio.com/) with the [Pico W Go extension](https://marketplace.visualstudio.com/items?itemName=paulober.pico-w-go), you could also use [Thonny](https://thonny.org/).

## Raspberry Pi Pico W Setup

### Install MicroPython

Connect the Raspberry Pi Pico W to your machine using the USB cable.  This powers the Pi Pico W and also provides a data connection to it.  Follow the drag and drop instructions [here](https://www.raspberrypi.com/documentation/microcontrollers/micropython.html#drag-and-drop-micropython) to install MicroPython.

### Code Editor Setup

I use VS Code as my editor.  If you choose to use Thonny, configure it to work with the Pi Pico W by following the instruction in section 4.1, Using Thonny [here](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf).

If you're using VS Code install the [Pico-W-Go extension](https://marketplace.visualstudio.com/items?itemName=paulober.pico-w-go) from the marketplace ([how to browse and install extensions](https://code.visualstudio.com/docs/editor/extension-marketplace)).

Whichever editor you're using, you'll next want to clone this repository from GitHub and open it in your editor.  Here's how to do this with VS Code from the terminal on a Mac:

```bash
git clone https://github.com/simonprickett/phewap.git
cd phewap
code .
```


## Install and Run the Software on the Raspberry Pi Pico W

I'm using VS Code for this.  Whichever editor you use, you'll need to have first installed the MicroPython runtime on the Raspberry Pi Pico W (see earlier instructions).

With the folder that you cloned this repository into open in VS Code, plug the micro USB end of your cable into the Raspberry Pi Pico W and the USB A or C end of your cable into the machine that's running VS Code.

Connect to the Pi Pico W from VS Code by clicking the "Pico W Disconnected" button in the editor's footer bar.  Wait for this to change to "Pico W Connected".

Now, copy the project files to the Pi Pico W.  Click on "All Commands" in the editor's footer bar, and select "Pico-W-Go > Upload project".  This copies all of the project files to the device and resets it.  It will then start running the project.

To see the logs in VS Code's built in Terminal, click the "Pico W Disconnected" button to reconnect.

## Connect to the Access Point and Configure the Wifi

When the software first runs, it exposes a wifi access point for the user to connect to.  The access point is called "pi pico" (you can change this in the code if you like) and it doesn't require a password.  

Using a wifi capable device (your phone, tablet, another computer etc), connect to the "pi pico" wifi network.  

Your device may automatically pop up a web page served to it by the Pi Pico W.  Use the form on this page to provide your wifi network's SSID and password then click "Save".

If you don't automatically see the web page, open your device's browser and navigate to `http://pipico.net`

Here's what the page looks like on an iPhone:

![Wifi setup page](wifi_setup.jpg)

Once you hit "Save", the Pi Pico W will reset and attempt to connect to your wifi:

![Wifi configured](wifi_configured.jpg)

If it succeeds, it will log its IP address to the console (connect to the Pi Pico W from VS Code to see this).  Using any other device that's connected to the same wifi network, browse to `http://<device ip address>` to see the application home page:

![Demo application page](demo_application.jpg)

Use the "Toggle LED" button to toggle the onboard LED on the Pi Pico W board.  The application code now also has access to the internet via your wifi network.

If you made a mistake when providing your wifi credentials, the Pi Pico W will try and connect then swap back to exposing the "pi pico" access point so that you can try again.

## Code Walkthrough

TODO

## Adapt this for your own Application

TODO