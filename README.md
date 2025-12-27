# Ex.05 Design a Website for Server Side Processing
## Date:12.12.2025

## AIM:
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA:
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
```
html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Power of Lamp Filament</title>
</head>
<body>
    <h2>Calculate Power of Lamp Filament (Incandescent Bulb)</h2>

    <p><strong>Formula:</strong> P = I² × R</p>

    <form method="post">
        {% csrf_token %}
        
        <label>Intensity (I) in Amperes:</label>
        <input type="number" name="intensity" step="any" required><br><br>

        <label>Resistance (R) in Ohms:</label>
        <input type="number" name="resistance" step="any" required><br><br>

        <button type="submit">Calculate Power</button>
    </form>

    <hr>

    {% if error %}
        <p style="color:red;">{{ error }}</p>
    {% endif %}

    {% if power != None %}
        <h3>Result</h3>
        <p>Intensity (I): {{ intensity }} A</p>
        <p>Resistance (R): {{ resistance }} Ω</p>
        <h3>Power (P) = {{ power }} Watts</h3>
    {% endif %}
</body>
</html>
views
from django.shortcuts import render

# Create your views here.
def calculate_power(request):
    power = None
    intensity = None
    resistance = None
    error = None

    if request.method == "POST":
        try:
            intensity = float(request.POST.get("intensity"))
            resistance = float(request.POST.get("resistance"))

            # Formula: P = I^2 * R
            power = (intensity ** 2) * resistance

        except (TypeError, ValueError):
            error = "Please enter valid numeric values."

    return render(request, "math.html", {
        "power": power,
        "intensity": intensity,
        "resistance": resistance,
        "error": error
    })
urls
"""
URL configuration for WebServer_Project project.

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/6.0/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path
from Weserverapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('math/', views.calculate_power, name='calculate_power'),
]
```

## SERVER SIDE PROCESSING:


## HOMEPAGE:


## RESULT:
The program for performing server side processing is completed successfully.
