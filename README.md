import speech_recognition as sr
import random
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import serial
import time





engine = pyttsx3.init()

"""
#This code is only when you have an arduino

arduino = serial.Serial('COM4', 9600)  # Replace with your port and baud rate

def turn_on_leds():
    arduino.write(b'1')  # Send command to turn on LEDs
    print("Turning on LEDs")
    talk("Turning on LEDs")

def turn_off_leds():
    arduino.write(b'0')  # Send command to turn off LEDs
    print("Turning off LEDs")
    talk("Turning off LEDs")
"""

time.sleep(2)
print("waiting")

print("starting now")
listener = sr.Recognizer()


responses = [
    "I'm doing well, thank you!",
    "I'm great, thanks for asking.",
    "I'm feeling pretty good today.",
    "I'm excellent, how about you?",
    "I'm fine, how's your day going?",
    "I'm good, just busy with some stuff.",
    "I'm doing alright, thanks.",
    "I'm okay, thanks for checking in.",
    "I'm hanging in there, how about you?",
    "I'm not too bad, thanks.",
    "I'm pretty fantastic, actually.",
    "I'm decent, thanks for asking.",
    "I'm better than I was yesterday.",
    "I'm feeling positive today.",
    "I'm in a pretty good mood.",
    "I'm doing just fine, thanks.",
    "I'm content, how's your day treating you?",
    "I'm doing well, all things considered.",
    "I'm managing, thank you.",
    "I'm on the up and up, how about you?",
    "I'm doing pretty well overall.",
    "I'm alright, thanks for caring.",
    "I'm surviving the day, how about you?",
    "I'm quite happy, thanks for asking.",
    "I'm doing fine, thanks for checking up on me.",
    "I'm in a positive state of mind.",
    "I'm feeling energetic and good.",
    "I'm holding up, how about yourself?",
    "I'm coping, thanks.",
    "I'm feeling pretty relaxed today.",
    "I'm doing good, how about your day?",
    "I'm in a decent place right now.",
    "I'm pretty content with things.",
    "I'm feeling better than yesterday, thanks.",
    "I'm okay, just taking it one step at a time.",
    "I'm doing well, and you?",
    "I'm quite alright, thanks.",
    "I'm feeling optimistic today.",
    "I'm doing fine, considering the circumstances.",
    "I'm pretty cheerful, thanks for asking.",
    "I'm steady and balanced right now.",
    "I'm hanging in there, how about you?",
    "I'm feeling calm and collected.",
    "I'm doing well, can't complain.",
    "I'm managing, thanks for your concern.",
    "I'm feeling upbeat and positive.",
    "I'm alright, thanks for your thoughtfulness.",
    "I'm in a good place mentally.",
    "I'm doing fine, and you?",
    "I'm feeling better today, thank you.",
    "I'm alright, just taking things as they come.",
    "I'm feeling pretty content, how about you?",
    "I'm doing well, thanks for asking.",
    "I'm holding up, thanks for checking in.",
    "I'm feeling pretty steady and stable.",
    "I'm doing good, how's everything on your end?",
    "I'm in a positive frame of mind.",
    "I'm coping well, thank you.",
    "I'm feeling relatively relaxed today.",
    "I'm alright, and you?",
    "I'm doing well, thanks for your consideration.",
    "I'm feeling upbeat and optimistic.",
    "I'm alright, just working through things.",
    "I'm feeling pretty decent today.",
    "I'm doing good, thanks for asking.",
    "I'm managing fine, how about you?",
    "I'm feeling balanced and composed.",
    "I'm in a positive state, thanks.",
    "I'm alright, and yourself?",
    "I'm doing well, appreciate your concern.",
    "I'm feeling optimistic and cheerful.",
    "I'm holding up well, thank you.",
    "I'm feeling pretty calm and collected.",
    "I'm doing good, how's your day treating you?",
    "I'm alright, thanks for checking up on me.",
    "I'm feeling relatively relaxed and content.",
    "I'm managing alright, how about you?",
    "I'm feeling positive and hopeful.",
    "I'm doing well, and you?",
    "I'm in a decent place emotionally.",
    "I'm alright, thanks for your kindness.",
    "I'm feeling pretty steady today.",
    "I'm doing good, thanks.",
    "I'm managing, and you?",
    "I'm feeling upbeat and energetic.",
    "I'm holding up, how's everything going?",
    "I'm feeling pretty balanced and composed.",
    "I'm alright, thanks for asking.",
    "I'm doing well, and yourself?",
    "I'm feeling positive and optimistic.",
    "I'm doing good, appreciate your thoughtfulness.",
    "I'm alright, just taking each moment as it comes.",
    "I'm feeling relatively calm and collected.",
    "I'm doing well, how about you?",
    "I'm managing fine, thanks for asking.",
    "I'm feeling upbeat and content.",
    "I'm holding up well, and you?",
    "I'm feeling pretty stable and composed.",
    "I'm alright, thanks for your consideration.",
    "I'm doing good, how about yourself?"
]


