# NTOES

## args and kwargs

```*args``` => gets value of generalized arguments

```**kwargs``` => gets keyword of the generalized arguments

e.i.:

```py
    def adder(*num):
        sum = 0

        for n in num:
            sum = sum + n

        print("Sum:",sum)
```

```py
    adder(3,5)
    adder(4,5,6,7)
    adder(1,2,3,5,6)
```

```py
    def concatenate(**words):
        result = ""
        for arg in words.values():
            result += arg
        return result

    print(concatenate(a="Real", b="Python", c="Is", d="Great", e="!"))
```

```py
    $ python concatenate_keys.py
    abcde
```

## import views to urls

-litteraly use the example in the file and it works
-decide towards one ```home_view```

```py
    from pages.views import home_view
```

## URL patterns

-```anything/``` leads yoou to ```x/anything```
-create as many views  as needed (home, about, contact pages...)

at urls.py

```py
    path('', home_view, name='home')
    path('home/', home_view,)
```

at views.py

```py
    def home_views(request, *args, **kwargs):
        print(args,kwargs)
        print(request.user)
        return ('<h1></h1>')
```

### using render to call a html doc

-create ```templates``` folder alongside the project folders

```py
    def home_views(request, *args, **kwargs):
        print(args,kwargs)
        print(request.user)
        return render(request, "home.html", {}) 
```

#### Making it OS independent

-add template dir in settings.py  

```py
TEMPLATES = [
    'DIRS': [os.path.join(BASE_DIR, "templates")]
]
```

## content blocks and extending

-use ```extent``` do link html files and ```block content``` to pass code to other pages as nedded
-makesure there's space before and after closing the ```{% block %}```

at ```about.html``` (```{% block content1 %}``` is being refered  in ```home.html``` file)

```html
    {% extend "base.html" %}

    {% block content1 %}
    <p>
    {{ my_text }}, {{ my_number }}
    </p>
    {% endblock content1 %}
```

at ```views.py```

```py
    def about_views(request, *args, **kwargs):
        my_content = {
            "my_text": "Hey there ho there hi there"
            "my_number": 69  
        }
```

### looping in a template

-let's pass a py list and make it a html list
-use ```forloop.counter``` to set a counter

```html
    {% for sub_item in my_list %}

            {% if sub_item ==  12 %}
            <li>{{ forloop.counter }}{{ sub_item|add:22 }} </li>

            {% elif sub_item >= 42 %}
            <li>{{ forloop.counter }}{{ sub_item|add :22 }} </li>
            {% else %}
            <li>{{ forloop.counter }}{{ sub_item|add:22 }} </li>

            {% endif %} 
    {% endfor %}
```

at ```views.py```

```py
    def about_views(request, *args, **kwargs):
        my_content = {
            "my_list" = [12,123,12312]
        }
```

### other template tags and filters

-make use of ```|``` to filter out some of the contents (capfirts, upper, safe(makes sure html is redered as such, even if in string format), etc.)
-stacking is possible by adding another ```|``` to your block's content

this will capitalize the first letter in the string

```html
{{ my_item|striptags|slugify }}
```

beep
