# jarvis-music-player
virtual assistant music player using python 3

"""
inputs are text based
"""

import pyttsx3
imprt os
import random
from pathlib import Path

def speak(text):    # Speak func that speak passed text/audio parameter
    # voice setup
    engine = pyttsx3.init()
    engine.setProperty('rate', 170)  # setting up new voice rate
    engine.setProperty('volume', 0.8)  # setting up volume level  between 0 and 1
    voices = engine.getProperty('voices')  # getting details of current voice
    engine.setProperty('voice', voices[0].id)  # changing index, changes voices. o for male
    # system speak
    engine.say(text)  # capture text
    engine.runAndWait()
    engine.stop()

def listen():  # temporary user input
    user_speak = input(":")   # get user input 
    return user_speak.lower()

def get_music(title):  # look for .mp3 files in main dir and sub-dir
    music_path = Path('raw path') # raw path = root directory(e.g. music folder)
    songs = []
    for root, dirs, files in os.walk(music_path):
        for entry in files:
            if entry.endswith(".mp3"):
                music_entry = os.path.join(root, entry)
                songs.append(music_entry)
    if title == "none":
        os.startfile(random.choice(songs))
    else:
        for entry in songs:
            if title in entry.lower():
                os.startfile(entry)
    songs.clear()
    
music_request = ["music", "sound", "songs", "sing"] # any phrase that relates to the command
for phrase in music_request:
    if phrase in user_said:
        speak("Sir do you have any request or do you want me to pick for you")
        user_said = listen()
        music_random_pick = ['pick', 'choose', 'anything', 'do it', 'no', 'none']
        for reply in music_random_pick:
            if reply in user_said:
                get_music("none")
            else:
                get_music(user_said)
    
