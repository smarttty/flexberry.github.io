---
title: Module1. Check-list check for jobs
keywords: Programming, Training, Developers school
sidebar: training-developers-school_sidebar
toc: false
permalink: en/tds_module1-check-list.html
lang: en
autotranslated: true
hash: a47946046e17a2ce2c216d48903aea7398e5958a42254aca5cea0c8dd0615821
---

### Task 1. Creating a web application based on REST API

The application must be implemented in a REST-based API using a JSON Server. Failure to comply with this requirement, the points for the assignment will not be counted!

1. On the main page of the application displays the list of invoices: **1 point**.
2. New feature: invoices: **1 point**.
3. Implemented change invoices: **1 point**.
4. Implemented deletion of invoices: **1 point**.
5. Implemented filtering of rows displayed by the value of the selected field: **2 points**.
6. Implemented full text search on all fields: **1 point**.
7. Implemented sorting by a single field in three modes: “sort”, “ascending”, “descending”: **1 point**.
8. Filter, sort and search can work together: **1 point**.
9. The server is deployed on Heroku: **2 points**.
10. The app is published on GitHub Pages: **1 point**.

**Total job**: 12 points.

### Task 2. Testing networking and server-side API

1. There are screenshots of HTTP responses from Chrome Chrome Developer Tools, Fiddler and Postman for the following query: "retrieve all invoices that any field which contains the number “7”": **1 point**.
2. There are screenshots of HTTP responses from Chrome Chrome Developer Tools, Fiddler and Postman for the following query: "retrieve all invoices that the value of the field number less than “100000”": **1 point**.
3. Are screenshots of the HTTP response from Postman and Fiddler for the request to create the invoice: **1 point**.
4. Are screenshots of the HTTP response from Postman and Fiddler for the change request invoice: **1 point**.
5. Are screenshots of the HTTP response from Postman and Fiddler for the request to delete the invoice: **1 point**.
6. The collection in Postman, which implements the tests for obtaining all invoices add invoices, edit invoices, delete invoices. The collection is exported to .a json file that is published in the repository on GitHub: **4 points** (one point for each completed test in the collection).
7. The collection in Postman, which implements the tests for obtaining all invoices filtered by the field value. The field name and its value are specified in the environment variables. For this test, prepared and published in the repository on GitHub a file with a JSON array of values of the variables (each field of the invoice corresponds to one element of the array). A collection of environment variables exported in .json files, which are published in the repository on GitHub: **4 points**.
8. A screenshot of the terminal with rezultatm run the test collections with Newman: **2 points** (one point per screenshot at the start of each collection).

**Total job**: 15 points.

## You can

* [Go to next module](tds_module2-about.html)
* [Go to the page with the jobs plugin](tds_module1-appendix.html)



{% include callout.html content="Переведено сервисом «Яндекс.Переводчик» <http://translate.yandex.ru>" type="info" %}