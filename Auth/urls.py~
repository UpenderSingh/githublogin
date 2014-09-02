from django.conf.urls import patterns, include, url
from django.contrib import admin
admin.autodiscover()

urlpatterns = patterns('',
    # Social Auth 
    url(r'^github$', 'Auth.views.github_login'),
    url(r'^github/callback$','Auth.views.github_login_callback'),   
)
