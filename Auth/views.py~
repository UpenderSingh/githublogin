from httplib2 import Http
import logging
import oauth2 as oauth
from django.shortcuts import render, redirect, render_to_response
from django.http import HttpResponse, HttpResponseRedirect
from django.template import RequestContext
from django.core import signing
import json
import urllib
import cgi
import settings

# Create your views here.
def home(request):
    return render(request,"home.html")

"""
Method for Login through github
"""

def github_login(request):
    params = {
        'scope': settings.SOCIAL_AUTH_GITHUB_SCOPE,
        'client_id': settings.GITHUB_APP_ID,
        'redirect_uri': settings.SITE_URL + '/auth/github/callback'
    }
    url = "https://github.com/login/oauth/authorize?" + urllib.urlencode(params)
    return HttpResponseRedirect(url)

"""
Github social auth callback method
"""
def github_login_callback(request):
    parser = Http()
    params = {
        'client_id': settings.GITHUB_APP_ID,
        'client_secret': settings.GITHUB_API_SECRET,
        'redirect_uri': settings.SITE_URL + '/auth/github/callback',
        'code': request.GET['code'] if 'code' in request.GET else ''
    }
    response = cgi.parse_qs(urllib.urlopen( "https://github.com/login/oauth/access_token?" +\
                             urllib.urlencode(params)).read())
    headers = {'content-type': 'application/x-www-form-urlencoded'}
    resp, content = parser.request("https://api.github.com/user?access_token=" + response['access_token'][0])
    user_profile = json.loads(content) 
    return HttpResponse(json.dumps(user_profile), content_type="application/json")
    
