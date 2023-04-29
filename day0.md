# Day 0 - Login to App

**Download the following software**

- Git - [git-scm.com/downloads](https://git-scm.com/downloads)
- Visual Studio Code - [code.visualstudio.com](https://code.visualstudio.com/)
- If you are using Windows, install Python from the Windows store

**Run the app**

In a terminal window (command prompt if you are using windows), run the following commands to download the project to your `Desktop` folder:

```bash
cd ~/Desktop
git clone https://github.com/andrewrobles/MyApp.git
```

If you are using Mac, run:

```bash
python3 -m venv venv
source venv/bin/activate
```

If you are using Windows, run:

```bash
python -m venv venv
venv\Scripts\activate
```

Run the following commands:

```bash
pip install -r requirements.txt
python manage.py runserver
```

Open the `http://localhost:8000` in a browser. You should see the following:

![https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/1a.png](https://github.com/andrewrobles/CodingWorkshop/raw/main/png/day1/1a.png)

- Initiate account creation process `python manage.py createsuperuser`
- Provide account credentials

```bash
Username: andrew
Email address: me@andrewrobles.com
Password: **********
Password (again): *********
Superuser created successfully.
```

With the server running, open `http://localhost:8000/admin` and login using the username and password you entered in the previous step.