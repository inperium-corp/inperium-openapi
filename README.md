# Inperium OpenAPI Specification

This repository contains OpenAPI 3.0 specifications for Inperium API.

The API is used internally for service-to-service communication. Clients can also leverage API to create custom integrations with Inperium apps and services.


Path: `api.inperium.com`

Current version: `v1`

Formats accepted & returned: json


## Project Structure

Since Inperium runs several microservices under the hood, each service has a dedicated API specification. Specifications are named after a corresponding service and organized into folders.

| Folder            |           Specification   |                                    Description |
|-------------------|---------------------------|------------------------------------------------|
| `/hub`            | `hub-api.yaml`            | Contains endpoints related to the Inperium Account functionality including auth services, user management, application settings, and licensing. |
| `/lead-router`    | `lead-router-api.yaml`    | Contains endpoints related to internal lead management microservice. |
| `/message-center` | `message-center-api.yaml` | Contains endpoints related to the Message Center microservice that is responsible for the functionality such as sending and receiving emails. |
| `/obs`            | `obs-api.yaml`            | Contains endpoints that provide access to the OBS microservice that helps manage documents stored in buckets. |
| `/sell`           | `sell-api.yaml`           | Contains endpoints related to the Inperium Sell app functionality. Provides access to companies, contacts, deals, products, etc. |
| `/talk`           | `talk-api.yaml`           | Contains endpoints related to the Inperium Talk app functionality. Provides access to calls, audio library, auto-receptionist settings, etc. |


## Authorization and Authentication

Two auth method are available:
* With Bearer access token (`Authorization: Bearer eyJraWQiOiIxIiwidHlwIjoiSldUIiwiYWxn...`)
* With API key (`X-API-KEY: 5d5b4ed1-8397-47ff-ad8d...`)

## Documentation

The 'In-development' API documentation is hosted at [developers.inperium.dev](https://developers.inperium.dev)

## API Guidelines — Help Make API Docs Awesome

While some requirements may seem excess, please note that API documentation is generated automatically out of the OpenAPI specifications and you are highly encouraged to comply with these rules in order to make the docs better.

When adding a new endpoint, follow these guidelines:

* Please follow the alphabetical order when adding new entities (tags, endpoints, calls, components, etc.).
* If you introduce a new tag, add it to the dedicated section on top and provide a description.

```
tags:
  - name: API Keys
    description: |
      API keys are used instead of bearer tokens to authenticate applications connecting to Inperium via API.
```

* An endpoint should have a short summary (main title), a description, and a tag.

    * The `summary` should be a short imperative sentence without an ending dot (e.g., Create a company).
    * The `description` should start with "Use this endpoint to ...". Provide any details that seem necessary.
    * Add a `tag`.

```
/features/{anchor}:
    get:
      summary: Retrieve a feature
      description: Use this endpoint to retrieve details for a specific feature.
      operationId: getFeature
      tags:
        - Features
```
* Each parameter (endpoint query parameters, request parameters or those in object models) should have a description.
* Each object model should have a description.

```
CompanyRelationshipRequest:
    type: object
    description: The incoming company relationship object enables you to link companies and define relations between companies.
    properties:
        id:
          $ref: "#/components/schemas/Id"
        companyId:
          type: string
          description: The ID of the origin company.
          format: uuid
        parentCompanyId:
          type: string
          description: The ID of the parent company.
          format: uuid
```
* If an endpoint or its method or probably the entire specification shouldn't be exposed to clients, then apply the property `x-access: private`. Add `THIS IS INTERNAL ENDPOINT.` to the description. To display endpoints and methods correctly in our API docs, please add the private flag after each HTTP method even if the entire endpoint should be concealed from view.

```
/internal/limitUsages:
    x-access: private
    post:
      x-access: private
      tags:
        - Limits
      summary: Update a limit usage
      description: THIS IS INTERNAL ENDPOINT. Inperium services send requests to this endpoint to update the occupied limits in Inperium Hub.
```

* Feel free to add meaningful examples to the object models (tentative). They will be displayed in API documentation. DO NOT add empty examples, i.e. `example: {}`.

```
    CompanyRequest:
      description: The incoming object that describes company properties such as a company name or employee count. To retrieve property definitions, send a GET request to '/properties'.
      type: object
      additionalProperties: true
      example:
        companyName: Arts Inc.
        industry: RETAIL
        employeeCount: 200
        country: US
        type: LEAD
        city: Newtown
        state: CA
        description: Musical instruments shop
```
* List response codes.

> When in doubt about texts, contact Olly Kirillova.
