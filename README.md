

<div style="background-color:black;color:white; vertical-align: middle; text-align:center;font-size:250%; padding:10px; margin-top:100px"><b>
 Using IBM API Connect
 </b></a></div>

---
# Managing your APIs with IBM API Connect
---

![API Connect Logo](./images/i000.png)

+++



# Table of Content


Managing your APIs with IBM API Connect
Table of Content
1. API Connect Overview
- Components in API Connect
- Terminology
- Architecture
- Concept Map
- Plans & Products
- Product LifeCycle
2. Objectives
3. Prerequisites
- Task 1 : Sign in to IBM Cloud
- Task 2 : Fill in the form
- Task 3 : Confirm your registration to IBM Cloud from you email application
4. Setup API Connect in IBM Cloud
- Task 4 : Login to IBM Cloud
- Task 5 : Access the Catalog
- Task 6 : Find API Connect
- Task 7 : Review the service instance
- Task 8 : Create the API Connect instance
- Task 9 : Learn the different parts of the screen
- Task 10 : Get access to the Sandbox catalog
- Task 11 : Instanciate the Developer Portal
5 - Expose an existing REST API
- Task 12 : Download the API swagger source to your laptop
- Task 13 : Create a Product
- Task 14 : Create (import) the API
- Task 15 : Modify the definitions of the API
- Task 16 : Testing the new created API
- Task 17 : Exploring the API
6. Publish your API to the Sandbox catalog
- Task 18 : Stage the API in the Sandbox Catalog
- Task 19 : Publish your API
7. Consumer Experience
- Task 20 : Accessing the Developer Portal
- Task 21 : Sign in as a Developer Portal
- Task 22 : Defining a Mobile Applocation
- Task 23 : Subscribe to a Plan for our Product
- Task 24 : Test QuoteMgmt APIs from the Developer Portal
- Task 25 : Test QuoteMgmt APIs from the Command Line
8. APIs Analytics
- Task 26 : Accessing the Analytics Dashboard
- Task 27 : Customizing the Dashboard
9. Conclusion
Results
End of Lab

+++

# 1. API Connect Overview

**IBM API Connect** is a comprehensive end-to-end API lifecycle solution that enables the automated creation of APIs, simple discovery of systems of records, self-service access for internal and third party developers and built-in security and governance. Using automated, model-driven tools, create new APIs and microservices based on Node.js and Java runtimes—all managed from a single unified console. Ensure secure & controlled access to the APIs using a rich set of enforced policies. Drive innovation and engage with the developer community through the self-service developer portal. IBM API Connect provides streamlined control across the API lifecycle and also enables businesses to gain deep insights around API consumption from its built-in analytics.

### Components in API Connect

Find below a list of the main components in API Connect :

- **Gateway** (either DataPower, either a NodeJS implementation called micro gateway in this case). The requests from apps are going through the gateway, policies are enforced and analytic are gathered.
- **Manager** where the APIs are defined and governed. It also collects the analytics from the gateway. The manager can be used directly or more likely using the toolkit.
- **Portal**, an open source Drupal CMS - Content Management System. For the API consumers (Apps developpers), they create Apps and subscribe to API within the portal. Based on Drupal, it is highly customizable.
- **Loopback runtime** or micro services runtime. This is where the loopback applications are running. This component is originally coming from StrongLoop acquisition. Loopback applications can be created in minutes to expose data from SQL or NoSQL database and also a good place to perform composition of APIs.
- Associated to the Loopback runtime is the **Kubernetes** that monitors the Loopback runtime and can provide advanced feature such as auto-scaling.
- **Developer Toolkit**, running on the API developer, it offers the same web experience as the manager to manage APIs. But this is also the only place where you can define Loopback applications. It also contains CLI to operate directly on the manager whether it is an onPremise version or Bluemix version of API Connect.

### Terminology

- **API** : Can be SOAP or Representational State Transfer - REST API defined with an Open API definition (Swagger) as a YAML file. One API = one yaml file though WSDLs and Schema are separated in a zip file for a SOAP API.
- **Plan** : this is where we specify the quotas and if an approval is needed to subscribe to a Product/API.
- **Product** : this is an aggregation of APIs, and one or many plans associated to those APIs. This is what is published to a catalog. One Product = one yaml file.
- **Catalog** : it's relates to a cluster of gateways and a portal. It sounds like an environment but it also contains a business dimension. For example, good names for a catalog are Sandbox, Dev, Production, CRM (for my CRM APIs exposed to a specific population), etc ...
- **API Connect Cloud** : not to be confused with a cloud infrastructure/platform, it is a combination of gateways clusters, managers cluster, portal clusters and loopback applications runtimes. Usually a customer will have one, two, sometime three or more API Connect clouds, based on its organization and needs to separate the infrastructures.
- **Assembly** panel : this is where we specify the policies to be executed in the gateway for each transactions.

