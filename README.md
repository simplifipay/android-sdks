**SimpliFiCard SDK Documentation**

SDK Name: SimpliFiCard

## Overview

The SimpliFi SDK provides a set of powerful functionalities for seamless integration into your mobile applications. With SimpliFi, developers can easily implement features related to card management and electronic Know Your Customer (eKYC) verification. This documentation will guide you through the installation process and provide detailed information about the available APIs.

## Table of Contents

1. [Installation](#installation)
2. [Initialization](#initialization)
3. [SimpliFiCard API Reference](#api-reference)
   - [showDetail()](#showdetail)
   - [requestPhysicalCard()](#requestphysicalcard)
   - [activateCard()](#activatecard)
   - [getPin()](#getpin)
   - [setPin()](#setpin)
4. [SFRequest Definition](#SFRequest-definition)
5. [SimpliFiEkyc API Reference](#simplifiekyc-sdk)
6. [Logging](#logging)
7. [Customizing UI](#customizing-ui)
8. [Security Considerations](#security-considerations)
9. [Release Notes and Versioning](#release-notes-and-versioning)
10. [Support and Contact Information](#support-and-contact-information)

## Installation

To integrate the SimpliFiCard SDK into your Android application, follow these steps:

1. Add the SimpliFiCard SDK dependency to your project's build.gradle file:
   ```
   implementation 'com.simplifi:card:3.0.0'
   ```

2. Sync your project with the updated dependencies.

## Initialization

Before using the SimpliFiCard SDK, you need to initialize it with the necessary configuration. Perform the following steps to initialize the SDK:

1. Import the SFCore SDK into your project:
   ```kotlin
   import com.simplifi.core.SFCore
   ```

2. Initialize the SFCore SDK by providing the base URL and the application context. This initialization should be performed in your application's `onCreate()` method or at an appropriate initialization point:
   ```kotlin
   SFCore.initialize(baseUrl, context)
   ```

Replace `baseUrl` with the base URL of the SimpliFiCard API, and `context` with the application context.

With these steps, the SimpliFiCard SDK is now ready for use in your application.

## API Reference

### showDetail()

```kotlin
SFCard.showDetail(request: SFRequest, context: Context)
```

The `showDetail()` method allows you to display the details of a SimpliFiCard.

- Parameters:
  - `request`: An instance of `SFRequest` containing the required information to retrieve card details.
  - `context`: The `Context` object representing the current application context.

This method presents the `CardDetailsActivity` to the user, showing the details of the requested SimpliFiCard.

### requestPhysicalCard()

```kotlin
SFCard.requestPhysicalCard(request: SFRequest, context: Context)
```

The `requestPhysicalCard()` method enables you to request a physical SimpliFiCard.

- Parameters:
  - `request`: An instance of `SFRequest` containing the required information to request a physical card.
  - `context`: The `Context` object representing the current application context.

This method presents the `RequestPhysicalCardActivity` to the user, allowing them to request a physical SimpliFiCard.

### activateCard()

```kotlin
SFCard.activateCard(request: SFRequest, context: Context)
```

The `activateCard()` method allows you to activate a SimpliFiCard.

- Parameters:
  - `request`: An instance of `SFRequest` containing the required information to activate a card.
  - `context`: The `Context` object representing the current application context.

This method presents the `ActivateCardActivity` to the user, guiding them through the card activation process.

### getPin()

```kotlin
SFCard.getPin(request: SFRequest, context: Context)
```

The `getPin()` method retrieves the PIN associated with a SimpliFiCard.

- Parameters:
  - `request`: An instance of `SFRequest` containing the required information to get the card's PIN.
  - `context`: The `Context` object representing the current application context.

This method presents the `GetPinActivity` to the user, allowing them to view the PIN associated with the SimpliFiCard.

### setPin()

```kotlin
SFCard.setPin(request: SFRequest, context: Context)
```

The `setPin()` method allows you to set a new PIN for a SimpliFiCard.

- Parameters:
  - `request`: An instance of `SFRequest` containing the required information to set a new PIN.
  - `context`: The `Context` object representing the current application context.

This method presents the `SetPinActivity` to the user, guiding them through the process of setting a new PIN for the SimpliFiCard.

## SFRequest Definition

The `SFRequest` data class represents the necessary parameters required by the SimpliFiCard SDK methods.

### SFRequest Properties

- `userUuid`: A `String` representing the user's unique identifier.
- `cardUuid`: A `String` representing the SimpliFiCard's unique identifier.
- `companyUuid`: A `String` representing the company's unique identifier.
- `token`: A `String` representing the authentication token for API requests.

Make sure to provide the correct values for these properties when making API calls using the SimpliFiCard SDK.

That concludes the documentation for the SimpliFiCard SDK. You are now equipped with the necessary information to integrate SimpliFiCard functionality into your Android application effectively.

## SimpliFiEkyc SDK

The SimpliFiEkyc SDK provides eKYC (Electronic Know Your Customer) capabilities. To use this SDK, follow the steps below:

1. Add the SimpliFiEkyc SDK dependency to your project's build.gradle file:
   ```
   implementation 'com.simplifi:ekyc:3.0.0'
   ```

2. Import the `SFKyc` class into your project:
   ```kotlin
   import com.simplifi.ekyc.SFEKyc
   ```

3. To start the eKYC journey, use the `start()` method of the `SFKyc` class:
   ```kotlin
   SFEKyc.start(request, context, callback)
   ```

   - Parameters:
     - `request`: An instance of `SFRequest` containing the required information for eKYC.
     - `context`: The `Context` object representing the current application context.
     - `callback`: An implementation of the `EkycCallback` interface to handle eKYC events and errors.

4. Implement the `EkycCallback` interface to handle the eKYC events and errors:
   ```kotlin
   interface EkycCallback {
       fun onJourneyStarted(journeyId: String)
       fun onJourneyResumed(journeyId: String)
       fun onJourneyCancelled(journeyId: String?)
       fun onJourneyCompleted(journeyId: String, isSucceeded: Boolean)
       fun onError(error: EkycError)
   }
   ```

   - The `onJourneyStarted()` method is called when the eKYC journey is started, providing the journey ID.
   - The `onJourneyResumed()` method is called when the eKYC journey is resumed, providing the journey ID.
   - The `onJourneyCancelled()` method is called when the eKYC journey is cancelled, providing the journey ID (nullable).
   - The `onJourneyCompleted()` method is called when the eKYC journey is completed, providing the journey ID and a boolean flag indicating whether the journey was successful.
   - The `onError()` method is called when an error occurs during the eKYC journey, providing the `EkycError` object.

## Logging

The SimpliFiCard SDK includes SimpliFiLogger SDK, which logs any network errors to Mixpanel. By default, logging is enabled. You can enable or disable logging using the following methods:

To enable logging, use:
```kotlin
SFLogger.enableLogging()
```

To disable logging, use:
```kotlin
SFLogger.disableLogging()
```

By enabling logging, network errors will be logged to Mixpanel for analysis and troubleshooting purposes.

## Customizing UI

The SimpliFiCard SDK allows you to customize the look and feel of the views displayed by the SDK. To change UI elements, you can use the `ThemeOptions` class.

### ThemeOptions

The `ThemeOptions` class provides methods to customize the UI elements used by the SimpliFiCard SDK. You can customize the following elements:

- `headerFont`: Specifies the font for the header text.
- `bodyFont`: Specifies the font for the body text.
- `buttonBackgroundColor`: Specifies the background color of buttons.
- `buttonTextColor`: Specifies the text color of buttons.
- `screenBackgroundColor`: Specifies the background color of screens.
- `textColorOnCard`: Specifies the text color on the card.

Here's an example of how to use the `ThemeOptions` class:

```kotlin
val themeOptions = ThemeOptions.Builder()
    .setHeaderFont(FontFace.Montserrat)
    .setBodyFont(FontFace.Montserrat)
    .setButtonBackgroundColor("#FF0000")
    .setButtonTextColor("#FFFFFF")
    .setScreenBackgroundColor("#F0F0F0")
    .setTextColorOnCard("#000000")
    .build()
```

You can set the desired font using the `setHeaderFont()` and `setBodyFont()` methods, providing one of the available

 `FontFace` options (`Roboto`, `Montserrat`, `F29LTBukra`).

To customize the button background color, use the `setButtonBackgroundColor()` method, providing a color in hexadecimal format.

To customize the button text color, use the `setButtonTextColor()` method, providing a color in hexadecimal format.

To customize the screen background color, use the `setScreenBackgroundColor()` method, providing a color in hexadecimal format.

To customize the text color on the card, use the `setTextColorOnCard()` method, providing a color in hexadecimal format.

After customizing the theme options, you can set them to the SFCore SDK using the following code:

```kotlin
SFCore.theme = themeOptions
```

By customizing the theme options, you can align the appearance of the SDK with your application's design and branding.

## Security Considerations
SimpliFi SDKs prioritize security when handling sensitive data, such as card information and user

 verification details. The SDKs implement encryption mechanisms and follow industry best practices to ensure the confidentiality and integrity of the data. However, it is essential to implement additional security measures in your application to protect user data and comply with relevant regulations.

## Release Notes and Versioning
- SimpliFiCard SDK, version 3.0.0
  - Show card details.
  - Request physical card.
  - Activating card.
  - Retrieving PIN.
  - Setting PIN.
 
- SimpliFiEKyc SDK, version 3.0.0
  - eKYC verification journey.

## Support and Contact Information
If you need any assistance or have questions regarding SimpliFi SDKs, you can reach out to our support team at support@simplifipay.com.
