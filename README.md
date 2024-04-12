# Raspberry Pi Voice Assistant
This is a lab experiment designed as part of TECHIN 515 - Hardware Software Lab 2.

## Objective
In this lab, we will learn how to develop a voice assistant powered by ChatGPT, a state-of-the-art language model developed by OpenAI. We will configure a Raspberry Pi with the necessary hardware and software components and utilize OpenAI's Application programming interface (API) to enable conversational interactions. 
Theory on Text to Speech, and Speech to Text...

API is a way for two or more computer programs or components to communicate with each other...

## Hardware
1.	Raspberry Pi 5
2.	Power adapter for Raspberry Pi (27 Watt recommended)
3.	HDMI cable and Monitor
4.	USB Keyboard and mouse
5.	MicroSD card (16GB or larger recommended)
6.  Relay Module
7. Lamp (Optional)

## Software: 
1.	The Latest Raspbian Operating System: Debian Bookwarm 64-bit with desktop environment
2.	Openai platform to generate API keys

## Steps 

### Step 1: Setting up Raspberry Pi

* Download and install the Raspberry Pi Imager from the [official Raspberry Pi website](https://www.raspberrypi.com/software/) 
* Insert the MicroSD card into your computer.
* Open Raspberry Pi Imager and choose your Raspberry Pi 5 hardware device. Select the latest Raspbian OS from the list of available operating systems. We choose the Debian Bookwarm 64-bit with desktop environment. Select your MicroSD card as the storage location (check for the storage capacity of your MicroSD card)

<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/c9aff5e8-ccee-4285-b684-da8cee67a98f" alt="Screenshot 2024-04-09 003233" width="400">

* Click "Next" and edit the OS customization settings. Here, add your username and password of choice.

<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/50042928-eb72-4cdf-898a-a446e49fd1e3" alt="Screenshot 2024-04-09 003321" width="400">



<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/bb608a93-e56f-4842-af73-f65223804da0" alt="Screenshot 2024-04-09 003602" width="400">


* Continue writing the OS into the MicroSD card and wait for the process to complete. In the meantime, you might want to go to Step 2 and obtain the OpenAI API keys to save some time! Come back to this step after you generate your OpenAI API key.
  
* Once the OS writing process is completed, eject the MicroSD card safely and insert it into your Raspberry Pi.
  
* Connect the monitor, keyboard, and mouse to your Raspberry Pi.
  
* Plug in the adapter and power on the Raspberry Pi. Check if you are automatically connected to the WiFi Network. If not, connect to a WiFi manually.

### Step 2: Obtaining OpenAI API Keys

We will use the OpenAI API to generate a text response. 
* Go to OpenAI Developer Platform API Keys Page: https://platform.openai.com/api-keys and Log in/ Sign up with your student account.
  
* Now click on "Create new secret key" and give your key a name of your choice. Create secret key and copy this key to a notepad/ text document to your computer. We will use this API key in the python script of the voice assistant.


<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/42f877a1-b4cc-4717-9657-db2d0c65b3d0" alt="Screenshot 2024-04-09 145345" width="400">

### Step 3: Build the circuit

This is an easy circuit setup, follow the diagram and connect your Raspberry Pi with the Relay Module.

Connections:
* Raspberry Pi Pin 4 (5V)       --- Relay Module VCC
* Raspberry Pi Pin 6 (GND)      --- Relay Module GND
* Raspberry Pi Pin 12 (GPIO 18) --- Relay Module IN1


<img width="600" alt="relay-pi5-circuit" src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/3fb9320b-dc6c-40e4-9dc2-ae69615ff83e">

For your reference, here is the pinout diagram of a Raspberry Pi 5. 

<img width="600" alt="Raspberry-Pi-5-Pinout" src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/ecac7728-baaf-42bd-854e-effdc7167db3">

_Pinout Diagram Reference Link: https://www.hackatronic.com/raspberry-pi-5-pinout-specifications-pricing-a-complete-guide/_

### Step 4: Installing Dependencies

* Connect your Raspberry Pi to the WiFi/ internet.
* Open the terminal on your Raspberry Pi.

Lets check for updates and upgrades first.
```bash
sudo apt update 
sudo apt upgrade
```


<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/6b15454e-0140-4f5e-8152-077514a139c7" alt="Screenshot 2024-04-09 030132" width="400">

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


<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/9ed11ccd-27b3-4e11-805e-9bff52938081" alt="Screenshot 2024-04-09 030252" width="400">

* Now install necessary dependencies by running the following terminal commands inside the virtual environment:

```bash
sudo apt install python3-dotenv
sudo apt-get install portaudio19-dev
pip install pyaudio
sudo apt install python3-pyaudio flac python3-espeak espeak python3-dotenv
pip install openai==0.28
pip install SpeechRecognition
pip install pyttsx3
pip install gtts
pip install lgpio
```

<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/c17deabf-6a26-4d69-9483-434cfacc8cb7" alt="Screenshot 2024-04-09 030635" width="400">

### Step 5: Change default mode for audio devices 

Now plug in your USB microphone and USB speaker to the USB ports of the Raspberry Pi. We need to define these two devices as our default audio devices. Open a new terminal and run the following commands:

```bash
arecord -l 
```
You will be able to see a list of the hardware devices that are connected to your Raspberry Pi. Note the Card Number associated with your USB audio (In this case, the card number is 2, yours might be different).

<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/d8285444-fd8b-4bee-b34a-acfed044d957" alt="Screenshot 2024-04-09 031129" width="400">

Now we will change the card number in the default settings.

```bash
sudo nano /usr/share/alsa/alsa.conf
```
<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/005cc619-64b1-498a-9064-76c28956dda0" alt="Screenshot 2024-04-09 030811" width="400">


This command will take you to the default configuration, scroll down to the default section and change the "defaults.ctl.card 0" and "defaults.pcm.card 0" with your Card Number. Now press ctrl + x to save the configuration. Change the modifications and press enter.


<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/9b065dd3-308e-4d1e-bae0-0cb310568186" alt="Screenshot 2024-04-09 030846" width="400">

### Step 6: Writing and Executing the Python Script
* Navigate to the voice_assistant directory from file explorer and create a new file named voice_assistant.py. Double click on the file and open it in a text editor. Now copy the **voice_assistant.py** script from here and paste it in the text editor. Make sure to replace the "KEY" with your own API key in the openai.api_key line.


<img src="https://github.com/mehrab-abrar/Raspberry-Pi-Voice-Assistant-Robot/assets/42034831/0a5d501d-3cfc-4110-88ff-83e60fe5274d" alt="Screenshot 2024-04-09 040155" width="400">

* From the terminal, navigate to the voice_assistant directory and activate your virtual environment using:

```bash
cd voice_assistant
source env/bin/activate
```

* Run the python script by executing the the following command:

```bash
python voice_assistant.py 2>/dev/null
```

* This code will keep listening for any word with the name "Tom". Say anything like "Hey Tom, .... " and the python script will convert your speech to text and send to the OpenAI API and generate a response back for you. If everything works well, you should be able to hear back a response.

* Use voice commands "Turn on the light/ Turn off the light" to control your relay.

### Takeaways from this lab experiment
* Write a Python script that utilizes the OpenAI platform API keys for interacting with ChatGPT.

* Use libraries such as openai and pyaudio to handle text-to-speech and speech recognition functionalities.

* Implement code logic to capture audio input from the microphone, send it to the OpenAI API for processing, and play back the response through the speaker.
