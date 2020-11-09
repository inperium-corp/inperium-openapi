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

Soon we'll have detailed API documentation. At the moment, feel free to explore OpenAPI specifications on your own. 
