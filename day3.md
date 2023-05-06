# Day 3 - Add User Actions

Edit the `[views.py](http://views.py)` file to look like this: 

```python
from django.shortcuts import render, redirect

from MyApp.models import ToDoItem

def index(request):
    context = {
        'todo_list': ToDoItem.objects.all()
    }
    return render(request, 'MyApp/index.html', context)

def do(request, id):
    todo = ToDoItem.objects.get(id=id)
    todo.done = True
    todo.save()
    return redirect('/')

def undo(request, id):
    todo = ToDoItem.objects.get(id=id)
    todo.done = False 
    todo.save()
    return redirect('/')
```

Edit the `MyApp/urls.py` to look like this:

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:id>/do/', views.do, name='do'),
    path('<int:id>/undo/', views.undo, name='undo'),
]
```

Edit the `index.html` file to look like this:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KK94CHFLLe+nY2dmCWGMq91rCGa5gtU4mk92HdvYe+M/SXH301p5ILy+dN9+nJOZ" crossorigin="anonymous">
<div class="m-4">
    {% for todo in todo_list %}
        {% if todo.done %}
            <input type="checkbox" checked onclick="location.href='/{{ todo.id }}/undo'">
        {% else %}
            <input type="checkbox" onclick="location.href='/{{ todo.id }}/do'">
        {% endif %}
        <label>{{todo.text}}</label>
        <br>
    {% endfor %}
</div>
```

After following these steps you should be able to mark the todo items as done or undone by clicking on the checkboxes!

Also, you should see the following styling changes:

*This is what the website looked like before:*

![Screenshot 2023-05-06 at 4.17.29 AM.png](png/Screenshot_2023-05-06_at_4.17.29_AM.png)

*And this is what it looks like after:*

![Screenshot 2023-05-06 at 4.17.12 AM.png](png/day3/Screenshot_2023-05-06_at_4.17.12_AM.png)