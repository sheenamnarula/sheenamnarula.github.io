+++
# A Projects section created with the Portfolio widget.
widget = "portfolio"  # See https://sourcethemes.com/academic/docs/page-builder/
headless = true  # This file represents a page section.
active = true  # Activate this widget? true/false
weight = 50  # Order that this section will appear.

title = "Projects"
subtitle = ""

[content]
  # Page type to display. E.g. project.
  page_type = "project"
  
  # Filter toolbar (optional).
  # Add or remove as many filters (`[[content.filter_button]]` instances) as you like.
  # To show all items, set `tag` to "*".
  # To filter by a specific tag, set `tag` to an existing tag name.
  # To remove toolbar, delete/comment all instances of `[[content.filter_button]]` below.
  
  # Default filter index (e.g. 0 corresponds to the first `[[filter_button]]` instance below).
  filter_default = 0
  
  # [[content.filter_button]]
  #   name = "All"
  #   tag = "*"
  
  #z [[content.filter_button]]
  #   name = "Deep Learning"
  #   tag = "Deep Learning"
  
  # [[content.filter_button]]
  #   name = "Other"
  #   tag = "Demo"

[design]
  # Choose how many columns the section has. Valid values: 1 or 2.
  columns = "2"

  # Toggle between the various page layout types.
  #   1 = List
  #   3 = Card
  #   5 = Showcase
  view = 3

  # For Showcase view, flip alternate rows?
  flip_alt_rows = false

[design.background]
  # Apply a background color, gradient, or image.
  #   Uncomment (by removing `#`) an option to apply it.
  #   Choose a light or dark text color by setting `text_color_light`.
  #   Any HTML color name or Hex value is valid.
  
  # Background color.
  # color = "navy"
  
  # Background gradient.
  # gradient_start = "DeepSkyBlue"
  # gradient_end = "SkyBlue"
  
  # Background image.
  # image = "background.jpg"  # Name of image in `static/img/`.
  # image_darken = 0.6  # Darken the image? Range 0-1 where 0 is transparent and 1 is opaque.

  # Text color (true=light or false=dark).
  # text_color_light = true  
  
[advanced]
 # Custom CSS. 
 css_style = ""
 
 # CSS class.
 css_class = ""
+++

## Ecommerce Platform
This is a product for a renowned fashion brand in Singapore which is having offline stores and online website for women clothes.
#### Technology Stack
NodeJS, NestJS, AWS Clouds Services (S3, SQS, Lambda), Docker, Kubernetes, Gitlab CI/CD, Slack Integration, Elasticsearch

##### Job roles and responsibilities:
```
. Architecture design and flow of the project.
. Acted as an Engineering Manager for the team
. Implementation of apis and migrating the existing one for performance improvement
. Implementation of authentication using KONG 
. Integration of Redis cache
. Dockerization of the project
. CI/CD pipelines for automating deployment
. Troubleshooting on EKS (in case devops are not available to support the team)
. SQS integrations and handling of failures in message processing
. Creating and updating Route53
```
--------------------
## Smart Conference Room 

This is a combination of Speech technology and IOT (Internet of Things) together. In this project, a conference room is made smart by deriving a meeting end to end through voice. In this project, following devices and applications were controlled through voice:
- Projector (integrated using IOT and Embedded concepts) 
- Lights (using IOT and Embedded concepts)
- PDF reader (For Presentation) 
- VLC media player (To play a video)

#### Technology Stack
Python, Embedded C, Arduino and Nodemcu (Hardware), Dialog flow Api provided by Google, Snowboy

##### Job roles and responsibilities:
```
    . Technically lead the project
    . Trained resources on IOT concepts
    . Integrated Snow boy for detection purposes
    . Integrated Dialog flow api for intent detection and streaming of voice
    . Decoded projector commands so that can be further coded in the required way
    . Worked on IR and Nodemcu to control the projector
```
----------------------------
    
