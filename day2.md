# Day 2 - Render a Webpage

- Create a new directory inside the `MyApp` directory called `templates`
- Inside of `templates`, create a new directory called `MyApp`
- Inside of this new `MyApp` directory, create a file called `index.html` containing the following code:

<pre>
&#x7b;&#x25;&#x20;&#x66;&#x6f;&#x72;&#x20;&#x74;&#x6f;&#x64;&#x6f;&#x20;&#x69;&#x6e;&#x20;&#x74;&#x6f;&#x64;&#x6f;&#x5f;&#x6c;&#x69;&#x73;&#x74;&#x20;&#x25;&#x7d;&#xa;&#x20;&#x20;&#x20;&#x20;&#x7b;&#x25;&#x20;&#x69;&#x66;&#x20;&#x74;&#x6f;&#x64;&#x6f;&#x2e;&#x64;&#x6f;&#x6e;&#x65;&#x20;&#x25;&#x7d;&#xa;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x69;&#x6e;&#x70;&#x75;&#x74;&#x20;&#x74;&#x79;&#x70;&#x65;&#x3d;&#x22;&#x63;&#x68;&#x65;&#x63;&#x6b;&#x62;&#x6f;&#x78;&#x22;&#x20;&#x63;&#x68;&#x65;&#x63;&#x6b;&#x65;&#x64;&#x3e;&#xa;&#x20;&#x20;&#x20;&#x20;&#x7b;&#x25;&#x20;&#x65;&#x6c;&#x73;&#x65;&#x20;&#x25;&#x7d;&#xa;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x69;&#x6e;&#x70;&#x75;&#x74;&#x20;&#x74;&#x79;&#x70;&#x65;&#x3d;&#x22;&#x63;&#x68;&#x65;&#x63;&#x6b;&#x62;&#x6f;&#x78;&#x22;&#x3e;&#xa;&#x20;&#x20;&#x20;&#x20;&#x7b;&#x25;&#x20;&#x65;&#x6e;&#x64;&#x69;&#x66;&#x20;&#x25;&#x7d;&#xa;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x6c;&#x61;&#x62;&#x65;&#x6c;&#x3e;&#x7b;&#x7b;&#x20;&#x74;&#x6f;&#x64;&#x6f;&#x2e;&#x74;&#x65;&#x78;&#x74;&#x20;&#x7d;&#x7d;&#x3c;&#x2f;&#x6c;&#x61;&#x62;&#x65;&#x6c;&#x3e;&#xa;&#x20;&#x20;&#x20;&#x20;&#x3c;&#x62;&#x72;&#x3e;&#xa;&#x7b;&#x25;&#x20;&#x65;&#x6e;&#x64;&#x66;&#x6f;&#x72;&#x20;&#x25;&#x7d;
</pre>

Open the file called `views.py` and copy over the following code:

```python
from django.shortcuts import render
from MyApp.models import ToDoItem

def index(request):
    context = {
        'todo_list': ToDoItem.objects.all()
    }

    return render(request, 'MyApp/index.html', context)
```

Create a new file inside `MyApp` called `urls.py` containing the following code:

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

Open the file called `urls.py` inside the `projects` directory and edit the code to look like:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('', include('MyApp.urls')),
    path('admin/', admin.site.urls),
]
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000/) in a browser to see your rendered webpage!

![Screenshot 2023-05-06 at 3.18.35 AM.png](png/Screenshot_2023-05-06_at_4.17.29_AM.png)