# Mailbox Analyzer

MailBox Analyzer is an application using [Watson Developer Cloud Java SDK](https://github.com/watson-developer-cloud/java-sdk) to demonstrate how to use the [Watson Developer Cloud services](https://www.ibm.com/watson/products-services/), a collection of REST APIs and SDKs that use cognitive computing to solve complex problems.

<br>

## Table of Contents

<!--
- [Overview of the application](#overview-of-the-application)
-->
- [Application Flow](#application-flow)
- [Prerequisite](#prerequisite)
  * [Install needed softwares](#install-needed-softwares)
  * [Check everything is installed properly](#check-everything-is-installed-properly)
  * [Check your IBM Cloud account](#check-your-ibm-cloud-account)
  * [Add some environment variables and aliases](#add-some-environment-variables-and-aliases)
- [Login to IBM Cloud](#login-to-ibm-cloud)
- [Setup environment with IBM Cloud Graphical User Interface](#setup-environment-with-ibm-cloud-graphical-user-interface)
- [Setup environment with command line](#setup-environment-with-command-line)
  * [Dump marketplace to get service name plan and description](#dump-marketplace-to-get-service-name-plan-and-description)
  * [Setup Tone Analyzer service](#setup-tone-analyzer-service)
    + [Get name and plan for Tone Analyzer service](#get-name-and-plan-for-tone-analyzer-service)
    + [Create Tone Analyzer service](#create-tone-analyzer-service)
    + [Create service key for Tone Analyzer service](#create-service-key-for-tone-analyzer-service)
  * [Setup Natural Language Understanding service](#setup-natural-language-understanding-service)
    + [Get name and plan for Natural Language Understanding service](#get-name-and-plan-for-natural-language-understanding-service)
    + [Create Natural Language Understanding service](#create-natural-language-understanding-service)
    + [Create service key for Natural Language Understanding service](#create-service-key-for-natural-language-understanding-service)
  * [Setup Discovery service](#setup-discovery-service)
    + [Get name and plan for Discovery service](#get-name-and-plan-for-discovery-service)
    + [Create Discovery service](#create-discovery-service)
    + [Create service key for Discovery service](#create-service-key-for-discovery-service)
  * [Create Discovery Collection](#create-discovery-collection)
      + [Store Discovery collection name in DSC_COLL_NAME environment variable](#store-discovery-collection-name-in-dsc_coll_name-environment-variable)
    + [Store Discovery collection language in DSC_COLL_LANG environment variable](#store-discovery-collection-language-in-dsc_coll_lang-environment-variable)
    + [Store Discovery version in DSC_VERSION environment variable](#store-discovery-version-in-dsc_version-environment-variable)
    + [Create collection coll0](#create-collection-coll0)
  * [Create Visual Recognition service](#create-visual-recognition-service)
    + [Get name and plan for Visual Recognition service](#get-name-and-plan-for-visual-recognition-service)
    + [Create Visual Recognition service](#create-visual-recognition-service)
    + [Create service key for Visual Recognition service](#create-service-key-for-visual-recognition-service)
  * [Check environment is setup correctly](#check-environment-is-setup-correctly)
- [Setup application](#setup-application)
  * [Get application code](#get-application-code)
  * [Prepare for application deployment](#prepare-for-application-deployment)
- [Deploy application](#deploy-application)
- [Run application](#run-application)
- [Send your own datas for analysis](#send-your-own-datas-for-analysis)
- [Clean your room](#clean-your-room)
- [About Watson Developer Cloud services being used in the application](#about-watson-developer-cloud-services-being-used-in-the-application)
- [About other Watson Developer Cloud services](#about-other-watson-developer-cloud-services)

<br>

<!--
### Overview of the application

A sample demo of the application with a mailbox analysis *may be* available [here](http://ma.bpshparis.eu-de.mybluemix.net).

<br>
-->

### Application Flow
![Flow](images/appFlow.jpg)

<br>

### Prerequisite

<br>

#### Install needed softwares

> :bulb: Ctrl + Click on links below to open them in new tab and keep the tutorial tab opened.

![](res/win.png)

* Download and install [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html)  
* Download and install [curl](https://curl.haxx.se/windows/)
* Download [jq](https://github.com/stedolan/jq/releases/download/jq-1.5/jq-win64.exe), rename it to **jq** and copy it in your %PATH%.

![](res/mac.png)

* Download and install [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html)  
* **curl** should already be installed. If not, get it from [here](https://curl.haxx.se/dlwiz/?type=bin&os=Mac+OS+X&flav=-&ver=-&cpu=i386)
* Download [jq](https://github.com/stedolan/jq/releases/download/jq-1.5/jq-osx-amd64), rename it to **jq** and copy it in your $PATH.

![](res/tux.png)

* Download and install [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html)  
* Get **curl** from your distribution repository or download and install it from [here](https://curl.haxx.se/dlwiz/?type=bin&os=Linux).
* Get **jq** from your distribution repository or download it from [here](https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64), rename it to **jq** and copy it in your $PATH.

<br>

#### Check everything is installed properly

![](res/win.png) ![](res/cmd.png) 

![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

Check ibmcloud command is available:

	ibmcloud -v

Check curl command is available:

	curl -V

Check jq command is available:

	jq

<br>

### Login to IBM Cloud

:bulb: To avoid being prompt when using ibmcloud command set the following config parameters

	ibmcloud config --check-version false
	ibmcloud config --usage-stats-collect false

Let's connect to :de:

![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

	iclde	
	
![](res/win.png) ![](res/cmd.png)

	%iclde%	

> :no_entry: If **login failed** because of logging in with a federated ID, then browse one of the following url:

> :bulb: Ctrl + Click on links below to open them in new tab and keep the tutorial tab opened.

 * https://login.ng.bluemix.net/UAALoginServerWAR/passcode
 * https://login.eu-gb.bluemix.net/UAALoginServerWAR/passcode
 * https://login.eu-de.bluemix.net/UAALoginServerWAR/passcode
 
> and get a one-time passcode.

> Then login with **--sso**,

![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

	iclsso
	
![](res/win.png) ![](res/cmd.png)

	%iclsso%	
	
> paste the one-time passcode when prompt

	One Time Code (Get one at https://login.eu-gb.bluemix.net/UAALoginServerWAR/passcode)>
	
> and hit enter.

> Then create an API key called apikey0 and save it in apikey0 file in current directory
	
	ibmcloud iam api-key-create apikey0 -d "apikey0" --file apikey0

> Now login with your API key stored in apikey0 file in current directory

	ibmcloud login target --apikey @apikey0
	
> and target :de: endpoint

![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

	ibmcloud target --cf-api ${DE_ENDPOINT} -o $ORG -s $SPACE
	
![](res/win.png) ![](res/cmd.png)	

	ibmcloud target --cf-api %DE_ENDPOINT% -o %ORG% -s %SPACE%

:thumbsup: Now you should be logged and ready to setup environment.

<br>

### Setup environment with IBM Cloud Graphical User Interface

Ctrl + Click on [IBM Cloud Catalog](https://console.bluemix.net/catalog/?category=ai)

To instanciate **Tone Analyzer** service click

![](guiScreenShots/ta0.jpg)

:zzz: Wait for followings panels to be available:

![](guiScreenShots/ta1.jpg)

![](guiScreenShots/ta2.jpg)

Then hit 

![](guiScreenShots/ta3.jpg)

:zzz: When you land on,

![](guiScreenShots/ta4.jpg)

:thumbsup: this mean that the **Tone Analyzer** service as been successfully instantiate.

To be ready to use  **Tone Analyzer** instance need a new credential to be created. So click on **Service credentials** available on top left under the menu:

![](guiScreenShots/ta5.jpg)

Then click

![](guiScreenShots/ta6.jpg)

Keep default setting

![](guiScreenShots/ta7.jpg)

and hit 

![](guiScreenShots/ta8.jpg)


To instanciate **Natural Language Understanding** service, go back to [IBM Cloud Catalog](https://console.bluemix.net/catalog/?category=ai) and click

![](guiScreenShots/nlu0.jpg)

:zzz: Wait for followings panels to be available:

![](guiScreenShots/nlu1.jpg)

![](guiScreenShots/nlu2.jpg)

Then hit 

![](guiScreenShots/nlu3.jpg)

:zzz: When you land on,

![](guiScreenShots/ta4.jpg)

:thumbsup: this mean that the **Natural Language Understanding** service as been successfully instantiate.

To instanciate **Visual Recognition** service, go back to [IBM Cloud Catalog](https://console.bluemix.net/catalog/?category=ai) and click

![](guiScreenShots/wvc0.jpg)

:zzz: Wait for followings panels to be available:

![](guiScreenShots/wvc1.jpg)

![](guiScreenShots/wvc2.jpg)

Then hit 

![](guiScreenShots/wvc3.jpg)

:zzz: When you land on,

![](guiScreenShots/wvc4.jpg)

:thumbsup: this mean that the **Visual Recognition** service as been successfully instantiate.



### Setup environment with command line

#### Dump marketplace to get service name, plan and description

:zzz: It may take a minute to display 

![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

	ibmcloud service offerings | tee marketplace

![](res/win.png) ![](res/cmd.png)	

	ibmcloud service offerings > marketplace

<br>

#### Setup Tone Analyzer service

![](res/ta50x.png) **Tone Analyzer** uses linguistic analysis to detect three types of tones from communications: emotion, social, and language.  This insight can then be used to drive high impact communications.

##### Get name and plan for Tone Analyzer service

<!--
	ibmcloud catalog search tone
	ibmcloud catalog service tone-analyzer
	ibmcloud resource service-instance-create ta tone-analyzer lite eu-de
	ibmcloud resource service-key-create taKey Manager --instance-name ta
	export TA_APIKEY=$(ibmcloud resource service-key taKey | awk '/^\s*apikey:/ {print $2}') && echo $TA_APIKEY
	export TA_URL=$(ibmcloud resource service-key taKey | awk '/^\s*url:/ {print $2}') && echo $TA_URL
	export TA_METHOD=/v3/tone?version=2017-09-21 && echo $TA_METHOD
	export TA_TEXT="On en a gros !" && echo $TA_TEXT
	jq -n --arg value "$TA_TEXT" '{"text": $value}' | tee ta.req.json | jq .
	curl -X POST -u 'apikey:'$TA_APIKEY -H 'Content-Type: application/json' -H 'Content-Language: fr' -H 'Accept-Language: fr' -d @ta0.req.json $TA_URL$TA_METHOD | tee ta.resp.json | jq .
-->

![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

	grep -i tone marketplace
	
![](res/win.png) ![](res/cmd.png)

	find /I "tone" marketplace

##### Create Tone Analyzer service
	ibmcloud service create tone_analyzer lite ta0

##### Create service key for Tone Analyzer service
	ibmcloud service key-create ta0 user0

<br>

#### Setup Natural Language Understanding

![](res/nlu50x.png) **Natural Language Understanding** analyze text to extract meta-data from content such as concepts, entities, emotion, relations, sentiment and more.

##### Get name and plan for Natural Language Understanding service

<!--
	ibmcloud catalog search understanding
	ibmcloud catalog service natural-language-understanding
	ibmcloud resource service-instance-create nlu natural-language-understanding free eu-de	
	ibmcloud resource service-key-create nluKey Manager --instance-name nlu
	export NLU_APIKEY=$(ibmcloud resource service-key nluKey | awk '/^\s*apikey:/ {print $2}') && echo $NLU_APIKEY
	export NLU_URL=$(ibmcloud resource service-key nluKey | awk '/^\s*url:/ {print $2}') && echo $NLU_URL
	export NLU_METHOD=/v1/analyze?version=2018-11-16 && echo $NLU_METHOD
	export NLU_FEATURES='{"sentiment": {}, "keywords": {}, "entities": {}}' && echo "$NLU_FEATURES" | jq .
	export NLU_TEXT="J'aimerai avoir des nouvelles de ma commande passée il y a déjà 15 jours et que je n'ai toujours pas reçu." && echo $NLU_TEXT
	jq -n --argjson features "$NLU_FEATURES" --arg text "$NLU_TEXT" '{"text": $text, "features": $features}' | tee nlu.req.json | jq .
	curl -X POST -u 'apikey:'$NLU_APIKEY -H 'Content-Type: application/json' -d @nlu.req.json $NLU_URL$NLU_METHOD | tee nlu.resp.json | jq .
-->


![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

	grep -i language marketplace

![](res/win.png) ![](res/cmd.png)

	find /I "language" marketplace

##### Create Natural Language Understanding service
	ibmcloud service create natural-language-understanding free nlu0

##### Create service key for Natural Language Understanding service
	ibmcloud service key-create nlu0 user0

<br>

#### Setup Discovery service

![](res/dsc50x.png) **Discovery** add a cognitive search and content analytics engine to applications.

##### Get name and plan for Discovery service

<!--
	ibmcloud catalog search discovery
	ibmcloud catalog service discovery
	ibmcloud resource service-instance-create dsc discovery lite eu-de	
	ibmcloud resource service-key-create dscKey Manager --instance-name dsc
	export DSC_APIKEY=$(ibmcloud resource service-key dscKey | awk '/^\s*apikey:/ {print $2}') && echo $DSC_APIKEY
	export DSC_URL=$(ibmcloud resource service-key dscKey | awk '/^\s*url:/ {print $2}') && echo $DSC_URL
	export DSC_VERSION=2019-01-01 && echo $DSC_VERSION
	export DSC_COLL_NAME=coll && echo $DSC_COLL_NAME
	export DSC_COLL_LANG=fr && echo $DSC_COLL_LANG
	export DSC_METHOD= && echo $DSC_METHOD
-->

![](res/mac.png) ![](res/tux.png) ![](res/term.png) 

	grep -i discovery marketplace

![](res/win.png) ![](res/cmd.png)

	find /I "discovery" marketplace

##### Create Discovery service

	ibmcloud service create discovery lite dsc0

##### Create service key for Discovery service

:warning: You may have to wait for service to display **create succeded** in **last operation** column before being able to create the key.

Check Discovery service have been created with 

	ibmcloud service list
	
When **last operation** column displays **create succeded** then create Discovery key 	

	ibmcloud service key-create dsc0 user0

#### Create Discovery Collection

##### Store Discovery Collection name in DSC_COLL_NAME environment variable

![](res/mac.png) ![](res/tux.png) ![](res/term.png)

	export DSC_COLL_NAME=coll0

![](res/win.png) ![](res/cmd.png)

	set "DSC_COLL_NAME=coll0"

##### Store Discovery Collection language in DSC_COLL_LANG environment variable

> Choose a language model among this list:

> * **en**
> * es
> * de
> * ar
> * **fr**
> * it
> * ja
> * ko
> * pt
> * nl

![](res/mac.png) ![](res/tux.png) ![](res/term.png)

	export DSC_COLL_LANG=en_us

![](res/win.png) ![](res/cmd.png)

	set "DSC_COLL_LANG=en_us"

##### Store Discovery Version in DSC_VERSION environment variable

![](res/mac.png) ![](res/tux.png) ![](res/term.png)

	export DSC_VERSION=2018-03-05

![](res/win.png) ![](res/cmd.png)

	set "DSC_VERSION=2018-03-05"
	
##### Create collection coll0	

:checkered_flag: Now, you should be ready to create the collection.

![](res/mac.png) ![](res/tux.png) ![](res/notepad.png)

Paste content below in a bat file e.g. run.sh
```
#!/bin/sh

export SVC_NAME=dsc0
export KEY_NAME=user0
export ENV_NAME=env0

echo DSC_COLL_LANG=$DSC_COLL_LANG
echo DSC_VERSION=$DSC_VERSION
echo DSC_COLL_NAME=$DSC_COLL_NAME

#Store Discovery url in URL environment variable
URL=$(ibmcloud service key-show $SVC_NAME $KEY_NAME | awk 'NR >= 4 {print}' | jq -r '.url') 
echo URL=$URL

#Store Discovery APIKEY in CRED environment variable
CRED=$(ibmcloud service key-show $SVC_NAME $KEY_NAME | awk 'NR >= 4 {print}' | jq -r '"apikey:" + .apikey')
echo CRED=$CRED

#Create env0 environment for Discovery service and store its id in ENVID
ENVID=$(curl  -X POST -u ${CRED} -H 'Content-Type: application/json' -d '{"name": "'$ENV_NAME'"}' ${URL}'/v1/environments?version='${DSC_VERSION} | jq -r '.environment_id')
echo ENVID=$ENVID

#Get configuration for Discovery service and store its id in CONFID
CONFID=$(curl -u ${CRED} ${URL}'/v1/environments/'${ENVID}'/configurations?version='${DSC_VERSION} | jq -r '.configurations[0].configuration_id')
echo CONFID=$CONFID

#Create collection for Discovery service and store its id in COLLID
COLLID=$(curl -X POST -H 'Content-Type: application/json' -u ${CRED} -d '{"name": "'$DSC_COLL_NAME'", "configuration_id":"'${CONFID}'" , "language": "'${DSC_COLL_LANG}'"}' ${URL}'/v1/environments/'${ENVID}'/collections?version='${DSC_VERSION} | jq -r '.collection_id')
echo COLLID=$COLLID
```

<!--
Get **environment_id** for Discovery service
	curl -u ${CRED} ${URL}'/v1/environments?version='${DSC_VERSION} | jq -r --arg ENV env0 '.environments[] | select(.name == $ENV) | .environment_id'
	curl -X POST -u ${CRED} -H 'Content-Type: application/json' -X DELETE ${URL}'/v1/environments/'${ENVID}'?version='${DSC_VERSION}
-->

<!--
Get **configuration_id** for Discovery service
	curl -u ${username}:${password} '${url}/v1/environments/${ENVID}/configurations?version=${DSC_VERSION}' | jq -r '.configurations[] | .configuration_id'
-->

![](res/win.png) ![](res/notepad.png)

Paste content below in a bat file e.g. run.bat

```
@echo off

setlocal ENABLEDELAYEDEXPANSION

set "SVC_NAME=dsc0"
set "KEY_NAME=user0"
set "ENV_NAME=env0"

@echo DSC_COLL_LANG=%DSC_COLL_LANG%
@echo DSC_VERSION=%DSC_VERSION%
@echo DSC_COLL_NAME=%DSC_COLL_NAME%

::Store credential in KEY environment variable
set "CMD=ibmcloud service key-show %SVC_NAME% %KEY_NAME%"
for /f "tokens=* skip=4" %%a in ('%CMD%') do (set LINE=%%a & set KEY=!KEY!!LINE!)

::Store Discovery url in URL environment variable
for /f "delims=" %%a in ('cmd /c "echo %KEY% | jq -r .url"') do set BASE_URL=%%a
@echo URL=%URL%

::Store Discovery APIKEY in CRED environment variable
for /f "delims=" %%a in ('cmd /c "echo %KEY% | jq -r .apikey"') do set APIKEY=%%a
set "CRED=apikey:%APIKEY%"
@echo %CRED%

::Create env0 environment for Discovery service and store its id in ENVID
set "URL=%BASE_URL%/v1/environments^?version^=%DSC_VERSION%"
set "PARMS={"name": "%ENV_NAME%"}"
echo %PARMS% > parms.json
set "CMD=curl  -X POST -u %CRED% -H "Content-Type: application/json" -d @parms.json %URL%"
for /f "tokens=*" %%a in ('cmd /c "%CMD%"') do (set LINE=%%a & set OUTPUT=!OUTPUT!!LINE!)
for /f "delims=" %%a in ('cmd /c "echo %OUTPUT% | jq -r .environment_id"') do set ENVID=%%a
@echo ENVID=%ENVID%

::Create configuration for Discovery service and store its id in CONFID
set "URL=%BASE_URL%/v1/environments/%ENVID%/configurations^?version^=%DSC_VERSION%"
set "CMD=curl -u %CRED% %URL%"
for /f "tokens=*" %%a in ('cmd /c "%CMD%"') do (set LINE=%%a & set OUTPUT=!OUTPUT!!LINE!)
for /f "delims=" %%a in ('cmd /c "echo %OUTPUT% | jq -r .configurations[0].configuration_id"') do set CONFID=%%a
@echo CONFID=%CONFID%

::Create collection for Discovery service and store its id in COLLID
set "PARMS={"name": "%DSC_COLL_NAME%", "configuration_id":"%CONFID%" , "language": "%DSC_COLL_LANG%"}"
echo %PARMS% > parms.json
set "URL=%BASE_URL%/v1/environments/%ENVID%/collections^?version^=%DSC_VERSION%"
set "CMD=curl -X POST -H "Content-Type: application/json" -u %CRED% -d @parms.json %URL%"
for /f "tokens=*" %%a in ('cmd /c "%CMD%"') do (set LINE=%%a & set OUTPUT=!OUTPUT!!LINE!)
for /f "delims=" %%a in ('cmd /c "echo %OUTPUT% | jq -r .collection_id"') do set COLLID=%%a
@echo COLLID=%COLLID%
```

and execute it to create Discovery collection

![](res/mac.png) ![](res/tux.png) ![](res/term.png)

	chmod +x run.sh && ./run.sh

![](res/win.png) ![](res/cmd.png)

	run.bat

> :bulb: You won't need neither environment_id nor configuration_id for further use but keep ENV_NAME and DSC_COLL_NAME in mind if you choose something else than **env0** and **coll0**.

<br>

#### Create Visual Recognition service

![](res/wvc50x.png) **Visual Recognition** find meaning in visual content! Analyze images for scenes, objects, faces, and other content. Choose a default model off the shelf, or create your own custom classifier. Develop smart applications that analyze the visual content of images or video frames to understand what is happening in a scene.

##### Get name and plan for Visual Recognition service

<!--
	ibmcloud catalog search vision
	ibmcloud catalog service watson-vision-combined
	ibmcloud resource service-instance-create wvc watson-vision-combined lite us-south	
	ibmcloud resource service-key-create wvcKey Manager --instance-name wvc
	export WVC_APIKEY=$(ibmcloud resource service-key wvcKey | awk '/^\s*apikey:/ {print $2}') && echo $WVC_APIKEY
	export WVC_URL=$(ibmcloud resource service-key wvcKey | awk '/^\s*url:/ {print $2}') && echo $WVC_URL
	export WVC_METHOD=/v3/classify?version=2018-03-19 && echo $WVC_METHOD
	export IMG=$(readlink -f image1.jpg) && echo $IMG
	curl -X POST -u 'apikey:'$WVC_APIKEY -H 'Accept-Language: fr' -F 'images_file=@'$IMG $WVC_URL$WVC_METHOD | tee wvc.resp.json | jq .
-->

![](res/mac.png) ![](res/tux.png) ![](res/term.png)

	grep -i visual marketplace
	
![](res/win.png) ![](res/cmd.png)

	find /I "visual" marketplace
	

##### Create Visual Recognition service

	ibmcloud resource service-instance-create wvc0 watson-vision-combined lite us-south	
	
	ibmcloud  resource service-alias-create wvc0 --instance-name wvc0

##### Create service key for Visual Recognition service

	ibmcloud service key-create wvc0 user0

<br>

#### Check environment is setup correctly

> :thumbsup: You are done with environment setup. Now at least four Watson services should be created (**ta0, nlu0, dsc0 and wvc0**) in your space.

>Check it with

	ibmcloud service list

<br>
	
### Setup application

#### Get application code

Download code

	curl -LO  https://github.com/bpshparis/ma/archive/master.zip

Unzip it

#### Prepare for application deployment

Change to code directory

	cd ma-master

> Now if you stand in the correct directory, you should be able to list directory such as **WebContent** and file such as **manifest.yml**.

>Before deploying the application you need to choose **3** things:

> :warning: **Don't use special characters. Use [a-z],[A-Z],[0-9] and [-] only.**
> * A **host** (must be unique in domain) for your application (e.g.: **mylastname-mycompagny**)
> * A **name** (must be unique in your space) for your application (e.g.: **myapp0**)
> * A **domain** (must be available in your space)  for your application (e.g.: **eu-de.mybluemix.net**)

:bulb: find domains available in your space with the following command

	ibmcloud app domains

![](res/notepad.png)

Edit the **manifest.yml** and update it accordingly by substituting **mylastname-mycompagny**, **myapp0** and **eu-de.mybluemix.net** if needed:
```
applications:
# WARNING: Only hyphen (e.g. -) are supported in hostname. Don't add any dot.
# host must be unique in domain
- host: mylastname-mycompagny
  disk: 256M
  #name must be unique in your space
  name: myapp0
  path: ./WebContent
  #domain must be available in your space
  domain: eu-de.mybluemix.net
  mem: 256M
  instances: 1
  services:
  - ta0
  - nlu0
  - dsc0
  - wvc0
```

<br>

### Deploy application

> :warning: For deployment to work you need to push your code from the same directory as **manifest.yml**.

:checkered_flag: Now you are ready to deploy the application :

	ibmcloud app push

Once staging has completed you should be able to run the application *on your own IBM Cloud environment*.

```
...
0 of 1 instances running, 1 starting
1 of 1 instances running

App started


OK

App app0 was started using this command `.liberty/initial_startup.rb`

Showing health and status for app app0 in org teatcher0@bpshparis.com / space dev as teatcher0@bpshparis.com...
OK

requested state: started
instances: 1/1
usage: 1G x 1 instances
urls: ma-bpshparis.eu-de.mybluemix.net
last uploaded: Wed Oct 3 23:05:17 UTC 2018
stack: cflinuxfs2
buildpack: Liberty for Java(TM) (WAR, liberty-18.0.0_3, buildpack-v3.25-20180918-1034, ibmjdk-1.8.0_20180830, env)

     state     since                    cpu      memory        disk           details
#0   running   2018-10-03 11:07:38 PM   112.4%   96.6M of 1G   223.5M of 1G
```

<br>

### Run application

Display your application state :

	ibmcloud app list
	
Copy urls columns content. It should be something like **mylastname-mycompagny.eu-de.mybluemix.net**.

Paste it in a new tab of your web browser and check application is running

Click on ![](res/envelope.png) to upload sample attached documents in Discovery Collection and get sample mails.

Once mails are displayed, click ![](res/cogwheels.png) to send sample mails for analysis.

When Watson returned, **4 new tabs** (one per service) should appear and are ready to browse. 

![](res/watsontabs.png)

<br>

### Send your own datas for analysis

![](res/notepad.png)

Edit a json file of this form :

```
[
  {
    "subject": "paste some text between double quotation marks or set to null",
    "content": "paste some text between double quotation marks or set to null",
    "attached": "paste a doc|docx|pdf file name between double quotation marks or set to null",
    "picture": "paste a picture file name between double quotation marks or set to null",
    "face": "paste a picture file name between double quotation marks or set to null",
    "tip": "paste a picture file name between double quotation marks or set to null"
  }
]
```

An example for 2 mails with documents and pictures attached :

```
[
  {
      "subject": "At UEFA, Mounting Concern About A.C. Milan’s Murky Finances",
      "content": null,
      "attached": "3.pdf",
      "picture": "pic3.jpg",
      "face": null,
      "tip": null
  },
  {
      "subject": null,
      "content": "At a flea market six years ago, a North Carolina lawyer named Frank Abrams unknowingly bought...",
      "attached": "4.doc",
      "picture": null,
      "face": "face4.jpg",
      "tip": "tip4.jpg"
  }
]
```

Save this file as **mails.json** 

:bulb: Test it with jq

	jq . mails.json

The command should display pretty json without error.

Now **zip mails.json with all files set in attached, picture, face and tip fields from mails.json**.

:bulb: your archive should be this form

```
Archive:  mails0.zip
    testing: 3.doc                    OK
    testing: 3.pdf                    OK
    testing: 4.doc                    OK
    testing: face4.jpg                OK
    testing: mails.json               OK
    testing: pic3.jpg                 OK
    testing: tip4.jpg                 OK
No errors detected in compressed data of mails0.zip.
```
Now go back to your application and click ![](res/compressed.png) to upload your datas.

Once your datas have been upload, click on ![](res/envelope.png) to upload your attached documents in Discovery Collection and get your mails.

Once your mails are displayed, click ![](res/cogwheels.png) to send your mails for analysis.

<br>

### Clean your room

![](res/mac.png) ![](res/tux.png) ![](res/term.png)

	export APP_NAME=app0 && for svc in ta0 nlu0 dsc0 wvc0; do ibmcloud service unbind ${APP_NAME} $svc; ibmcloud service key-delete -f $svc user0; ibmcloud service delete -f $svc; done && ic app delete ${APP_NAME} -f

![](res/win.png) ![](res/web.png)

Browse your [IBM Cloud dashboard](https://console.bluemix.net/dashboard/apps)

Open each services **More Actions** popup menu and choose **Delete Service**

![](res/delsvc.png)

Do the same for application. Open application **More Actions** popup menu and choose **Delete App**

![](res/delapp.png)

<br>

### About Watson Developer Cloud services being used in the application

![](res/ta50x.png) **Tone Analyzer** uses linguistic analysis to detect three types of tones from communications: emotion, social, and language.  This insight can then be used to drive high impact communications.

[Documentation](https://console.bluemix.net/docs/services/tone-analyzer/getting-started.html) 
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/tone-analyzer-dashboard.html) 
[Github](https://github.com/watson-developer-cloud)

![](res/nlu50x.png) **Natural Language Understanding** analyze text to extract meta-data from content such as concepts, entities, emotion, relations, sentiment and more.

[Documentation](https://console.bluemix.net/docs/services/natural-language-understanding/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/natural-language-understanding-dashboard.html)
[Github](https://github.com/watson-developer-cloud)

![](res/dsc50x.png) **Discovery** add a cognitive search and content analytics engine to applications.

[Documentation](https://console.bluemix.net/docs/services/discovery/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/discovery-dashboard.html)
[Github](https://github.com/watson-developer-cloud)
[Tool](https://watson-discovery.bluemix.net)

![](res/wvc50x.png) **Visual Recognition** find meaning in visual content! Analyze images for scenes, objects, faces, and other content. Choose a default model off the shelf, or create your own custom classifier. Develop smart applications that analyze the visual content of images or video frames to understand what is happening in a scene.

[Documentation](https://console.bluemix.net/docs/services/visual-recognition/getting-started.html)
[Dashboard](https://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/dashboard/en/visual-recognition-dashboard.html)
[Github](https://github.com/watson-developer-cloud)
[Tool](https://watson-visual-recognition.ng.bluemix.net/)

<br>

### About other Watson Developer Cloud services

![](res/s2t50x.png) **Speech to Text** Low-latency, streaming transcription.

[Documentation](https://console.bluemix.net/docs/services/speech-to-text/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/speech-to-text-dashboard.html)
[Github](https://github.com/watson-developer-cloud)

![](res/t2s50x.png) **Text to Speech** Synthesizes natural-sounding speech from text.

[Documentation](https://console.bluemix.net/docs/services/text-to-speech/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/text-to-speech-dashboard.html)
[Github](https://github.com/watson-developer-cloud)

![](res/lt50x.png) **Language Translator** Translate text from one language to another for specific domains.

[Documentation](https://console.bluemix.net/docs/services/language-translator/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/language-translator-dashboard.html)
[Github](https://github.com/watson-developer-cloud)

![](res/pi50x.png) **Personality Insights** The Watson Personality Insights derives insights from transactional and social media data to identify psychological traits

[Documentation](https://console.bluemix.net/docs/services/personality-insights/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/personality-insights-dashboard.html)
[Github](https://github.com/watson-developer-cloud)

![](res/cvt50x.png) **Conversation** Add a natural language interface to your application to automate interactions with your end users. Common applications include virtual agents and chat bots that can integrate and communicate on any channel or device. 

[Documentation](https://console.bluemix.net/docs/services/conversation/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/conversation-dashboard.html)
[Github](https://github.com/watson-developer-cloud)
[Tool](https://watson-conversation.ng.bluemix.net)

![](res/nlc50x.png) **Natural Language Classifier** performs natural language classification on question texts. A user would be able to train their data and the predict the appropriate class for a input question.

[Documentation](https://console.bluemix.net/docs/services/natural-language-classifier/getting-started.html)
[Dashboard](https://www.ibm.com/watson/developercloud/dashboard/en/natural-language-classifier-dashboard.html)
[Github](https://github.com/watson-developer-cloud)
[Tool](https://natural-language-classifier-toolkit.eu-gb.bluemix.net)

### Annexes

#### Run application elsewhere from IBM Cloud

##### Using Resource Group (Manual-generated service credentials)

```
#!/bin/sh

output=resources.json

echo '{}' | tee $output

services=$(ibmcloud service list | awk 'NR>6 {print "{\""$2"\":[{\"credentials\":null,\"name\":\""$1"\"}]}"}')

count=$(ibmcloud resource service-instances | awk -F'   ' 'NR>3 {count++} END {print count}') && echo $count " service-instances found."

instances=$(ibmcloud resource service-instances | awk -F'   ' 'NR>3 {print $1 ";;"}')

for i in $(seq 1 $count)
	do
		instance=$(echo $instances | awk -F ';;' '{print $'$i'  }');
		# service=$(echo $service | tr -d '[:space:]');
		instance=$(echo $instance | sed -e 's/^[[:space:]]*//');
		echo "Getting setting for service-instance "$instance;
		obj=$(ibmcloud resource service-instance "$instance" | awk -F ':' '/^ID:/ {print $6 ":" $7 ":" $9}');
		# echo $obj;

		service=$(echo $obj | cut -d':' -f1);
		region=$(echo $obj | cut -d':' -f2);
		id=$(echo $obj | cut -d':' -f3);

		region=$(ibmcloud resource service-instance "$instance" | awk -F ':' '/^ID:/ {print $7}');
		jq --argjson svc "{\"$id\":{\"credentials\":null,\"service\":\"$service\",\"region\":\"$region\",\"instance\":\"$instance\"}}" '. += $svc' $output | sponge $output;


	done

count=$(ibmcloud resource service-keys | awk -F'   ' 'NR>3 {count++} END {print count}') && echo $count " service-keys found."
keys=$(ibmcloud resource service-keys | awk -F'   ' 'NR>3 {print $1 ";;"}')

for i in $(seq 1 $count)
	do
		keyName=$(echo $keys | awk -F ';;' '{print $'$i'  }');
		# service=$(echo $service | tr -d '[:space:]');
		keyName=$(echo $keyName | sed -e 's/^[[:space:]]*//');
		echo "Getting setting for service-key "$keyName;
		obj=$(ibmcloud resource service-key "$keyName" | awk -F ':' '/^ID:/ {print $9 ":" $11}');
		instanceId=$(echo $obj | cut -d':' -f1);
		keyId=$(echo $obj | cut -d':' -f2);
		apikey=$(ibmcloud resource service-key "$keyName" | awk -F ':' '/^\s*apikey:/ {print $2}');
		apikey=$(echo $apikey | tr -d '[:space:]');
		url=$(ibmcloud resource service-key "$keyName" | awk '/^\s*url:/ {print $2}');
		role=$(ibmcloud resource service-key "$keyName" | awk -F ':' '/^\s*iam_role_crn:/ {print $11}');
		role=$(echo $role | tr -d '[:space:]');

		cred='{"id": "'$keyId'", "name": "'$keyName'", "apikey": "'$apikey'", "url": "'$url'", "role": "'$role'"}';

		jq --argjson cred "$cred" 'if (.["'$instanceId'"]) then .["'$instanceId'"].credentials[.["'$instanceId'"].credentials| length] |= . + $cred else . end' $output | sponge $output;

	done

jq . $output

echo ""
echo "!!!! Resources available in " $(readlink -f $output) " !!!!"

# Sample usage:
# jq -r '.[] | select(.instance=="Visual Recognition-cv" and .credentials[1].role=="Writer") | .credentials[1].apikey + ":" + .credentials[1].role' $output


exit 0;
``` 

##### Using Resource Group (Auto-generated service credentials)

```
#!/bin/bash

input=credentials
output=resourcesAG.json

echo '{}' | tee $output

services=$(ibmcloud service list | awk 'NR>6 {print "{\""$2"\":[{\"credentials\":null,\"name\":\""$1"\"}]}"}')

count=$(ibmcloud resource service-instances | awk -F'   ' 'NR>3 {count++} END {print count}') && echo $count " service-instances found."

instances=$(ibmcloud resource service-instances | awk -F'   ' 'NR>3 {print $1 ";;"}')

for i in $(seq 1 $count)
	do
		instance=$(echo $instances | awk -F ';;' '{print $'$i'  }');
		# service=$(echo $service | tr -d '[:space:]');
		instance=$(echo $instance | sed -e 's/^[[:space:]]*//');
		echo "Getting setting for service-instance "$instance;
		obj=$(ibmcloud resource service-instance "$instance" | awk -F ':' '/^ID:/ {print $6 ":" $7 ":" $9}');
		# echo $obj;

		service=$(echo $obj | cut -d':' -f1);
		region=$(echo $obj | cut -d':' -f2);
		id=$(echo $obj | cut -d':' -f3);

		region=$(ibmcloud resource service-instance "$instance" | awk -F ':' '/^ID:/ {print $7}');
		jq --argjson svc "{\"$id\":{\"credentials\":null,\"service\":\"$service\",\"region\":\"$region\",\"instance\":\"$instance\"}}" '. += $svc' $output | sponge $output;


	done

ibmcloud resource service-key "Auto-generated service credentials" > ./input;

instanceIds=();
keyIds=();
keyNames=();
apikeys=();
urls=();
roles=();

while read LINE
  do
    id=$(echo $LINE | awk -F ':' '/^ID:/ {print $9 ":" $11}');
    instanceId=$(echo $id | cut -d':' -f1);
    if [ ! -z "$instanceId" ]; then
      instanceIds+=($instanceId);
    fi

    keyId=$(echo $id | cut -d':' -f2);
    if [ ! -z "$keyId" ]; then
      keyIds+=($keyId);
    fi

    keyName=$(echo $LINE | awk -F ':' '/^Name:/ {print $2}');
    keyName=$(echo $keyName | sed -e 's/^[[:space:]]*//');
    if [ ! -z "$keyName" ]; then
      keyNames+=("$keyName")
    fi

    apikey=$(echo $LINE | awk -F ':' '/^\s*apikey:/ {print $2}');
		apikey=$(echo $apikey | tr -d '[:space:]');
    if [ ! -z "$apikey" ]; then
      apikeys+=($apikey)
    fi

    url=$(echo $LINE | awk '/^\s*url:/ {print $2}');
    if [ ! -z "$url" ]; then
      urls+=($url)
    fi

    role=$(echo $LINE | awk -F ':' '/^\s*iam_role_crn:/ {print $11}');
    role=$(echo $role | tr -d '[:space:]');
    if [ ! -z "$role" ]; then
      roles+=($role)
    fi

  done < ./input

rm -f ./input;

echo "instanceIds="${instanceIds[@]};
echo "keyNames="${keyNames[@]};
echo "keyIds="${keyIds[@]};
echo "apikeys="${apikeys[@]};
echo "urls="${urls[@]};
echo "roles="${roles[@]};

count=${#apikeys[@]};
echo $count "service-keys found";

for i in $(seq 0 $(($count -1)))
  do
    echo "Getting setting for service-key "${keyNames[$i]};
    cred='{"id": "'${keyIds[$i]}'", "name": "'${keyNames[$i]}'", "apikey": "'${apikeys[$i]}'", "url": "'${urls[$i]}'", "role": "'${roles[$i]}'"}';
    echo $cred;
    jq --argjson cred "$cred" 'if (.["'${instanceIds[$i]}'"]) then .["'${instanceIds[$i]}'"].credentials[.["'${instanceIds[$i]}'"].credentials| length] |= . + $cred else . end' $output | sponge $output;
  done

jq . $output

echo ""
echo "!!!! Resources available in " $(readlink -f $output) " !!!!"

# Sample usage:
# jq -r '.[] | select(.instance=="Visual Recognition-cv" and .credentials[1].role=="Writer") | .credentials[1].apikey + ":" + .credentials[1].role' $output


exit 0;
```

##### Using Cloud Foundry

```
#!/bin/sh

output=vcap.json

echo '{}' | tee $output

services=$(ibmcloud service list | awk 'NR>6 {print "{\""$2"\":[{\"credentials\":null,\"name\":\""$1"\"}]}"}')

for service in $(echo $services)
	do 
		jq --argjson value $service '. += $value' $output | sponge $output; 
	done

for svc in $(ibmcloud service list | awk 'NR>6 {print $1 ":" $2}')
	do
		echo $svc;
		label=$(echo $svc | cut -d':' -f2);
		name=$(echo $svc | cut -d':' -f1);
		echo $label;
		echo $name;
		
		key=$(ibmcloud service key-show $name user0 | awk 'NR>4');
		
		echo $key
		
		jq \
		--arg name $name \
		--arg label $label \
		--argjson clef "$key" \
		'if (.["'$label'"][].name==$name) then .["'$label'"][].credentials = $clef else . end' $output | sponge $output;
	done
	
jq . $output
	
exit 0;
```
		
	
	