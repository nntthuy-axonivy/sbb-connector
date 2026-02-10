# SBB Connector

Axon Ivy's SBB Connector seamlessly integrates Swiss public transport services into your business workflows through the [Swiss Mobility API](https://developer.sbb.ch/apis/b2p/information). This powerful connector enables businesses to provide real-time transportation information, fare calculations, and booking capabilities directly within their applications, enhancing customer experience and streamlining travel-related business processes.

## Description

The SBB Connector brings the comprehensive Swiss public transportation network to your fingertips by integrating both the **Swiss Mobility API (B2P API)** and the **Swiss Mobility API - Journey** provided by SBB (Swiss Federal Railways). 

**What it does:**
- Retrieves real-time timetables and journey information for Swiss public transport
- Provides detailed fare calculations and pricing information
- Enables creation and management of bookings for trains, buses, and other public transport services
- Supports location search and place recommendations across Switzerland

**Problem it solves:**
Modern businesses need to integrate transportation services into their workflows - whether for employee travel management, customer booking systems, or logistics planning. Manually accessing transportation information is time-consuming and error-prone. The SBB Connector automates this process, providing programmatic access to Switzerland's comprehensive public transport network.

**Value it brings:**
- **Enhanced Customer Experience**: Offer seamless travel booking and information services directly within your applications
- **Operational Efficiency**: Automate travel planning and booking processes, reducing manual effort
- **Real-time Information**: Access up-to-date timetables, delays, and fare information
- **Business Integration**: Embed Swiss public transport services naturally into your existing business processes
- **Cost Savings**: Reduce development time by leveraging pre-built integration components
- **Reliability**: Built on SBB's official APIs, ensuring accurate and dependable transportation data

The connector is particularly valuable for travel agencies, corporate travel management systems, HR departments managing employee mobility, event organizers, and any business that needs to incorporate Swiss public transportation into their services.

> **Note:** API credentials are required to access the Swiss Mobility API features. While credentials are provided free of charge by SBB, the API is designed to facilitate commercial transportation services. For detailed information about API access, features, and commercial terms, visit the [Swiss Mobility API - Journey](https://developer-int.sbb.ch/apis/smapi-osdm-journey/information) information page.

## Features

The SBB Connector provides the following key capabilities:

- **🔍 Place Search**  
  Search for locations, stations, and points of interest across Switzerland using the `GetPlaces` process. Retrieve detailed place information including coordinates, addresses, and transport accessibility.

- **🚆 Trip Planning**  
  Find optimal travel routes with the `GetTripsCollection` process. Get comprehensive journey information including:
  - Multiple route alternatives
  - Departure and arrival times
  - Transfer details and platforms
  - Travel duration and distance
  - Real-time delay information

- **💰 Fare Information**  
  Access detailed pricing information for planned journeys, including different ticket types and discount options.

- **📅 Booking Management**  
  Create, modify, and manage bookings for Swiss public transport directly through the API (requires appropriate credentials and permissions).

- **🔐 Secure Authentication**  
  Built-in OAuth2 authentication ensures secure access to SBB's APIs using your client credentials.

- **🎯 Flexible Integration**  
  Easy-to-use callable processes that can be integrated into any Axon Ivy workflow with minimal configuration.

- **📊 Structured Data Models**  
  Pre-defined data classes following the OSDM (Open Sales and Distribution Model) standard for consistent data handling.

## Demo

The SBB Connector includes a comprehensive demo application that showcases the key features and helps you understand how to integrate the connector into your own projects.

### Search for Trips

The demo provides an intuitive interface to search for trips between any locations in Switzerland. Simply enter your origin and destination, select your preferred date and time, and retrieve available journey options.

![Search for Trips Form](images/search-for-trips.png)

### View Trip Results

The results display all available trip options with detailed information including departure times, arrival times, transfers, and journey duration. Users can easily compare different route alternatives to choose the best option for their needs.

![Show Trips](images/trips.png)

## Setup

Follow these steps to configure and use the SBB Connector in your Axon Ivy project:

### 1. Install the Connector

Install the SBB Connector from the Axon Ivy Market. The connector will be added as a dependency to your project.

### 2. Configure API Credentials

To use the SBB Connector, you need to configure your API credentials. Add the following variables to your Axon Ivy Project's `variables.yaml` file:

```
@variables.yaml@
```

**Variable descriptions:**
- `uri`: The base URI of the Swiss Mobility API (B2P API)
  - Integration: `https://b2p-int.api.sbb.ch`
  - Production: `https://b2p.api.sbb.ch`
- `contractId`: Your contract ID provided by SBB (e.g., `ACP1024`)
- `clientId`: Your OAuth2 client ID (UUID format)
- `clientSecret`: Your OAuth2 client secret (will be encrypted)
- `tokenEndpoint`: The OAuth2 token endpoint URL (e.g., `https://login.microsoftonline.com/2cda5d11-f0ac-46b3-967d-af1b2e1bd01a/oauth2/v2.0`)
- `scope`: The OAuth2 scope provided by SBB
- `journeyUri`: The base URI of the Journey API
  - Integration: `https://smapi-osdm-journey-int.api.sbb.ch`
  - Production: `https://smapi-osdm-journey.api.sbb.ch`

### 3. Obtain API Credentials

To get your API credentials:
1. Visit the [SBB Developer Portal](https://developer.sbb.ch/)
2. Register for API access
3. Request credentials for the Swiss Mobility API
4. Configure the credentials in your `variables.yaml` as shown above

### 4. Configure Requestor Header

Any request to the Swiss Mobility API requires a `Requestor` header to identify the business process making the request. You have two options:

**Option 1: Set as Custom Field**  
Set the `requestor` custom field at the beginning of your process:
```
customField.requestor = "YourCompanyName";
```

**Option 2: Pass as Argument**  
Provide the `Requestor` as an argument each time you call a subprocess. Refer to the demo project (`sbb-connector-demo`) for implementation examples.

### 5. Use the Connector

Once configured, you can use the following callable processes in your workflows:

- **GetPlaces**: Search for locations and places
- **GetTripsCollection**: Find trip options between locations
- **GetLocations**: *(Deprecated)* Legacy location search
- **GetTrips**: *(Deprecated)* Legacy trip search

For detailed usage examples, explore the demo processes included with the connector.

---

> [!IMPORTANT]
> **Migration Notice**  
> If you are upgrading from a previous version, please note:
> - `GetLocations` and `GetTrips` callable processes are **deprecated**
> - Use the new `GetPlaces` and `GetTripsCollection` processes instead
> - Data class structures have changed - you may need to adapt your existing code
> - Visit the [Swiss Mobility API](https://developer.sbb.ch/apis/b2p/information) information page for migration details