# aiVoiceAssistant

Overview
This project demonstrates the creation of an AI assistant using Python's speech recognition library, allowing users to interact with their computer through voice commands. The assistant can perform tasks like playing songs on YouTube, retrieving information from Wikipedia, providing responses to greetings, and more.

The integration with an Arduino board enhances the project by enabling voice-controlled hardware actions. The AI assistant can turn on and off LEDs connected to the Arduino board using voice commands.

Features
Voice recognition and synthesis using the speech_recognition and pyttsx3 libraries.
Interaction with web services: playing songs on YouTube using pywhatkit and fetching information from Wikipedia.
Responding to greetings with random and context-appropriate replies.
Integration with an Arduino board for voice-controlled hardware actions.
Ability to turn on and off LEDs connected to the Arduino using voice commands.
Getting Started
Clone this repository to your local machine.
Install the required Python libraries using pip install -r requirements.txt.
Connect an Arduino board to your computer.
Review the code and comments:
Note that lines 21 to 34 and lines 302 to 309 are commented out since they require an Arduino board connection.
Modify the Arduino port on line 309 if needed (arduino = serial.Serial('COM4', 9600)).
Usage
Run the assistant.py script.
The AI assistant will greet you and wait for your voice commands.
Try saying "play a song," "tell me about X," "what's the time," or other predefined commands.
To interact with the Arduino, uncomment lines 21 to 34 and lines 302 to 309, and ensure your Arduino is connected.
Requirements
Python 3.x
speech_recognition
pyttsx3
pywhatkit
wikipedia
serial (for Arduino communication)
Contributions
Contributions are welcome! If you have any suggestions or improvements, feel free to create an issue or submit a pull request.
