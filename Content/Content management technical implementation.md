<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

# Introduction
Based on the definitions listed at “Content organization.md”, a solution architecture must be defined. It will contain the the conceptual design technical implementation.

# Meta-data management
At its first incarnation, all metadata related to the different objects used to deliver our courses will be manager using Google Sheets.

Besides its simple implementation, Google Sheets offers additional advantages:
- native integration with GBQ;
- possible to increase control and usability with simple scripting.

One spreadsheet will be used to manage all objects. Each object will have its own sheet. In addition, many-to-many relationships between two objects will get a dedicated sheet.

Keys and file links will be generated automatically. To help data entry, value lists will be provided. Status will be also managed automatically.

# File storage
GCS will be used to store and serve contents and parts. One bucket will be dedicated to contents and a second one to parts. Files will be named after the content id plus extension. Contents and parts should be upload to GCS only after the creation process is completed.

# LMS population
Hierarchy, groups and contents with status 02 Testing and 03 Active will be created at the LMS. Hierarchy will give origin to courses. Contents are to be uploaded to form the course activities. Groups will generate categories and groups.

At first, all integration will be done by hand.