def respond_to_greeting(greeting):
    if greeting.lower() in greeting_responses:
        possible_responses = greeting_responses[greeting.lower()]
        selected_response = random.choice(possible_responses)
        return selected_response
    else:
        return random.choice(default_responses)


greeting_responses = {
    "hello": [
        "Hello!",
        "Hi there!",
        "Hey!",
        "Greetings!",
        "How's it going?"
    ],
    "hi": [
        "Hello!",
        "Hey there!",
        "Hi!",
        "Greetings!",
        "How's it going?"
    ],
    "hey": [
        "Hey!",
        "Hi there!",
        "Hello!",
        "Howdy!",
        "How's it going?"
    ],
    "how are you": [
        "I'm just a computer program, but I'm here to help!",
        "I don't experience emotions, but I'm ready to assist you.",
        "I'm functioning perfectly and at your service.",
        "I'm here and ready to assist you with anything you need.",
        "I'm an AI, so I'm always ready to help you out."
        # ... (more AI responses)
    ],

    "what's up": [
        "Not much, just here to assist you!",
        "I'm here and ready for your questions.",
        "Just hanging out in the digital realm!",
        "Ready and waiting to help you!",
        "Just processing data and answering queries."
        # ... (more AI responses)
    ],
    "hey there": [
        "Hello!",
        "Hi!",
        "Hey!",
        "Greetings!",
        "How can I assist you today?"
        # ... (more AI responses)
    ]
    # Add more greetings and responses here
}

trigger_phrases = ['wikipedia', 'get me info on', 'search', 'find out', 'who is', 'what is']

default_responses = [
    "I'm not quite sure what to say to that.",
    "I'm not familiar with that topic, but I'm here to help.",
    "That's an interesting question. Let me think...",
    "Hmm, I'm not sure I have the answer to that right now.",
    "I'm still learning and might not have an answer for that.",
    "I'm processing, but I don't have a response just yet.",
    "I'm here to assist, even if I don't have an immediate answer.",
    "Your question got me thinking. Give me a moment.",
    "I'm a work in progress and don't have all the answers.",
    "I'm still learning the ropes, so bear with me.",
    "I'm here to learn and grow, just like our conversation.",
    "I'm not equipped to handle that question at the moment.",
    "I'm still learning the nuances of human language.",
    "I'm here to help, even if I'm not entirely certain.",
    "I'm an AI in training, and some questions stump me.",
    "I don't have all the answers, but I'm eager to assist.",
    "I'm here to provide information, but I'm not infallible.",
    "I'm working on expanding my knowledge, but I'm not there yet.",
    "I might not have that information in my database.",
    "I'm an AI assistant, and some things still perplex me.",
    "I'm not equipped with all possible answers, but I'll try my best.",
    "I'm here to assist, even if I can't always respond perfectly.",
    "Your question challenges my programming a bit.",
    "I'm still honing my skills and don't have a definitive answer.",
    "I'm learning as we go, and your question is thought-provoking.",
    "That's an interesting question. Let's explore it together."
    # ... (more alternative responses)
]
def talk(text):
    engine.say(text)
    engine.runAndWait()


def youtube_song(command):

    index_of_play = command.find("play")

    # Extract the text after "play"
    song = command[index_of_play + len("play"):].strip()
    pywhatkit.playonyt(song)
    print(f"The song you asked me to play was {song}\n")
    talk(f"Playing {song}")
    print(f"Playing {song}")






def take_command():
    try:
        with sr.Microphone() as source:
            print("listening...")
            voice = listener.listen(source)
            command = listener.recognize_google(voice)

    except:
        talk("You have not given me any instructions, going back to hibernation!")

    return command
def run_alexa():
    command = take_command()
    if "how are you" in command.lower():
        # random_index = random.randint(0, len(responses) - 1)
        # selected_response = responses[random_index]
        # print(selected_response)
        random_response = random.randint(0, 99)
        words = "So, what can i help you with?"
        response = responses[random_response]
        talk(f"{response} {words}")


    if "play" in command:
        youtube_song(command)

    if "time" in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk(f"Its currently {time}")

    if any(phrase in command.lower() for phrase in trigger_phrases):
        # Perform your Wikipedia query here
        matched_trigger = next((phrase for phrase in trigger_phrases if phrase in command.lower()), None)
        querry = command.replace(matched_trigger, "").strip()

        talk("Searching...")

        try:

            info = wikipedia.summary(querry, 1)
            talk(f"Here is what i found. {info}")
            print(f"here is what i found on wikipedia {info}")
        except:
            print(f"No wikepedia pages found on {querry}")
"""
# This code is only when you have an arduino

    if "turn on led" in command.lower() or "on" in command.lower() or "lights on" in command.lower():
        turn_on_leds()
    elif "turn off led" in command.lower() or "turn off" in command.lower() or "off" in command.lower():
        turn_off_leds()
"""



while True:
    run_alexa()

