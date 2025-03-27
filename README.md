# Alexa 
I made an alexa using Python. Mulitple python libraries also have been used like Speechrecognition to initialize recognizer and text-to-speech engine, pyttsw for speech function, and pywhatkit for listen and process voice command.

# Code
import speech_recognition as sr
import pyttsx3
import pywhatkit

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)

def talk(text):
  engine.say(text)
  engine.runAndWait()
  
def take_command():
  command=""
  try:
    with sr.Microphone() as source:
      print('listening...')
      voice = listener.listen(source)
      command = listener.recognize_google(voice)
      command = command.lower()
      if 'alexa' in command:
        command = command.replace('alexa', '')
        print(f"Command received: {command}")
        return command
  except:
    pass
  return command
  
def run_alexa():
    command = take_command()
    print(command)

    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif command:
        talk('Please say the command again.')
        

run_alexa()