### Architecture 

IBM API Connect can work on Premises or in a Cloud. 
Find below the architecture details of the solution in the IBM Cloud that we are going to use during this labs :

![API Connect Architecture in the Cloud](./images/i091.png)

### Concept Map

We often speak about an API Connect **Cloud** which represents an instantiation of all the components of API Connect. The following diagram describes all the relationships between all the components. 
![API Connect Components](./images/i092.png)

### Plans & Products

To make an API available to a customer, it must be included in a **Plan**. Plans are used to differentiate between different offerings. Plans can share APIs, but whether subscription approval is required depends upon the Plan itself. Additionally, you can enforce rate limits through Plans or through operations within a Plan's APIs that override the Plan's rate limit.

**Products**

Plans and APIs are grouped in Products. Through Products, you can manage the availability and visibility of APIs and Plans. Use the API Designer to create, edit, and stage your Product. Use the API Manager to manage the lifecycle of your Product.

The following diagram demonstrates how Products, Plans, and APIs relate to one another. Note how Plans belong to only one Product, can possess different APIs to other Plans within the same Product, and can share APIs with Plans from any Product. Figure to show the hierarchy of Products, Plans, and APIs. 

![Products-Plans-APIs](./images/i094.png)

### Product LifeCycle

When you manage your Product versions, you move them through a series of lifecycle states, from initially staging a draft Product version to an environment, through to publishing to make the Product version available to your application developers, and to eventual retiring and archiving. The following table and diagram describe the various Product lifecycle states for a Product version.

![Products LifeCycle](./images/i093.png)


# 2. Objectives


In this workshop, you will use **API Connect** to define a simple REST API and an API Product in your private instance of API Connect in the **IBM Cloud**. This API is providing a **quote for a loan request**. The back-end application has already been implemented somewhere in the IBM Cloud thru Java code. 

![Quote API](./images/i001a.png)


You will learn:

- Goals of API Connect (Presentation)
- Basics on the architecture of the API Connect and terminology useful with API Connect (Presentation)
- How to create and test a REST API definition (Lab)
- How to publish an API to the IBM Cloud (Lab)
- How to subscribe to an API previously published and test in the Developer Portal (Lab)
- How to manage security and analytics about APIs (Lab)

 
# 3. Prerequisites

This lab is running on the **IBM Cloud** (ex Bluemix).

So before you start this lab, you should have satisfied the following prerequisites :
- [ ] You should have **2 valid emails** (one will be used to connect to IBM Cloud and the other one will be used to connect to the Developer Portal)
- [ ] Sign up to the **IBM Cloud** (ex Bluemix)

Here are some helpful steps :

