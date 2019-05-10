---
title: include file
description: include file
services: active-directory
documentationcenter: dev-center-name
author: danieldobalian
manager: CelesteDG
editor: ''

ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/20/2019
ms.author: dadobali
ms.custom: include file 

---

# Sign in users and call the Microsoft Graph from an Android app

In this tutorial, you'll learn how to build an Android application and integrate it into Microsoft identity platform. Specifically, this app will sign in a user, get an access token to call the Microsoft Graph API, and make a basic request to the Microsoft Graph API.  

When you've completed the guide, your application will accept sign-ins of personal Microsoft accounts (including outlook.com, live.com, and others) and work or school accounts from any company or organization that uses Azure Active Directory.

## How the sample app generated by this guide works

![Shows how the sample app generated by this tutorials works](media/active-directory-develop-guidedsetup-android-intro/android-intro.svg)

The app in this sample will sign in users and get data on their behalf.  This data will be accessed via a remote API (Microsoft Graph API in this case) that requires authorization and is also protected by Microsoft identity platform.

More specifically:

* Your app will launch a web page to sign in the user.
* Your app will be issued an access token for the Microsoft Graph API.
* The access token will be included in the HTTP request to the web API.
* Process the Microsoft Graph response.

This sample uses the Microsoft Authentication library for Android (MSAL) to be coordinating and helping with Auth. MSAL will automatically renew tokens, deliver SSO between other apps on the device, help manage the Account(s), and handle most Conditional Access cases.

## Prerequisites

* This guided setup uses Android Studio 3.0.
* Android 21 or later is required (25+ is recommended).
* Google Chrome or a web browser that uses Custom Tabs is required for this version of MSAL for Android.

## Library

This guide uses the following authentication library:

|Library|Description|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Microsoft Authentication Library (MSAL)|