# Intership_-task_month2

Build a Social Media Platform using the Django web framework:
Features required:

User registration & login
User profile
Create posts
Like & comment
Friend system / follow system
Notifications
REST API
Responsive frontend
Deploy online

Install Required Tools
Install these first.
Install Python
Download:
👉 https://python.org

Install Django:
pip install django
1.Install Django
REST Framework
2.pip install 
djangorestframework
3.Install other libraries
pip install pillow
pip install channels

Create Django Project
Open terminal:
django-admin startproject social_platform
cd social_platform
Run server:
python manage.py runserver

Create Apps:

Create the apps shown in your project structure:

python manage.py startapp users
python manage.py startapp posts
python manage.py startapp friends
python manage.py startapp notifications
python manage.py startapp api

Project Structure:

Your final structure should look like this:

social_platform/
│
├── manage.py
├── requirements.txt
│
├── social_platform/
│
├── users/
├── posts/
├── friends/
├── notifications/
├── api/
│
├── templates/
├── static/
├── media/
└── tests/



User Model (users app)

users/models.py

from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    bio = models.TextField(blank=True)
    profile_pic = models.ImageField(upload_to='profiles/', blank=True)

Add in settings.py

AUTH_USER_MODEL = 'users.User'



Post Model

posts/models.py

from django.db import models
from django.conf import settings

User = settings.AUTH_USER_MODEL

class Post(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    content = models.TextField()
    image = models.ImageField(upload_to='posts/', blank=True)
    created_at = models.DateTimeField(auto_now_add=True)



    Comment & Like System
class Comment(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    text = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

class Like(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    post = models.ForeignKey(Post, on_delete=models.CASCADE)



    Friend System

friends/models.py

class FriendRequest(models.Model):
    sender = models.ForeignKey(User, related_name='sender', on_delete=models.CASCADE)
    receiver = models.ForeignKey(User, related_name='receiver', on_delete=models.CASCADE)
    accepted = models.BooleanField(default=False)


    
    Notifications

notifications/models.py

class Notification(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    message = models.CharField(max_length=255)
    created_at = models.DateTimeField(auto_now_add=True)



    1️⃣ REST API:

In api/serializers.py

from rest_framework import serializers
from posts.models import Post

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = '__all__'
12️⃣ Create Frontend

Use Bootstrap for UI.

Example template:

templates/home.html

<h1>Social Media Feed</h1>

{% for post in posts %}
<p>{{post.content}}</p>
{% endfor %}
What is this?
13️⃣ Run Migrations
python manage.py makemigrations
python manage.py migrate

Create admin:

python manage.py createsuperuser
14️⃣ Run Project
python manage.py runserver
15️⃣ Deploy Project

Deploy using:

Heroku

Railway

16️⃣ Upload Project to GitHub

Create repository on GitHub

Then run:

git init
git add .
git commit -m "Initial commit - Django Social Media Project"
git branch -M main
git remote add origin https://github.com/yourusername/social_platform.git
git push -u origin main
17️⃣ requirements.txt

Generate automatically:

pip freeze > requirements.txt



Create Complex Data Models with Relationships

Use relationships like ForeignKey, ManyToManyField, OneToOneField.

Example:

from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    author = models.ForeignKey(Author, on_delete=models.CASCADE)


    