### Task 1 : Sign in to IBM Cloud
If you don't have already registered to **IBM Cloud**,  
Open this link  [IBM Cloud](http://bluemix.net)


![Create your Lite Account](./images/a001.png)

### Task 2 : Fill in the form
Specify last name, first name, corp, country, phone number and password.
> By **default**, all new people that register to IBM Cloud will have an **Lite Account** with **no time restriction**. This is not a 30 day trial account. 

Click on **Create Account** button. 
![Register to IBM Cloud](./images/a002.png)

![Thanks](./images/a003.png)

### Task 3 : Confirm your registration to IBM Cloud from you email application
From your email application, confirm the account creation.

![Confirm Account](./images/a004.png)

Log in to IBM Cloud with your credentials :

![Success Sign up](./images/a005.png)

> Once connected to IBM Cloud, you will notice that you are directed automatically to the closest region (UK for our case). IBM Cloud also create an org (your email) and a space (dev) by default. 


![Bluemix Dashboard](./images/a006.png)


# 4. Setup API Connect in IBM Cloud

This exercise will show you how to create and setup an API Connect instance in IBM Cloud.


### Task 4 : Login to IBM Cloud
Open this link  [IBM Cloud](http://bluemix.net) and log in to IBM Cloud.

### Task 5 : Access the Catalog
Click on Catalog on the top left bar.

![Catalog button](./images/i003.png)


### Task 6 : Find API Connect
On the left navigation bar find APIs and click on API Connect.
![API Connect Service](./images/i004.png)

### Task 7 : Review the service instance
> For this lab, you'll need the Lite plan (Free Plan).

![APIC instance-1](./images/i005.png)

### Task 8 : Create the API Connect instance
Don't change anything. Click on the Create button.

![APIC instance-2](./images/i006.png)


### Task 9 : Learn the different parts of the screen

When looking at the screen, there are 2 areas :
- The bold blue box belongs to **IBM Cloud**, the Hamburger (small blue box) give menus specific to IBM Cloud.
- The bold red box belongs to **API Connect**, the chevrons (small red box) gives menus specific to API connect.

![Screen Layout](./images/i007a.png)

### Task 10 : Get access to the Sandbox catalog
API Connect is using a concept of "Catalog of products" to group a set of products and APIs all together. By default, at creation time, we only have one catalog called "Sandbox" that we are using for this lab.

> You can create any number of catalogs depending on your organization.

![Sandbox Catalog](./images/i007.png)

### Task 11 : Instanciate the Developer Portal
Each catalog has its own components and propose a developer portal.
Click on **Settings**, then on **Portal** and finally choose **Developer Portal**.  Follow the 3 steps (1,2 and 3 in red).
> Note that a yellow message will appear to indicate that your request is in process. You will normally receive a message later on your email indicating that the Developer Portal is ready to use. We will customize a standard access to the portal later in this lab.

![Portal Configuration](./images/i010.png)

We are now to ready to create, run and manage APIs in security.

# 5 - Expose an existing REST API

In this first step, we assume that a developer of an API is providing you the Swagger source associated with that API. The developer is using WAS Liberty as the runtime and he also uses JAX-RS annotations along api discovery feature. This allows him to get a Swagger easily consumed by API Connect.

In this lab, we are going to use the IBM Cloud to implement the API and the Developer Toolkit (in another lab).

> Note: Using the Developer Toolkit (locally) or using API Connect manager directly (remote server) is a pretty important decision. Using the toolkit allows to use a Source Control Management System and perform micro versioning as well as backup of the various yaml (and wsdl). It also provides a local experience with a very low response time. Using the Manager simplifies sharing the API Drafts. In reality, there are ways to benefit of both approaches.

### Task 12 :  Download the API swagger source to your laptop
Follow this link to download the source definition of the API. 

[Link Here](https://github.com/phthom/Using-IBM-API-Connect/blob/master/QuoteManagementAPI_AW_S.yaml)

or 

https://github.com/phthom/Using-IBM-API-Connect/blob/master/QuoteManagementAPI_AW_S.yaml

### Task 13 :  Create a Product
Depending where you are in the API Connect console, Click on the chevrons (**>>**) to get access to the navigation menu on the left side.

Choose **Drafts** to implement the product. 

![Draft](./images/i011a.png)

![Draft](./images/i011.png)

Click the **Add** button, select **New product**. 

![Add New Product](./images/i012.png)

In the Title section, enter **QuoteMgmt**.

![Fill in the product name](./images/i013.png)

Click **Create product** button.

![Back to Draft](./images/i014.png)
Go back to **All Products**.

### Task 14 :  Create (import) the API

Click on **APIs** in the menu.

Now we can create the API that will be included later in the Product just created. Click on **Add** and then on  **Import API from File or URL**.


![Add an API](./images/i015.png)

Specify the location of the Swagger file you just downloaded. Click **Import**.

![Upload the source API](./images/i016.png)

### Task 15 :  Modify the definitions of the API

We need to complete/review a few informations, that were not specified in the generated Swagger. The amount of information that need to be completed will depend greatly on the use of the annotations or the Swagger generator used.

Click on **Design** in the top menu.  
Select https for the scheme, in the Schemes section. 
![Design the API](./images/i018.png)

Create the security definition, click on + sign close to the Security Definitions section.

![Security Definitions](./images/i019.png)

Select **API Key**.

![Security Definitions](./images/i020.png)

Enter **client-id** in the name.

![Security Definitions](./images/i021.png)

Specify the security of the API, click on the + sign close to the Security section, and check the client-id API Key (3 steps)

![Security](./images/i023.png)

Create a property to define the target-url of the back end API. This allows us to create a variable that may take different values based on the catalog instance. Click on the + sign close to the Properties section. Set the Property name to **target-url**, and enter 
http://SampleJAXRS20-aw.eu-gb.mybluemix.net in the value, close to Default value. 

![Properties](./images/i025.png)

Click on the Assemble menu, click on the **Invocation** policy, and set the URL property to $(target-url)$(request.path)$(request.search)

![Assembly](./images/i027.png)

Save the changes, by clicking on the Save diskette icon at the top.

### Task 16 :  Testing the new created API

To test the API from an API provider perspective, click on Assemble, in the left hand side panel, switch from Micro Gateway policies to **DataPower Gateway** policies if necessary.
Save the change. Click on the **read icon**, check the catalog to run the API, select the **QuoteMgmt** product if necessary.

![Assembly](./images/i032.png)

Select the operation : **get /extQuote** 
> Don't click on the other buttons. 

![Test Assembly](./images/i050.png)

Enter the parameters (amount 1000, rate 1.1, duration 36, delay 10, msg length 11) and click invoke. 
> Don't change the generated Client ID.

![Test Assembly](./images/i052.png)

Here is a example of the answer :

![Results from Test Assembly](./images/i051.png)

### Task 17 :  Exploring the API

You can also test the API using the explore facility. You get a view similar to the API consumer in the portal, but in this case you do not need to create an Apps and subscribe to the API. Click on the **Explore** link on the top right, you see the documentation and have the possibility to test the various operations. 

Click on the **Sandbox** link :

![Back to Catalog Sandbox](./images/i053.png)

Select the operation : **get /extQuote** then click on **Try it**

![Try it](./images/i054.png)

Fill the request for the loan as you did previously and click on **Call Operation**

![Explore](./images/i055.png)

See the result of the request :

![Result from the Try it](./images/i056.png)

Click the X icon on the top right to close the explore window.

# 6. Publish your API to the Sandbox catalog

### Task 18 : Stage the API in the Sandbox Catalog

Within the Draft area, select the **QuoteMgmt** product :

![Stage](./images/i057.png)

In the APIs Section, add the **Quote API**, then **Apply** and click on the **Save** icon :

![Stage](./images/i059.png)

Click on **Publish icon** (cloud shape) in the top right corner, select Sandbox. This does effectively stage the product in the **Sandbox** catalog. The product is not yet published to the Portal. 

![Publish](./images/i058.png)


### Task 19 : Publish your API 

Click on the chevron (>>) and get access to the Dashboard, then click on the Sandbox tile :

![Back to Sandbox](./images/i060.png)

You should see the product just staged :

![Stage results](./images/i061.png)

Click on the dots link and select Publish :

![Publish](./images/i062.png)

Check the visibility and click on **Publish button**. 

![Visibility](./images/i063.png)

Your QuoteMgmt Product is now visible in Developer Portal.

# 7. Consumer Experience

In this step, you will learn the consumer experience for APIs that have been exposed to your developer organization. You login as a developer to register your application and then subscribe to the product just published and then test the API included in the product.



### Task 20 : Accessing the Developer Portal

Navigate to the Dashboard section and click on the Sandbox catalog tile. Click on Settings, then Portal and finally on the Portal URL :

![Link for the Developer Portal](./images/i070.png)

You are now on the Developer Portal, navigate to the API Products :

![Portal access](./images/i071.png)

You can now explore the API and Products (without login) :

![My API published in Portal](./images/i072.png)


### Task 21 : Sign in as a Developer Portal

From the Developer Portal, click on **Login**, create an account, then enter **your account information** for the developer account. **This must be a different email address than your IBM Cloud account**.  You can create a **email account** on mail.com for example. 

![Account Information](./images/i073.png)

A validation email will be sent out to the email address used at sign up. Click on the validation link and then you will have completed the sign up process and will be authenticated into the page.

Go to your email application, locate the new message and log in thru the link :

![Account Confirmation](./images/i075.png)

Log in into the developer portal as an application developer using your developer credentials.

![Account Login](./images/i074.png)


### Task 22 : Defining a Mobile Applocation

Click the **Apps menu**, then click on the **Create new App** button :

![Add new Application](./images/i076.png)


Enter a **title** and **description** for the application and click the **Submit** button.

![Application Information](./images/i077.png)

We need to capture the Client Secret and Client ID in a **text editor** for later use by our test application.

Client secret is at the top of the page :
![Application ID and Secret](./images/i078.png)

Client ID is at the bottom of the page :
![Application ID and Secret](./images/i079.png)

> **Copy Client Secret and Client ID in a text editor**


### Task 23 : Subscribe to a Plan for our Product

In this section, we will subscribe to a plan for the "QuoteMgmt" using the **Mobile App Consumer**  application.

- Click the API Products menu on the top of the page.
- Click the QuoteMgmt (v1.0.0) API product tile.
- Click on the **Subscribe** button under the Default plan.

![API access](./images/i080.png)

Select the Mobile App Consumer toggle and click the **Subscribe** button.

![Subscribe to the API](./images/i081.png)

The MobileApp Consumer application is now subscribed to the **Default plan** for the QuoteMgmt product.


### Task 24 : Test QuoteMgmt APIs from the Developer Portal

In this section, we will use the developer portal to test Quote Management API REST API. This is useful for application developers to try out the APIs before their application is fully developed or to simply see the expected response based on inputs they provide the API. We will test the Quote Management API REST API from the developer portal.

Click the **Quote link** on the left-hand navigation menu and then expand the **GET /quote** path by clicking on the twisty next to the path.

![Testing the API](./images/i082.png)

Scroll down to the **Try this** operation section for the GET /quote path. Enter your **Client ID** and your **Client secret** (if necessary - the credentials should be already set) and then click the **Call Operation** button

Scroll down below the Call operation button. You should see a **200 OK** and a **response body** as shown below.

![Testing the API](./images/i083.png)


### Task 25 : Test QuoteMgmt APIs from the Command Line


It is now time to test our API from the command line. 
From the previous cURL screen, Copy the cURL example from the left side into your text editor window replacing REPLACE_WITH_CLIENT_ID and REPLACE_WITH_CLIENT_SECRET with your client id and your client secret saved from the prior step

```
curl --request GET \
  --url 'https://api.eu.apiconnect.ibmcloud.com/philmetalmailcom-dev/sb/loanmgt/resources/loans/v1/extQuote?loanAmount=10000&annualInterestRate=1.1&termInMonths=36&delay=10&msgLength=725' \
  --header 'accept: application/json' \
  --header 'x-ibm-client-id: REPLACE_WITH_CLIENT_ID' \
  --header 'x-ibm-client-secret: REPLACE_WITH_CLIENT_SECRET'
 ```

You may have to add the client secret parameter. 

Copy and try it into your terminal windows.
Here is the result in a command line :

![cURL execution](./images/i084.png)


# 8. APIs Analytics

It is very important to get some analytics from the API Gateway when you want to follow errors, response time and hundreds of metrics from the your APIs, Catalogs, Products ... 


### Task 26 : Accessing the Analytics Dashboard


Return to the **IBM Cloud API Connect** screen.
Navigate to the **Dashboard** section and click on the **Sandbox** catalog tile.
Click on your **QuoteMngnt** Product and you can see number of subscriptions to you API.

![Account Information](./images/i085.png)

You can scroll down the analytics page. On the top right part of the page, there are some controls that you can use to change the visualizations in the page.
![Account Information](./images/i086.png)
![API Analytics](./images/i087.png)



### Task 27 : Customizing the Dashboard


> The default dashboard gives some general information like the 5 most active Products and 5 most active APIs. This information is interesting, but we can see much more information by customizing the dashboard. Add a new visualization by clicking on the ``+ Add`` Visualization icon.

![Visuatizations](./images/i088.png)

This will bring a list of some of the standard visualizations. You can then type in a string to filter through visualizations or use the arrows to page through the list.
Add the **Average Response Time** visualization to the dashboard by simply clicking on it. The new visualization will be added to the bottom of our dashboard. 

![Visuatizations](./images/i089.png)

The new visualization will be added to the bottom of our analytic dashboard. 

![Dashboard Customization](./images/i090.png)

# 9. Conclusion

###  Results
<span style="background-color:yellow;">Successful exercise ! </span>
You finally went thru the following features :
- [x] You logged in the  IBM Cloud
- [x] You created an instance of API Connect in the Cloud
- [x] You imported an API to that instance
- [x] You added API key and some security definitions to that API
- [x] You tested the API before publishing
- [x] You created an instance of the developer portal
- [x] You published your API Product to a catalog
- [x] You were able to subscribe as a developer to this API
- [x] You were able to test this API from the internet
- [x] Finally, you were able to see analytics on the APIs and Products.

---
# End of Lab
---
<div style="background-color:black;color:white; vertical-align: middle; text-align:center;font-size:250%; padding:10px; margin-top:100px"><b>
 Using IBM API Connect
 </b></a></div>