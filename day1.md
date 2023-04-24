# Day 1 - Create a Database

### Step 1 - Set Up Your Computer for Building Apps

### DOWNLOAD THE REQUIRED SOFTWARE

- Git - [git-scm.com/downloads](https://git-scm.com/downloads)
- Visual Studio Code - [code.visualstudio.com](https://code.visualstudio.com/)
- ONLY if you are using Windows: Install Python from the Windows store

### ENABLE AUTO-SAVE

In order to prevent you from having to manually save the files every time you make a change, let's enable *Auto-Save* so your changes will be saved automagically.

- Open Visual Studio Code
- Enable auto save by going to `File > Auto Save`

### RUN YOUR APP FOR THE FIRST TIME

In a terminal window, run the following commands to download the project to your `Desktop` folder:

```bash
cd ~/Desktop
git clone https://github.com/andrewrobles/MyApp.git
```

- Open up the project in Visual Studio Code by going to `File > Open` and navigating to `~/Desktop/MyApp`
- Open up a terminal window by going to `Terminal > New Terminal`
- Depending on if you're using Mac or Windows, run the following command under the section of whichever type of computer you're using:
- If you are using a Mac run `python3 -m venv VirtualEnvironment`
- If you are using Windows run `python -m venv VirtualEnvironment`
- Run the following commands:

```bash
source VirtualEnvironment/bin/activate
pip install -r requirements.txt
python manage.py migrate
```

- Now this is where the magic happens... are you ready? Run the following command:

`python manage.py runserver`

- Open the URL in a browser window provided in the terminal output - [http://127.0.0.1:8000](http://127.0.0.1:8000/)
- You should see the following:
    
    ![https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/1a.png](https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/1a.png)
    

Congratulations, you're officially an app developer ;)

### Step 2 - Create An Account and Log In

### CREATE ACCOUNT

- Initiate account creation process `python manage.py createsuperuser`
- Provide account credentials

```bash
Username: andrew
Email address: me@andrewrobles.com
Password: **********
Password (again): *********
Superuser created successfully.
```

### LOGIN THROUGH THE WEBSITE

With the server running, open `http://127.0.0.1:8000/admin` and login using the username and password you entered in the previous step.

### Step 3 - Store Information In App Database

- Copy the following code to `models.py`

```python
from django.db import models

class ToDoItem(models.Model):
    text = models.CharField(max_length=200)
    done = models.BooleanField(default=False)
```

- Run the following command `python manage.py makemigrations`
- You should see the following output

```bash
Migrations for 'todo':
  todo/migrations/0001_initial.py
    - Create model TodoItem
```

- Run the following command `python manage.py migrate`
- You should see the following output

```bash
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, todo, sessions
Running migrations:
  Rendering model states... DONE
  Applying todo.0001_initial... OK
```

- Copy the following code to `admin.py`

```python
from django.contrib import admin

from .models import ToDoItem

admin.site.register(ToDoItem)
```

- Use the app to create some todo items then observe the result

![https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/3a.png](https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/3a.png)

- Convert the todo item text to something more readable by adding a `__str__` function to `models.py`

```python
from django.db import models

class TodoItem(models.Model):
    # ...
    def __str__(self):
        return self.text
```

- You should see something like the following

![https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/3b.png](https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/3b.png)

### Step 4 - Customize How Text is Displayed

Using the app, edit the to-do item and click on the checkbox to mark it as done.

![https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/4a.png](https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/4a.png)

Now, we are going to write some code so that any items marked as done are crossed out. Let’s update the contents of `MyApp/models.py` to:

```python
from django.db import models
from .utils import strike

class TodoItem(models.Model):
    text = models.CharField(max_length=200)
    done = models.BooleanField(default=False)

    def __str__(self):
        if self.done == True:
            return strike(self.text)
        else:
            return self.text
```

If you go back to your list of to-do items, you should see your item crossed out because it was marked as done.

![https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/4b.png](https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/4b.png)