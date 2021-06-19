Please Follow Below Steps

## Download Python
1. [Download Python](https://www.python.org/downloads/)
2. Ensure pip is installed with pip --version if not [install pip](https://pip.pypa.io/en/stable/installing/#installing-with-get-pip-py)

```
python -m pip install --upgrade pip 
```

## Python Text to Speech App 

Open command prompt and install below package

```
pip install pyttsx3
```

## Create a new python file Eg: speak.py

```
import pyttsx3

text = "Hello World of Audio!"

speaker = pyttsx3.init()
speaker.say(text)
speaker.runAndWait()

```

Goto Command Prompt and run below

```
python speak.py
```

## Explore more voice options


```
voices = speaker.getProperty("voices") # Getting the available voices
print("Printing Voices")
print("There are ", len(voices), " options")
```

Try different voices by changing the number Eg: voices[3]

Add Below code to speak.py

```
speaker.setProperty("voice",voices[1].id) # Setting a nicer voice than default
speaker.say(text)
speaker.runAndWait()
```

## Make program to list your tasks

```
speaker.say("Good Morning!, your tasks for today are:") # Introducing the task-list
speaker.runAndWait()

tasks = ['Learn', 'Eat', 'Play', 'Sleep']

for task in tasks: # Speaking each task sequentially from a list
	speaker.say(task)
	speaker.runAndWait()

speaker.say("Have a good day!")
```

## Module the above code and keep it as a function say_tasks(tasks)

```
def say_tasks(tasks):
	speaker.say("Good Morning!, your tasks for today are:") # Introducing the task-list
	speaker.runAndWait()

	tasks = ['Learn', 'Eat', 'Play', 'Sleep']

	for task in tasks: # Speaking each task sequentially from a list
		speaker.say(task)
		speaker.runAndWait()

	speaker.say("Have a good day!")

```

## Yah!! Now we have a function to say tasks. Lets move on to get tasks from your calendar

Goto this link and complete the steps https://developers.google.com/calendar/api/quickstart/python

