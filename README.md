# Raspberry-Pi-Voice-Assistant-Robot
This is a lab experiment designed as part of TECHIN 515 - Hardware Software Lab 2.

## Objective
In this lab, we will learn how to develop a voice assistant robot powered by ChatGPT, a state-of-the-art language model developed by OpenAI. We will configure a Raspberry Pi with the necessary hardware components and utilize OpenAI's Application programming interface (API) to enable conversational interactions with your robot... (DETAILS)
Theory on Text to Speech, and Speech to Text...

API is a way for two or more computer programs or components to communicate with each other...


## Hardware
1.	Raspberry Pi 3/4B 
2.	Monitor
3.	Keyboard
4.	Mouse
6.	Micro SD card 
7.	USB microphone
8.	Speaker
**
Add on: Relay modules
Add on: Lamp

## Software: 
1.	Raspbian Operating System: Legacy bullseye 64-bit with desktop environment
2.	Openai platform to generate API keys

## Steps 

### Step 1: Setting up Raspberry Pi
•	Insert the SD card with Raspbian OS into your Raspberry Pi.
•	Connect the monitor, keyboard, and mouse to your Raspberry Pi.
•	Power on the Raspberry Pi and follow the on-screen prompts to complete the setup process.




### Step 2: Installing Dependencies
•	Connect your Raspberry Pi to the internet.
•	Open the terminal on your Raspberry Pi.
•	Install necessary dependencies by running the following terminal commands:

```bash
sudo apt update 
sudo apt upgrade 
python3 -m pip install python-dotenv
sudo apt-get install portaudio19-dev
pip install pyaudio
sudo apt install python3-pyaudio flac python3-espeak espeak python3-dotenv
pip uninstall dotenv   (not required)
pip install python-dotenv   (not required)
pip install openai (pip install openai==0.28)
pip install SpeechRecognition
pip install pyttsx3
pip install gtts
```bash//  

### Step 3: Obtaining OpenAI API Keys
•	Sign up to  OpenAI account.
•	Navigate to the API keys section and generate new API keys if you haven't already
•	Copy the API key and save for later use in your Python script.

# Step 4: Writing Python Script:
•	Create a new Python script on your Raspberry Pi using your preferred text editor.
•	Write a Python script that utilizes the OpenAI platform API keys for interacting with ChatGPT.
•	Use libraries such as openai and pyaudio to handle text-to-speech and speech recognition functionalities.
•	Implement code logic to capture audio input from the microphone, send it to the OpenAI API for processing, and play back the response through the speaker.
