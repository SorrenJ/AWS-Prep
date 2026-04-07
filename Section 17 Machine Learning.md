
# Rekognition

Find objects, people, text, scenes in images and videos using ML

Facial analysis and facial search to do user verification, people counting

Create a database of “familiar faces” or compare against celebrities


# Transcribe

Automatically convert speech to text, using automatic speech recogntion (ASR)

automatically removing Personally Identifiable Information (PII) using reduction -> removing someone's age or name, SIN
Use cases: 

- supports automatic language identification for multilungual

- transcribe customer service calls
- automate closed captioning and subttitling
- generate metadata for media assets

# Polly

Turn text into lifelike speech using deep learning

creates applications that talk

# Translate

Natural language and accurate language translation

Use cases:

- localize content for websites, and applications, especially international users, to easily translate large volume of text efficently


# Lex 

 automatic speech recognition, Natural language Understanding to recognize the intent of text, callers, helps build chatbots


# Connect

virtual contact center, recieve calls, create contact flows 

integrates with CRM or AWS

no upfront payments

Example




![[Screenshot 2026-03-07 213450.png|587]]



a phone call to schedule an appointment that is made into a number that is defined by Amazon Connect. So they call Amazon Connect. Lex is streaming all the information from this call and understand the intent of the phone call, and therefore, it will invoke the right lender function.

And that lender function, for example, can be very smart and say, "Hey, someone has said to schedule a meeting tomorrow with Tom at 3:00 PM." Okay, I will go into my CRM and schedule that meeting by writing some code.

# Comprehend

Natural Language Processing (NLP)

Fully managed and serverless service uses ML to find insights and reltionhips in texts

For example, it can understand what is the language of the text, it can extract key phrases, places, people, brands, or events from that text. It can understand, do a sentiment analysis to understand how positive or negative the text you're analyzing is. It can also analyze a text using tokenization and parts of speech.

Use cases:
analyze customer interactions (emails)
create and group articles by topics that Comprehend will uncover

# SageMaker AI

Used to build ML models

Here you can feed historical data, label columns, give prediction scores, train and fine tune, apply the machine learning model, and make it learn from new data


# Kendra

Fully managed, ML document search service, like Google

extract answers from any documents 

Can also learn from user interactions (incremental learning)

Examples: 

if a user says, Hey, where is the IT support desk into Amazon Kendra?
Kendra can reply, 1st floor. And this could be due to the fact that Kendra knows from all the resources that it took that the IT support desk was on the 1st floor


# Personalize

A ML service that personalizes reccomendations based on the user

Example: amazon shopping, retail store recommendations, entertainment

Integrates into existing web app, SMS, email marketing systems

you dont need to train, build, or deploy ML solutions

# Textract

Extraxts text, hnadwriting, and data from any scanned documet

use cases 
Financial services (invoices, financial reports), Healthcare (medial records, insurance claims), public sector (tax forms)


# Quiz

Question 1:

You should use Amazon Transcribe to turn text into lifelike speech using deep learning.

False

Transcribe is an AWS service that makes it easy for customers to convert speech-to-text. Amazon Polly is a service that turns text into lifelike speech


Question 2:

A company would like to implement a chatbot that will convert speech-to-text and recognize the customers' intentions. What service should it use?

Lex


Question 3:

You would like to find objects, people, text, or scenes in images and videos. What AWS service should you use?

rekognition

Question 4:

A start-up would like to rapidly create customized user experiences. Which AWS service can help?

personalize

Question 5:
A research team would like to group articles by topics using Natural Language Processing (NLP). Which service should they use?

comprehend

Question 6:

A company would like to convert its documents into different languages, with natural and accurate wording. What should they use?

Translate

a neural machine translation service that delivers fast, high quality, and affordable language translation

Question 7:
A developer would like to build, train, and deploy a machine learning model quickly. Which service can he use?

SageMaker

is a fully managed service that provides every developer and data scientist with the ability to build, train, and deploy machine learning ,models quickly. SageMaker removes the heavy lifting from each step of the machine learning process to make it easier to develop high quality models

Question 8:
Which AWS service makes it easy to convert speech-to-text?

Transcribe

Question 9:

Which of the following services is a document search service powered by machine learning?

Kendra