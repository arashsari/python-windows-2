How did you configure the site to be ready for Azure?
1.	Configure Visual Studio with web.config 
a.	 
2.	Configure Visual Studio with publishing profile.
a.	 
3.	Add requirement.txt in order to install Django and whitenose. App is failed to run as requirement.txt was missing. According to Deploy from local Git repo - Azure App Service | Microsoft Learn. Python project should have at least one of “*.py, requirements.txt, or runtime.txt” in repo. 
a.	Adding below dependency ( library/frameworks)
-	Django==4.0.1
-	whitenoise==6.0.0
4.	Configure whitenose to service static files in settings.py
a.	  
5.	Adding address to static files
a.	STATIC_URL = os.environ.get("DJANGO_STATIC_URL", "/static/")
b.	STATIC_ROOT = os.environ.get("DJANGO_STATIC_ROOT", "./static/")
6.	Adding website url into allow list in Django setting file. It is passed as environment variable rather than been hardcoded. Value is set in Application setting in Configuration section. 
a.	 
b.	 

Did you install or configure something in Azure Portal?
-	Add Python 3.6.4 extension
o	 
-	Set environment variable for Allow Host and Set Static Url for Django
-	 
What is the best recommendation for deploying Python Applications on Azure App Service Windows?
-	Set Allow Host as an environment variable
-	Set Security Code as an environment variable. Move Security key (in line 23) into Application Setting use it here as Environment variable
o	SECRET_KEY = '=kpli-kjn@mk+-^ng+d%-frxc@c-_qr^i_6(+)m+ytm!11ue6@'
-	Set Debug to False for security purposed (CSRF). Change the value of DEBUG variable in line 26 to False. The DEBUG = True is not recommended for Production. It Is not setting CSRF_Token (Cross Site Request Forgeries) which causes security vulnerability.references: Cross Site Request Forgery protection | Django documentation | Django (djangoproject.com)
-	 
-	For troubleshooting I used Kudo, Log Stream. Download Diagnostic dump from kudo site 
Other recommendations:
-	Python App Service runtime is not supported for Windows anymore. Either use Linux or Containerise the APP. I changed App Service Plan and App Service to be on Linux and latest supported version of Python. 
o	Python App Service runtime is not supported for Windows anymore
o	Python 3.4 is end of support
-	The upgrade has a benefit of using DevOps and github Action for CICD. Github action is not supporting python 3.6.4 anymore. 
o	Step 2- Build is failed with below error .  Runtime stack is set for Python 3.4 which is not available anymore. 
o	build-and-deploy: Version 3.4.0 with arch x64 not found Available versions: 3.10.9 (x86) 3.11.1 (x86) 3.7.9 (x86) 3.8.10 (x86) 3.9.13 (x86) 3.10.9 (x64) 3.11.1 (x64) 3.7.9 (x64) 3.8.10 (x64) 3.9.13 (x64)
 
Website is up and running  The Admin Page is also tested with Provided user/Pass 
