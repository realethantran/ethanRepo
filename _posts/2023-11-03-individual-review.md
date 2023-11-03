---
toc: True
comments: True
layout: post
title: Individual Review - Ethan Tran
description: None
type: hacks
courses: {'csa': {'week': 11}}
---

# Code Contribution - Spacebook

### Image to Base64 Code
- Specify the base URL path so that all endpoints are relative to /image
- GET request mapping fetches all records from our database

![image](https://github.com/realethantran/ethan_student/assets/109186517/b2cbf7f6-da10-46ef-b1e0-756ae200220a)

- The POST request saves the uploaded file and fileName
- Uploaded image is then encoded to Base64 string, so that it can be stored as text in our database
- A new file is then made with the fileName and the encoded string

![image](https://github.com/realethantran/ethan_student/assets/109186517/e149d667-9d72-4c68-9412-f478b4fcb471)

- Images can be accessed via the endpoint "/image/{fileName}"
- If the image is present, then the Base64 string is retrieved and decoded back into binary format

![image](https://github.com/realethantran/ethan_student/assets/109186517/0159c9ec-1f6f-4686-8e88-cb6b5fc704fa)

- Check format of file and adjust media type accordingly 

![image](https://github.com/realethantran/ethan_student/assets/109186517/d208426d-45e0-4b15-8b16-1b826c4921bf)

## Frontend integration

### Image Viewer
- Fetches the image from the backend based off value of fileName input by the user
- URL is created for the blob (binary large object) to use it as an image source on the page

![image](https://github.com/realethantran/ethan_student/assets/109186517/6f0da296-8235-4ed7-9541-e5095cd6f789)

### Upload Image

![image](https://github.com/realethantran/ethan_student/assets/109186517/d9c6db1b-0f6e-49c2-8d16-1afabc992832)

# GitHub Analytics 

![image](https://github.com/realethantran/ethan_student/assets/109186517/08ce10ce-54bb-44a8-916d-61b23f11e7cc)

- [Notable Frontend Commit](https://github.com/Cosmic-Carnage/Passion-Project/commit/83ac2150b402a454d7bdd11461c5ced79e572299) - Adding Spacebook + View Image

- [Notable Backend Commit](https://github.com/Cosmic-Carnage/cosmic_backend_final/commit/58d56fe661c420adb53037f3c6659447e82dc978) - Setting up mapping + Image to Base64

# My Blog
[Link](https://ethan.nighthawkcodingsociety.com/)