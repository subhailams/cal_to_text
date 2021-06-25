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
import pyttsx3


speaker = pyttsx3.init()


def say_tasks(tasks):
	speaker.say("Good Morning!, your tasks for today are:") # Introducing the task-list
	speaker.runAndWait()

	tasks = ['Learn', 'Eat', 'Play', 'Sleep']

	for task in tasks: # Speaking each task sequentially from a list
		speaker.say(task)
		speaker.runAndWait()

	speaker.say("Have a good day!")

```

Yah!! Now we have a function to say tasks. Lets move on to get tasks from your calendar

## Steps to create Google Console Application

Goto this link and complete the steps https://developers.google.com/calendar/api/quickstart/python

Complete Below Steps
1. https://developers.google.com/workspace/guides/create-project#create_a_new_google_cloud_platform_gcp_project
2. https://developers.google.com/workspace/guides/create-project#enable-api
3. https://developers.google.com/workspace/guides/create-credentials#configure_the_oauth_consent_screen
4. https://developers.google.com/workspace/guides/create-credentials#create_a_oauth_client_id_credential

Download json file of credential from here https://developers.google.com/workspace/guides/create-credentials#create_a_oauth_client_id_credential
Don't forget to publish your app here https://developers.google.com/workspace/guides/create-credentials#configure_the_oauth_consent_screen

Now Copy below code and paste in new file called quickstart.py

https://github.com/googleworkspace/python-samples/blob/master/calendar/quickstart/quickstart.py

Authorize the App in your Browser

```
def get_tasks_from_calendar():
    # source: https://developers.google.com/calendar/quickstart/python
    """Shows basic usage of the Google Calendar API.
    Prints the start and name of the next 10 events on the user's calendar.
    """
    creds = None
    # The file token.pickle stores the user's access and refresh tokens, and is
    # created automatically when the authorization flow completes for the first
    # time.
    # If modifying these scopes, delete the file token.pickle.
    SCOPES = ['https://www.googleapis.com/auth/calendar.readonly']
    if os.path.exists('token.pickle'):
        with open('token.pickle', 'rb') as token:
            creds = pickle.load(token)
    # If there are no (valid) credentials available, let the user log in.
    if not creds or not creds.valid:
        if creds and creds.expired and creds.refresh_token:
            creds.refresh(Request())
        else:
            flow = InstalledAppFlow.from_client_secrets_file(
                'credentials.json', SCOPES)
            creds = flow.run_local_server(port=0)
        # Save the credentials for the next run
        with open('token.pickle', 'wb') as token:
            pickle.dump(creds, token)

    service = build('calendar', 'v3', credentials=creds)

    # Call the Calendar API
    now = datetime.datetime.utcnow().isoformat() + 'Z' # 'Z' indicates UTC time
    print('Getting the upcoming 10 events')
    events_result = service.events().list(calendarId='primary', timeMin=now,
                                        maxResults=10, singleEvents=True,
                                        orderBy='startTime').execute()
    tasks = events_result.get('items', [])
    task_list = []
    if not tasks:
        print('No upcoming tasks found.')
    for event in tasks:
        today = str(datetime.date.today())
        task_date = event['start'].get('dateTime', event['start'].get('date'))
        if today in task_date:
            task_list.append(event["summary"])

    return task_list

```

```
if __name__ == '__main__':
    tasks = get_tasks_from_calendar()
    say_tasks(tasks, name="Lucas") 
```

