---
layout: page
title: Vaccine Distribution System
description: Tool that models the flow of vaccines through various distribution channels
img:
importance: 2
category: school
---

<em>Authors:</em> Inbar Ofer and Daniel Rosenman

- Click [here](https://youtu.be/4qWIzNc5ybQ) to view project demo.
- Click [here](https://github.com/inbaro-neu/vaccine_distribution) to view GitHub repository.


## Description

Our system provides an example of a vaccine distribution/sign-up system that could be used to support the COVID-19 vaccine distribution efforts. Currently, the vaccine distribution efforts in the United States are going quite slowly compared to other countries, and the large population of the United States contributes to the challenge. The United Kingdom has thus far relied on a much more centralized approach to vaccine distribution. According to Tinglong Dai, associate professor of operations management and business analytics at the Johns Hopkins University Carey Business School, “the NHS knows who these people are that are getting the vaccine. The NHS notifies people when it is their turn. It’s much more streamlined compared to what we have here in the U.S.” Currently, the United States has several distinctions to determine who should receive the vaccine first. These distinctions, such as two or more comorbidities or essential worker status, seem reasonable, but, as The Wall Street Journal mentions, “the cost in delay and confusion is high.” Age is a statistic that is readily available about individuals to the government, hospitals, pharmacies, and doctor’s offices. Therefore, we believe that developing a more centralized system for vaccine distribution that is based on age is the most effective way for getting the vaccine out to as many people as possible as quickly as possible.

### What the System Can Do

The system could receive citizen data from the government regarding social security number, home address, birth date, and gender. The system could also receive other types of data, including vaccine information and doses, and staff, clinic, and appointment information. We have provided example data for the purpose of testing the project because that kind of personal data is not available to us.

A user (citizen or staff) receives a code to create an account. When they click to sign up, they are prompted to enter that code so that they are assigned the correct permissions. Each user type then has a different flow, which can be seen in the activity flow below.

<em>Types of users:</em>
- Health care providers, such as nurses, doctors, and pharmacists who will be administering the vaccine doses to citizens
    - This type of user can view the clinic information, delete a patient from the system, view upcoming appointments, and add new available appointments to the system.
- Citizens
    - This type of user will be able to schedule an appointment when a vaccine dose is available to them.

## Interest

Vaccine distribution is the number one problem the US is currently facing (as of project creation). The US has been experiencing great difficulties with managing the logistics of the vaccine distribution process. We believe that it is crucial for the US to be able to manage vaccine distributions and keep track of vaccines so it can move the vaccination process as quickly and efficiently as possible. We are both concerned about the situation of the US economy which is still in large part closed and is reliant on constant stimulus injections by the fed, and we want high risk groups to get vaccinated as quickly as possible so the economy can open and recover. Therefore, we are working on creating a data management system which will allow easy and efficient tracing of vaccinations and will help prioritize high risk groups.

## Technical Specifications

We used SQL storage for our relational database and Java to connect to it, since our database is accessible via the command line. For developing the project, we used our personal laptops to write code and Github for version control and ease of code-sharing and merging.

## Design

### Conceptual Design

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project4_conceptual_design.png" title="Conceptual Design" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Logical Design

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project4_logical_design.png" title="Logical Design" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Flow Chart

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project4_flowchart.png" title="Flow Chart" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## Future Work

### Potential Areas for Added Functionality

There are many areas for added functionality in this database. These types of databases can be scaled incredibly, so much so that even the CDC has not implemented a perfect or even near-perfect solution for vaccine distribution and sign up. Other user types could be added to the database, including the following:

- Government officials
    - This type of user will be able to access database information and contact information for vaccine providers, health care providers, and citizens in order to confirm that the vaccine distribution is going as planned
    - This type of user will also be able to access patient information in order to send out notices that a vaccine dose is ready for the patient, and which clinic they should contact to schedule an appointment
- Vaccine providers, such as employees from Pfizer, Moderna, and Johnson & Johnson
    - This type of user will be able to log the number of vaccines available and already distributed from their company

Beyond adding additional user types, additional functionality could be added to existing users. Citizens could view their past appointments and add side effects they’ve had from their vaccine dose(s). Clinic staff could add appointment notes to the database. The addition of side effect notes and appointment notes would be novel because that is not currently a feature in the CDC VAMS database. However, it would greatly improve the centralization of the vaccine distribution and help with tracking the vaccination efforts’ success.

Some other important improvements would be:

- Making sure that the user who signs up is of age to receive the vaccine. Currently, we are relying on the assumption that a user who has received a code to sign up must be of age (because they would have received the code from the government or a clinic, someone who has their information).
- Adding support for different vaccine types. Currently, our vaccine system only supports vaccines that require two doses, as both of the current vaccines that are available (Pfizer and Moderna) require two doses. In the future, support for additional vaccine types, such as the currently on hold Johnson & Johnson, could be added.

## References

- https://www.wsj.com/articles/vaccination-by-age-is-the-way-to-go-11610476439
- https://www.usnews.com/news/best-countries/articles/2021-02-04/supply-distribution-logistics-key-to-countries-covid-19-vaccination-efforts
- https://www.cdc.gov/phlp/publications/topic/hipaa.html
- https://www.mindk.com/blog/how-to-make-your-health-care-app-hipaa-compliant/
