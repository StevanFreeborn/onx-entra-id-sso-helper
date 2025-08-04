# Onspring Entra ID SSO Helper

This repository provides an interactive web-based tool to help users register an application in Microsoft Entra ID (formerly Azure AD) and pre-configure its Single Sign-On (SSO) settings for use with [Onspring](https://onspring.com) using the SAML 2.0 protocol.

## Overview

Setting up SSO integration between Onspring and Microsoft Entra ID typically requires manual configuration through the Azure portal, involving multiple steps and technical knowledge of SAML configuration. This tool automates the entire process, making it accessible to users who may not be familiar with the intricacies of SAML setup.

## Demo

https://share.stevanfreeborn.com/onx-entra-id-sso-helper/example.mp4

## What This Tool Does

The application performs the following automated steps:

1. **Creates a Custom App Instance**: Instantiates a new enterprise application from Microsoft's custom SAML template
2. **Configures Default Claims Mapping**: Sets up the required claim mappings that Onspring expects:
   - `NameID` (Unique User Identifier) → `user.userprincipalname`
   - `Email` → `user.mail`
   - `FirstName` → `user.givenname`
   - `LastName` → `user.surname`
3. **Sets SAML Mode**: Configures the application to use SAML 2.0 as the preferred SSO method
4. **Configures URLs**: Sets the Identifier (Entity ID) and Reply URL based on your Onspring instance
5. **Generates Signing Certificate**: Creates a new token signing certificate for secure SAML assertions
6. **Provides Metadata**: Retrieves all necessary information for Onspring support to complete the integration

## Features

- **Progressive Visual Feedback**: Animated checkmarks show the completion of each step
- **Responsive Design**: Works on desktop and mobile devices
- **Dark/Light Theme Support**: Automatically adapts to your system's theme preference
- **Error Handling**: Comprehensive error messages and recovery options
- **No Server Required**: Runs entirely in the browser using Microsoft's JavaScript SDKs

## Prerequisites

- An active Microsoft 365 or Azure AD tenant
- Global Administrator or Application Administrator privileges in your tenant
- An Onspring instance URL
- Modern web browser with pop-up support enabled

## How to Use

1. **Sign In**: Click the "Sign In" button and authenticate with your Microsoft credentials
2. **Grant Permissions**: Consent to the required Microsoft Graph API permissions
3. **Enter Details**: Provide your desired app name and Onspring instance URL
4. **Configure**: Click "Configure App" and watch as each step is completed automatically
5. **Share Metadata**: Provide the generated metadata link and certificate to Onspring support

## Technical Implementation

### Architecture

This is a single-page application (SPA) built with vanilla JavaScript and modern web standards:

- **Frontend**: Pure HTML5, CSS3, and ES6+ JavaScript
- **Authentication**: Microsoft Authentication Library (MSAL) for browser
- **API Integration**: Microsoft Graph JavaScript SDK
- **State Management**: Custom reactive state system using JavaScript Proxies
- **Styling**: CSS custom properties with automatic dark/light theme switching

### Key Technologies

- **[MSAL Browser](https://github.com/AzureAD/microsoft-authentication-library-for-js)**: Handles OAuth 2.0/OpenID Connect authentication flows
- **[Microsoft Graph SDK](https://github.com/microsoftgraph/msgraph-sdk-javascript)**: Provides simplified access to Microsoft Graph APIs
- **CSS Grid & Flexbox**: Modern layout techniques for responsive design
- **CSS Custom Properties**: Theme system supporting light/dark modes
- **Web Components Principles**: Modular, reusable component patterns

### Microsoft Graph API Endpoints Used

- `POST /applicationTemplates/{id}/instantiate` - Creates the enterprise application
- `PATCH /servicePrincipals/{id}` - Configures SAML SSO mode
- `PATCH /applications/{id}` - Sets identifier URIs and redirect URLs
- `POST /servicePrincipals/{id}/addTokenSigningCertificate` - Generates signing certificate

### Required Permissions

The application requests the following Microsoft Graph permissions:

- `Application.ReadWrite.All` - Create and modify applications

## Security Considerations

- **Client-Side Only**: No server-side components reduce attack surface
- **Microsoft SDKs**: Uses official Microsoft libraries with built-in security best practices
- **Minimal Permissions**: Requests only the permissions necessary for functionality
- **No Data Storage**: No user data is stored locally or transmitted to third parties
- **HTTPS Required**: Microsoft authentication requires secure connections

## Browser Compatibility

- **Modern Browsers**: Chrome 88+, Firefox 85+, Safari 14+, Edge 88+
- **ES6+ Support**: Requires support for Promises, async/await, and Proxy objects
- **Pop-up Support**: Must allow pop-ups for authentication flow

## Support

For issues related to:

- **This Tool**: Open an issue in this repository
- **Onspring SSO Setup**: Contact Onspring support with the generated metadata
- **Microsoft Entra ID**: Consult Microsoft documentation or Azure support

## License

This project is licensed under the MIT License - see the LICENSE file for details.
