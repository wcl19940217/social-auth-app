# social-auth-app
python

https://django-allauth.readthedocs.io/en/latest/installation.html  

django-allauth的使用。

Social-auth-app 库的使用

1、安装
pip install social-auth-app-django
2、设置settings里面的设置
INSTALLED_APPS = (
    ...
    'social_django',
    ...
)

3、数据库
./manage.py migrate

4、设置
设置里面指定使用的账号信息等
Authentication backends
Add desired authentication backends to Django’s AUTHENTICATION_BACKENDS setting:
AUTHENTICATION_BACKENDS = (
    'social_core.backends.open_id.OpenIdAuth',
    'social_core.backends.google.GoogleOpenId',
    'social_core.backends.google.GoogleOAuth2',
    'social_core.backends.google.GoogleOAuth',
    'social_core.backends.twitter.TwitterOAuth',
    'social_core.backends.yahoo.YahooOpenId',
    ...
    'django.contrib.auth.backends.ModelBackend',
)

5、url
urlpatterns = patterns('',
    ...
    url('', include('social_django.urls', namespace='social'))
    ...
)

6、模板templates
<a href="{% url "social:begin" "google-oauth2" %}">Google+</a>
TEMPLATES = [
    {
        ...
        'OPTIONS': {
            ...
            'context_processors': [
                ...
                'social_django.context_processors.backends',
                'social_django.context_processors.login_redirect',
                ...
            ]
        }
    }
]

social_details - Get the information we can about the user and return it in a simple format to create the user instance later. On some cases the details are already part of the auth response from the provider, but sometimes this could hit a provider API.
social_uid - Get the social uid from whichever service we’re authing thru. The uid is the unique identifier of the given user in the provider.
auth_allowed - Verifies that the current auth process is valid within the current project, this is where emails and domains whitelists are applied (if defined).
social_user - Checks if the current social-account is already associated in the site.
get_username- Make up a username for this person, appends a random string at the end if there’s any collision.
create_user - Create a user account if we haven’t found one yet.
associate_user - Create the record that associated the social account with this user.
extra_data - Populate the extra_data field in the social record with the values specified by settings (and the default ones like access_token, etc).
user_details - Update the user record with any changed info from the auth service.
Some other pipelines are available for use as well, but are not included by default:
associate_by_email - Associate current auth with a user with the same email address in the DB. Obs: This pipeline entry is not 100% secure unless you know that the providers enabled enforce email verification on their side, otherwise a user can attempt to take over another user account by using the same (not validated) email address on some provider.


7、运行
127.0.0.1:8000/login/google信息登录。

会调用相关程序的api。

# 调用哪个网站的就去哪个网站开发者平台注册
SOCIAL_AUTH_WEIBO_KEY = ''
SOCIAL_AUTH_WEIBO_SECRET = ''


SOCIAL_AUTH_LOGIN_REDIRECT_URL = 'index/'


指定id和key的使用。
还需要回调hansh函数，指定回调的url。

























