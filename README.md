# Raspberry-Pi-Voice-Assistant-Robot
This is a lab experiment designed as part of TECHIN 515 - Hardware Software Lab 2.

## Objective
In this lab, we will learn how to develop a voice assistant robot powered by ChatGPT, a state-of-the-art language model developed by OpenAI. We will configure a Raspberry Pi with the necessary hardware components and utilize OpenAI's Application programming interface (API) to enable conversational interactions with your robot... (DETAILS)
Theory on Text to Speech, and Speech to Text...

API is a way for two or more computer programs or components to communicate with each other...

## Hardware
1.	Raspberry Pi 5
2.	Power adapter for Raspberry Pi (27 Watt recommended)
3.	HDMI cable and Monitor
4.	USB Keyboard and mouse
5.	MicroSD card (16GB or larger recommended)
8.  Relay Module
9.  LED
10. Lamp (Optional)

## Software: 
1.	The Latest Raspbian Operating System: Debian Bookwarm 64-bit with desktop environment
2.	Openai platform to generate API keys

## Steps 

### Step 1: Setting up Raspberry Pi

* Download the Raspberry Pi Imager from the [official Raspberry Pi website](https://www.raspberrypi.com/software/)
* Insert the MicroSD card into your computer.
* Open Raspberry Pi Imager and choose your Raspberry Pi hardware device. Select the latest Raspbian OS from the list of available operating systems. We choose the Debian Bookwarm 64-bit with desktop environment. Select your MicroSD card as the storage location.
* Edit the OS customization settings and add your user name and password of choice
* Click "Write" and wait for the process to complete.
* Once done, eject the MicroSD card safely and insert it into your Raspberry Pi.
* Connect the monitor, keyboard, and mouse to your Raspberry Pi.
* Plug in the adapter and power on the Raspberry Pi.


### Step 2: Installing Dependencies

* Connect your Raspberry Pi to the internet.
* Open the terminal on your Raspberry Pi.

Lets check for updates and upgrades first.
```bash
sudo apt update 
sudo apt upgrade
```

We will create a separate directory for this project and install the dependencies in virtual environment. 

```bash
mkdir voice_assistant
cd voice_assistant
python -m venv env
```

This will create a virtual environment in the voice_assistant directory. We will use this directory to upload our python codes. To activate your virtual environment, we use the following command:

```bash
source env/bin/activate
```

* Now install necessary dependencies by running the following terminal commands:

```bash
sudo apt install python3-dotenv
sudo apt-get install portaudio19-dev
pip install pyaudio
sudo apt install python3-pyaudio flac python3-espeak espeak python3-dotenv
pip uninstall dotenv   (not required)
pip install python-dotenv   (not required)
pip install openai (pip install openai==0.28)
pip install SpeechRecognition
pip install pyttsx3
pip install gtts
pip install lgpio
```

### Step 3: Change default mode for audio devices 

Now plug in your USB microphone and USB speaker to the USB ports of the Raspberry Pi. We need to define these two devices as our default audio devices. Open a new terminal and run the following commands:

```bash
arecord -l 
```
You will be able to see a list of the hardware devices that are connected to your Raspberry Pi. Note the Card Number associated with your USB audio. Now we will change the card number in the default settings.

```bash
sudo nano /usr/share/alsa/alsa.conf
```
This command will take you to the default configuration, scroll down to the default section and change the "defaults.ctl.card 0" and "defaults.pcm.card 0" with your Card Number. 

### Step 4: Obtaining OpenAI API Keys

We will use the OpenAI API to generate a text response. 
•	Sign up to  OpenAI account.
•	Navigate to the API keys section and generate new API keys if you haven't already.
•	Copy the API key and save for later use in your Python script.

### Step 5: Writing Python Script
•	Create a new Python script on your Raspberry Pi using your preferred text editor.
•	Write a Python script that utilizes the OpenAI platform API keys for interacting with ChatGPT.
•	Use libraries such as openai and pyaudio to handle text-to-speech and speech recognition functionalities.
•	Implement code logic to capture audio input from the microphone, send it to the OpenAI API for processing, and play back the response through the speaker.
