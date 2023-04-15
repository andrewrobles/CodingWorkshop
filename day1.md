#  DAY 1 - LOG IN TO THE DATABASE

#### Step 1 - Set Up Your Computer for Building Apps

##### DOWNLOAD THE REQUIRED SOFTWARE

- Git - [git-scm.com/downloads](https://git-scm.com/downloads)
- Visual Studio Code - [code.visualstudio.com](https://code.visualstudio.com)

- ONLY if you are using Windows: Install Python from the Windows store

##### ENABLE AUTO-SAVE

In order to prevent you from having to manually save the files every time you make a change, let's enable *Auto-Save* so your changes will be saved automagically.

- Open Visual Studio Code
- Enable auto save by going to `File > Auto Save`

##### RUN YOUR APP FOR THE FIRST TIME

In a terminal window, run the following commands to download the project to your `Desktop` folder:

  ```bash
  cd ~/Desktop
  git clone https://github.com/andrewrobles/MyApp.git
  ```

- Open up the project in Visual Studio Code by going to `File > Open` and navigating to `~/Desktop/MyApp`
- Open up a terminal window by going to `Terminal > New Terminal`
- Depending on if you're using Mac or Windows, run the following command under the section of whichever type of computer you're using:
- If you are using a Mac:
```bash
python3 -m venv VirtualEnvironment 
```
-  If you are using Windows:
```bash
python -m venv VirtualEnvironment 
```
- Run the following commands:
```bash
source VirtualEnvironment/bin/activate
pip install -r requirements.txt
python manage.py migrate
```
- Now this is where the magic happens... are you ready? Run the following command:
```bash
python manage.py runserver
```
- Open the URL in a browser window provided in the terminal output - http://127.0.0.1:8000
- You should see the following:
  ![NOT FOUND](png/day1/1a.png)

Congratulations, you're officially an app developer ;)

#### Step 2 - Create An Account and Log In

##### INITATE ACCOUNT CREATION PROCESS

```bash
python manage.py createsuperuser
```

##### PROVIDE ACCOUNT CREDENTIALS

```
Username: andrew
Email address: me@andrewrobles.com
Password: **********
Password (again): *********
Superuser created successfully.
```

##### UTILIZE WEBSITE TO LOGIN

With the server running, open `http://127.0.0.1:8000/admin` and login using the username and password you entered in the previous step.

#### Step 3 - Store Information In App Database

##### COPY TO `models.py`

```python
from django.db import models

class ToDoItem(models.Model):
    text = models.CharField(max_length=200)
    done = models.BooleanField(default=False)
```

##### RUN IN TERMINAL

```bash
python manage.py makemigrations
```

##### OBSERVE THE RESULT

```
Migrations for 'todo':
  todo/migrations/0001_initial.py
    - Create model TodoItem
```

##### RUN IN TERMINAL

```bash
python manage.py migrate
```

##### OBSERVE THE RESULT

```
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, todo, sessions
Running migrations:
  Rendering model states... DONE
  Applying todo.0001_initial... OK
```

##### COPY TO `admin.py`

```python
from django.contrib import admin

from .models import TodoItem

admin.site.register(TodoItem)
```
##### USE APP TO CREATE SOME TO-DO ITEMS THEN OBSERVE THE RESULT 

![added](png/day1/3a.png)

##### CONVERT TO-DO ITEM TEXT TO SOMETHING MORE READABLE BY ADDING A `__str__` FUNCTION TO `models.py`


```python
from django.db import models

class TodoItem(models.Model):
    # ...
    def __str__(self):
        return self.text
```

##### OBSERVE THE RESULT

![NOT FOUND](png/day1/3b.png)

#### Step 4 - Customize How Text is Displayed

Using the app, edit the to-do item and click on the checkbox to mark it as done.

![NOT FOUND](png/day1/4a.png)

Now, we are going to write some code so that any items marked as done are crossed out. Let’s update the contents of `MyApp/models.py` to:

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

![NOT FOUND](png/day1/4b.png)