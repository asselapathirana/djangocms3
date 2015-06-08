# djangocms3

## Installing django-cms
- There are common problems with Pillow with jpeg support. 
 
 sudo apt-get install libjpeg libjpeg-dev libfreetype6 libfreetype6-dev zlib1g-dev
 mkvirtualenv myven
 
 cp postactivate $VIRUAL_ENV/bin/postactivate
 
 cp predeactivate $VIRUAL_ENV/bin/predeactivate

 \# then edit the desination files to provide suitable values for the variables. (notice the datbase url and provide values to match that in the DATABASE related entries!
 
 \# reload the virutal environment
 
 workon virtual_env_name
 
 \# then within the virtual enviroment
 easy_install Pillow
 
 \# note down the version say x.y.z. Also make sure that the jpeg support is compiled
 
 \#--- JPEG support available message should appear at the end of building. 
 
 \# now dump thre requirements of djangocms as so:
 djangocms -p . mysite -R 
 
 \# past requirements to ../rquirements.txt
 
 \#now edit the requirements.txt and make sure that
 
 Pillow==x.y.z
 
 \# now create the local postgres database to match 
 
 sudo su postgres
 
 ...
 
 \# then run after noting the correct database url postgres://..
 
 djangocms -p . mysite -r ../requirements.txt 

 \# copy requirements.txt to the project directory
 
 cp ../requirements.txt . 
 
 \# edit requirements and add the following additional requirements (needed for deployment).  NOTE: All these might not be needed 
 \# now clone the distribution directory 

  gunicorn==19.3.0
  dj-static==0.0.6
  django-sslify==0.2.7
  gunicorn==19.3.0
  requests==2.7.0
  static3==0.6.0
  whitenoise==1.0.6
 
  git clone  git@github.com:asselapathirana/django_deploy_with_ansible.git deploy
 
 \# now edit mysite/settings.py and append ./deploy/_settings.py to it
 
 \# now test the local server. 
 ./manage.py runserver
 
 \# add a dummy file to the <appname>/static directory so that the directory will be recorded in git. 
 
 \# Create a github repo  <myrepo> 
 
 git clone <repo's ssh url>
 
 \# edit .gitignore and add a line
 
 deploy/
 
 \# then
 
 git status
 git add . 
 git commit -am "message"
 git push origin master
 

## Deploying remotely 
 - Goto deploy directory and run
 ./ed ../pass.yml 

 ./setkye

 ./setup

## Copy local (development) database to remote 

-  This will REPLACE the remote database
 
 \# activate the lcoal virtualenv and make sure the postactivate script is sourced. 
 
 ./manage.py dumpdata > /tmp/out.json
 
 \# copy /tmp/out.json to the remote server. Then on the remote

 \# sudo to the user (owner) of the app. 
 \# make sure virtualenv is loaded and postactivate scrip is sourced. 
 
 ./manage.py loaddata /tmp/out.json

 \# reload the page on the browser. 

## Create a superuser
 
 \# if you have not copied the database content from development to remote server, the remote will not have a superuser account. then create one

 ./manage.py createsuperuser

## Video playing issues. 

 \# try replacing player.swf with new version (http://github.com/FlashJunior/OSFlashVideoPlayer/raw/master/player.swf)  at <app>/static/cms/swf/player.swf 

This need to be automated in deploy. 


