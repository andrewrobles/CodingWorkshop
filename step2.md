# Step 2 - Create An Account and Log In

Run the following command to create an account
```bash
python manage.py createsuperuser
```

Enter a username and press Enter
```
Username: andrew
```

You will then be prompted for your desired email address
```
Email address: me@andrewrobles.com
```

The final step is to enter your password. You will be asked to enter your password twice, the second time as a confirmation of the first.
```
Password: **********
Password (again): *********
Superuser created successfully.
```

With the server running, open `http://127.0.0.1:8000/admin` and login using the username and password you entered in the previous step.