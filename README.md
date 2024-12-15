# Ex.05 Design a Website for Server Side Processing
# Date:24.10.2024
# AIM:
To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side.

# FORMULA:
P = I2R
P --> Power (in watts)
 I --> Intensity
 R --> Resistance

# DESIGN STEPS:
## Step 1:
Clone the repository from GitHub.

## Step 2:
Create Django Admin project.

## Step 3:
Create a New App under the Django Admin project.

## Step 4:
Create python programs for views and urls to perform server side processing.

## Step 5:
Create a HTML file to implement form based input and output.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
views.py
```
from django.shortcuts import render

def lamp(request):
    context={}
    context['Power'] = ""
    context['I'] = ""
    context['R'] = ""
    if request.method == 'POST':
        print("POST method is used")
        I = request.POST.get('Intensity','')
        R = request.POST.get('Resistence','')
        print('request=',request)
        print('Intensity=',I)
        print('Resistence=',R)
        Power = int(I) * int(I) * int(R)
        context['Power'] = Power
        context['I'] = I
        context['R'] = R
        print('Power=',Power)
    return render(request,'Calculation.html',context)
```
calculation.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Incandescent Bulb Power Calculator</title>
    <style>
        /* Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: #1e1e2f;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #f5f5f5;
        }

        .container {
            background: linear-gradient(135deg, #3a3a66, #1e1e2f);
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.5);
            width: 100%;
            max-width: 400px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .container:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.7);
        }

        h1 {
            text-align: center;
            font-size: 24px;
            color: #ffcc29;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            font-size: 16px;
            display: block;
            color: #ffcc29;
            margin-bottom: 8px;
        }

        input {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            border: 1px solid #444;
            border-radius: 8px;
            background-color: #2e2e4d;
            color: #fff;
            transition: border-color 0.3s ease, background-color 0.3s ease;
        }

        input:focus {
            border-color: #ffcc29;
            background-color: #3a3a66;
        }

        .btn {
            width: 100%;
            padding: 12px;
            background-color: #ffcc29;
            color: #1e1e2f;
            font-size: 18px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease;
            margin-top: 15px;
        }

        .btn:hover {
            background-color: #ffd966;
        }

        .result-box {
            background-color: #2e2e4d;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            color: #ffcc29;
            border: 1px solid #444;
        }

        .footer {
            margin-top: 20px;
            text-align: center;
            font-size: 12px;
            color: #aaa;
        }

        .footer a {
            color: #ffcc29;
            text-decoration: none;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Incandescent Bulb Power Calculator</h1>
    <form method="POST">
        {% csrf_token %}
        <div class="form-group">
            <label for="intensity">Enter Intensity (I) in Amperes:</label>
            <input type="text" id="intensity" name="Intensity" value="{{I}}" placeholder="Enter intensity" required>
        </div>
        <div class="form-group">
            <label for="resistance">Enter Resistance (R) in Ohms:</label>
            <input type="text" id="resistance" name="Resistence" value="{{R}}" placeholder="Enter resistance" required>
        </div>
        <button type="submit" class="btn">Calculate</button>
        <div class="result-box">
            <label for="power">Power:</label>
            <input id="power" name="Power" value="{{ Power}} Watts" readonly>
        </div>
    </form>
</div>

<div class="footer">
    <p>&copy; 2024 Power Calculator. All rights reserved</p>
</div>

</body>
</html>

```
css
```

body {
    font-family: Arial, sans-serif;
    background-color: #f9f9f9;
    margin: 0;
    padding: 20px;
}
.container {
    max-width: 500px;
    margin: 50px auto;
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
h1 {
    text-align: center;
    color: #333;
}
label {
    display: block;
    margin: 10px 0 5px;
    font-weight: bold;
}
input[type="number"] {
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
}
button {
    width: 100%;
    background-color: #4CAF50;
    color: white;
    padding: 10px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
}
button:hover {
    background-color: #45a049;
}
.result-box {
    background-color: #e1f5e1;
    padding: 20px;
    border-radius: 10px;
    margin-top: 20px;
    text-align: center;
    font-size: 20px;
    font-weight: bold;
    color: #333;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}
-->
```
settings.py
```
"""
Django settings for web project.

Generated by 'django-admin startproject' using Django 5.1.4.

For more information on this file, see
https://docs.djangoproject.com/en/5.1/topics/settings/

For the full list of settings and their values, see
https://docs.djangoproject.com/en/5.1/ref/settings/
"""

from pathlib import Path

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent


# Quick-start development settings - unsuitable for production
# See https://docs.djangoproject.com/en/5.1/howto/deployment/checklist/

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'django-insecure--7=y4$$9z5sq&l8=^pd3elzj&31jn6o63vj2$cszyivhe#rdn%'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = []


# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'web.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'web.wsgi.application'


# Database
# https://docs.djangoproject.com/en/5.1/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}


# Password validation
# https://docs.djangoproject.com/en/5.1/ref/settings/#auth-password-validators

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]


# Internationalization
# https://docs.djangoproject.com/en/5.1/topics/i18n/

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/5.1/howto/static-files/

STATIC_URL = 'static/'

# Default primary key field type
# https://docs.djangoproject.com/en/5.1/ref/settings/#default-auto-field

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

```
urls.py
```
from django.contrib import admin
from django.urls import path
from app import views
urlpatterns = [
    path('admin/',admin.site.urls),
    path('PowerOfLampFilamentInAnIncandescentBulb/',views.lamp),#,name="PowerOfLampFilamentInAnIncandescentBulb"
    path('',views.lamp,name="PowerOfLampFilamentInAnIncandescentBulb")
]
```


# SERVER SIDE PROCESSING:
![web3](https://github.com/user-attachments/assets/048a40b2-4f33-4454-af78-23e7597b61a2)

# HOMEPAGE:
![web4](https://github.com/user-attachments/assets/c1078a5d-9ee6-44d5-8823-2a3602332ec0)

# RESULT:
The program for performing server side processing is completed successfully.
