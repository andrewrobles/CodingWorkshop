# Day 1 - Make a Database

[![https://youtu.be/lcuwEj7SXvo](png/day1/day1.png)](https://youtu.be/lcuwEj7SXvo)

- Open the `MyApp` project in Visual Studio Code
- Enable auto save by going to `File > Auto Save`
- Copy the following code to `models.py`

```python
from django.db import models

class ToDoItem(models.Model):
    text = models.CharField(max_length=200)
    done = models.BooleanField(default=False)
```

- Open a terminal window by going to `Terminal > New Terminal`
- Run the following commands

```bash
python manage.py makemigrations
python manage.py migrate
```

Copy the following code to `admin.py`

```python
from django.contrib import admin

from .models import ToDoItem

admin.site.register(ToDoItem)
```

Use the app to create some todo items then observe the result

![https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/3a.png](https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/3a.png)

Convert the todo item text to something more readable by adding a `__str__` function to `models.py`

```python
from django.db import models

class TodoItem(models.Model):
    # ...
    def __str__(self):
        return self.text
```

You should see something like the following

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