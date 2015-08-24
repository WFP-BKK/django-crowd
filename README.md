django-crowd
============
Simple Atlasian CROWD authentication backend for Django with SSO support



Configuration:
==============
Put a CROWD configuration in your `settings.py`:


```
CROWD = {
    'url': 'http://your.crowd.url:port/crowd/rest',         # your CROWD rest API url
    'app_name': 'your-registered-application-name',         # appname, registered with CROWD
    'password': 'your-registered-application-password',     # correct password for provided appname
    'superuser': False,                                      # if set makes CROWD-authorized users superusers;
    'staffuser': True,                                      # Makes user Staff User
    'validation':'10.11.40.34',                             # The ipaddress the Crowd server is responding to
    'sso': False,                                           # Set to true to enable Crowd SSO
}
```


Add `crowd.CrowdBackend` in your `AUTHENTICATION_BACKENDS` settings list.
Put it first so that password are only kept in CROWD:

```
AUTHENTICATION_BACKENDS = (
    # ...
    'crowd.backends.CrowdBackend'
    'django.contrib.auth.backends.ModelBackend',
)
```


Add     'crowd.middleware.CookieMiddleware' to the Middleware 

AUTHENTICATION_BACKENDS should be first to make sure you always start with crowd authentication before falling over to
a local account.

Credits:
========

Originally written for Django v1.3 by Konstantin J. Volkov <konstantin-j-volkov@yandex.ru> at 12.07.2012

Refactored, put together and tested with Django v1.4 by Grigoriy Beziuk <gbezyuk@gmail.com> at 27.08.2012

Refactored and added SSO by Tobias Carlander <tobias.carlander@wfp.org>
