##### Some necessarily need to be added to new project. 

Don't have time find on the internet.

I'm too old to remember.

### INIT.

```shell
gcl git@github.com:bboyadao/django_template.git proj_name \ 
&& cd proj_name  \
&& rm -rf .git
&& git init

poetry install
```
### SETTINGS.
```python

ALLOWED_HOSTS = ["*"]

AUTH_APPS = [
    "rest_framework_simplejwt.token_blacklist",
    "oauth2_provider",
    "rest_framework.authtoken",
    "dj_rest_auth",
    "dj_rest_auth.registration",
    "allauth",
    "allauth.account",
    "allauth.socialaccount",
    "allauth.socialaccount.providers.facebook",
    "allauth.socialaccount.providers.google",
]

DOCS_APPS = ["drf_spectacular",
             "drf_spectacular_sidecar"]

CELERY_APPS = ["django_celery_results",
               "django_celery_beat"]

LIB_APPS = ["rest_framework",
            "django_filters",
            "phonenumber_field",
            "corsheaders",
            "fcm_django",
            "actstream",
            ]

EXTERNAL_APPS = LIB_APPS + CELERY_APPS + AUTH_APPS + DOCS_APPS
INTERNAL_APPS = []
INSTALLED_APPS += EXTERNAL_APPS + INTERNAL_APPS
```