## Synthetic Data Framework

This project was about the generation of data (screenshots and corresponding Json) for the training purpose of Machine learning models.

#### Technology Stack
NodeJS, Express, for storage used GCS Buckets, Docker

##### Job roles and responsibilities:
```
    . Technically lead the team
    . Architecture design and flow of project
    . Handled backend completely 
    . Implementation of templating engine in right way
    . Containerization of the application
    . Scaling of application
```
--------------------------------
## K-LITE

This project is to visualize the Machine learning data in filtered form as we do in Kibana, but along with other interesting features as well like drawing bounding boxes to label data in real time.

#### Technology Stack
NodeJS, Graphql, HapiJS, Elasticsearch, for storage supported 3 platforms AWS, GCS, AZURE, Kubernetes, Docker, ReactJS (Frontend)

##### Job roles and responsibilities:
```
    . Technically lead the team
    . Handled backend completely and designed the architecture of the project
    . Supporting in frontend issues (In case of Production)
    . Containerization of the application
    . Set up to automate the deployment process
```

-------------------------
## Banking Sector

This tool is used to manage the loan specifications. At some places, like in Canada , loan interest rates are not predefined.These are calculated on the basis of earnings and expenditure of a person who is applying loan. Basically.a person can bargain for loan interest rate.So to manage all these things, this tool has some formula which can calculate interests and keeps record of every bargain and also about interest rates provided by competitor parties so that manager can see all the record at one place and can approve or reject loan.

#### Technology Stack
NodeJS
##### Job roles and responsibilities:
```
    • Worked as a Backend developer.
    • Migration of APIs from meteor to node.
```
-------------------
## Samarthya

The project was an employment portal where skilled workers can come and register as a job seeker and employers can search for the workers on the basis of the work showcased by the job 
This project has two parts


#### Technology Stack
NodeJS, MongoDB, Email Integration
##### Job roles and responsibilities:
```
    • Worked as a backend developer.
    • Email Integration using nodemailer.
    • Stripe integration for the subscription of premium accounts.
    • Twilio integration for SMS notifications.
  ```
 --------------------
## Cheforder

The project was a catering app where a customer can pre book a chef or caterer.Chefs can register and can easily get orders.


#### Technology Stack
MeteorJS, MongoDB, Twilio for SMS, Stripe (Payment Gateway)

##### Job roles and responsibilities:
```
    • Worked as a backend developer.
    • Implemeted all crud operations along with required flow of application.
    • Email Integration.
    • Stripe integration for payment to business users.
    • Twilio integration for SMS notifications.
    • Fcm-node integration for mobile notifications
    • Implemented logic for cron jobs for ontime auto credit of payments.
```
----------------
## Konnect

This project was mainly Uber like in technical implementation but this is to book car cleaners and services.In this project, customer role is there to book cleaners. But car cleaners can be manager and can hire further persons for work.For this purpose, a management portal was also a part of this project.

#### Technology Stack
Nodejs, Graphql, MongoDB
##### Job roles and responsibilities:
```
    • Managed a small team of interns who were learning graphql.
    • Worked as a backend developer.
    • Implemented graphql subscriptions for real-time requests for the services
      to the agents.
    • Integrated Stripe for online payments.
    • Integrated apis for management portal using redux architecture in react.
```
------------------

## Brang

It was an app like Olx where customers can post pics of articles. They can act as sellers and buyers both.
#### Technology Stack
Nodejs, MongoDB, Mango pay 


##### Job roles and responsibilities:
```
    • Worked as a backend developer
    • Developed custom subscription module for auto-payment as mango pay does
      not support subscriptions.
```
--------------------
## Node Cli

This project is about offering cli commands so that a non-technical person can come to an instance and up the project using one command. (before we use auto-deployment)
#### Technology Stack
Nodejs


##### Job roles and responsibilities:
```
    . Development of scripts which can run and deploy project on instance.

```




