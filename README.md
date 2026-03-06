import streamlit as st
import datetime
import webbrowser
import speech_recognition as sr
import pyttsx3
import openai

openai.api_key = "YOUR_API_KEY"

engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def ask_ai(question):
    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[{"role": "user", "content": question}]
        )
        return response.choices[0].message.content
    except:
        return "AI service unavailable"

def process_command(command):
    command = command.lower()

    if "time" in command:
        return datetime.datetime.now().strftime("Current time: %H:%M")

    elif "date" in command:
        return datetime.datetime.now().strftime("Today is %d %B %Y")

    elif "open youtube" in command:
        webbrowser.open("https://youtube.com")
        return "Opening YouTube"

    elif "open google" in command:
        webbrowser.open("https://google.com")
        return "Opening Google"

    else:
        return ask_ai(command)

def voice_input():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        st.write("Listening...")
        audio = recognizer.listen(source)

    try:
        command = recognizer.recognize_google(audio)
        return command
    except:
        return "Sorry, I couldn't understand"

st.title("🎓 AI Student Voice Assistant")

st.write("Ask questions, give commands, or use voice.")

user_input = st.text_input("Type your question")

if st.button("Send"):
    response = process_command(user_input)
    st.write("**Assistant:**", response)
    speak(response)
    
if st.button("🎤 Speak"):
    command = voice_input()
    st.write("**You said:**", command)

    response = process_command(command)
    st.write("**Assistant:**", response)

    speak(response)
