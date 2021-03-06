SMS
===

Basic system for managing student records


Introduction
************

This project is a server-based student management system. It allows users to register students, as well view, edit and
track information ranging from their current classes, event calendar, timetables, communications and basic book keeping
and online accounts payments.

The project is based around Python (2.7), Django (1.7) and PostgreSQL (9.3) and has been developed to run on Linux
based systems.


Requirements
************

1. First install Python (2.7), Django (1.7) and PostgreSQL (9.3).

2. After installing Django, also install a django app called 'autofixture'. This is used to automatically populate the
database with data, primarily usefull for testing. Django 1.7 should come with pip already installed, so you can use
this command to install autofixture from the command line :~ pip install django-autofixture

  .If you would not like to use it, remember to remove it from installed apps in the settings.py file.
  
  
Design Philosophy
*****************

The following philosophies have shaped the development of this project:

1. DRY (Do not Repeat Yourself) - as far as possible, any code that need not be repeated is not, primarily to save on
design time. With Student and Staff models, for example, 95% of their behaviour is inherited from a single base class
which also hooks them direcly into django's own user authentication and session handling framework.

2. Explicitly Defined - This comes in two parts, one that any business logic that is used regularly or by various apps
(except when it comes to handling forms, e.g. the contact us form and event creation forms) must be defined as a
function. This improves readability and helps ensure sticking to DRY. The other half of the coi is that whenever
functions and models are used, and this applies particularly to importing modules, the desired components should
ideally be imported explicity. This is primarily to avoid naming conflicts, particularly with the inbuilt django
modules and functions.

3. Walk Softly, Carry a Big Stick - The sytem is designed to be as light-weight and simple as possible, except for key
performance issues (which is why PostgreSQL is used in favor of MySQL or SQLite). It is designed to be run on Python,
Django, PostgreSQL, Gunicorn and Ngninx. This is very light-weight (much smaller total file-size and resource needs than
could be achieved with other options such as MySQL and PHP) and more simple (whilst Apche offers a wider array of
settings, the majority of them add nothing to our project).

4. Python First - As a programming language, Python takes priority. It means that for any functionality required by the
system, the first port of call is to try find a way to solve the problem uing Python. Success messages after sending
e-mails are generated using python code, for example. The reasons for this are: a) As a developer, I am focused on
Python, primarily because of its maturity, future growth prospects (very heavily backed by large corporations) and
versatility, but also because I am focused on general application development, Django is just the best way of
developing this particular application. b) Python is very easy to learn, and it reduces the complexity caused by using
other languages (I believe it more effective to know a lot about Python and a little bit about the rest, than to have
mediocre knowledge of everything). Whilst in some respects this affects performance (with simple arithmetic, PHP is
much faster than Python) Python provides better scalability, ease of development and cohesion in the logic.
  

Outline
*******

Major functional aspects of the site are broken up into several discrete apps. All of the apps listed below have been
created for the SMS system. Whilst some apps, for example the calendar app, are effectively stand alone, some are
closely related, although the goal is for each app to stand completely alone. Those marked with an asterix (*) are
either still in the very early stages of development or still rapidly changing.

bookkeeping* - Basic bookkeeping functions

cal - calendar with the ability to add and display events and send e-mail reminders.

msg_box - handles delivery of internal communications to students as well as e-mails (sent from a suitable gmail account
accessible to the server).

office* - handles the storage and manipulation of student and staff records, including associated classes, student
results, etc.

sms_admin* - provides the means for users to actually create, view and manipulate information on the system. It
basically ties all of the apps together and presents them in a logical way (as an aside, the admin's color scheme
is a nod to the admin panel that comes with django).
