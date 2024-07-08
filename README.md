# Steps

1. models.py (app)

class Topic(models.Model):

    text = models.CharField(max_length=200)
    
    date_added = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
    
        return self.text

2. settings.py (project)

INSTALLED_APPS =[]

3. admin.py (app)

from .models import Topic

admin.site.register(Topic)

4. urls.py (project)

path("", include('topic.urls'))

5. urls.py (app)

from . import views

path("", views.topics, name='topics')

6. views.py (app)

def topics(request):
    
    topics = Topic.objects.order_by('date_added')
    
    context = {'topics':topics}
    
    return render(request, 'topics.html', context)
    
7. templates/topics.html (app)

<p> Topics </p>

<ul>
    
    {% for topic in topics %}
        <li> {{ topic }} </li>
    {% empty %}
        <li> No topics yet </li>
    {% endfor %}
    
</ul>


