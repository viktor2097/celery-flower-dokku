# Celery flower monitoring on Dokku

Simple app to monitor to celery task running on Dokku.

## Instructions:

Lets start by setting up an app to host your flower page

Create an app
`dokku apps:create myapp-flower`

Set environment variables
(It uses REDIS_URL as a broker by default, if you use any other broker, just change the Procfile)
If you already have Redis setup, you can link it to this app to get the REDIS_URL environment variable

`dokku redis:link myapp-redis myapp-flower`

`dokku config:set myapp-flower PORT=5000 FLOWER_BASIC_AUTH=USERNAME:PASSWORD`

Set up any custom domains, if i own myapp.com i want my app accessible at flower.myapp.com
`dokku domains:add myapp-flower flower.myapp.com`

Clone the repo
`git clone https://github.com/viktor2097/celery-flower-dokku.git`

Add the remote to your dokku host
`git remote add dokku dokku@myhost.com:myapp-flower`

Push and you're done
`git push dokku master`

If you use letsencrypt, make sure to `dokku letsencrypt myapp-flower`