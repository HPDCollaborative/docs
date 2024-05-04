---
title: Response Codes
description: HTTP status and internal response codes for the HPDC API.
---

[[toc]]

# {{ $frontmatter.title }}

Below find our HTTP and Internal Response Codes and their corresponding text messages.

## HTTP Status Codes

| **Code** | **Text**                      |
| -------- | ----------------------------- |
| 100      | Continue                      |
| 101      | Switching Protocols           |
| 200      | OK                            |
| 201      | Created                       |
| 202      | Accepted                      |
| 203      | Non-Authoritative Information |
| 204      | No Content                    |
| 205      | Reset Content                 |
| 300      | Multiple Choices              |
| 301      | Moved Permanently             |
| 302      | Found                         |
| 303      | See Other                     |
| 305      | Use Proxy                     |
| 307      | Temporary Redirect            |
| 400      | Bad Request                   |
| 401      | Unauthorized                  |
| 402      | Payment Required              |
| 403      | Forbidden                     |
| 404      | Not Found                     |
| 405      | Method Not Allowed            |
| 406      | Not Acceptable                |
| 408      | Request Timeout               |
| 409      | Conflict                      |
| 410      | Gone                          |
| 411      | Length Required               |
| 413      | Payload Too Large             |
| 414      | URI Too Long                  |
| 415      | Unsupported Media Type        |
| 417      | Expectation Failed            |
| 422      | Unprocessable Entity          |
| 426      | Upgrade Required              |
| 500      | Internal Server Error         |
| 501      | Not Implemented               |
| 502      | Bad Gateway                   |
| 503      | Service Unavailable           |
| 504      | Gateway Timeout               |
| 505      | HTTP Version Not Supported    |

## Internal Response Codes

> [!info] Changes & Updates
> Internal Response Codes may be updated from time to time and the date of changes will be located within the [Change log.](./changelog)

| **Code** | **Text**                                             |
| -------- | ---------------------------------------------------- |
| 999      | The requested endpoint was not found.                |
| 1000     | Please correct any invalid fields.                   |
| 1001     | The requested product resource was not found.        |
| 1002     | Could not create product - no HPD tokens left        |
| 1100     | List of company products.                            |
| 1101     | Single product listing.                              |
| 1102     | Product created successfully.                        |
| 1105     | Filtered list of products.                           |
| 1107     | Filtered single product listing.                     |
| 2001     | The requested record resource was not found.         |
| 2100     | List of product records.                             |
| 2101     | Single record listing.                               |
| 2102     | Record created successfully.                         |
| 2105     | Filtered list of product records.                    |
| 2106     | Please submit filters with this endpoint.            |
| 2107     | Filtered single record listing.                      |
| 3001     | The requested material resource was not found.       |
| 3100     | List of record materials.                            |
| 3101     | Single material listing.                             |
| 3102     | Material created successfully.                       |
| 3105     | Filtered list of record materials.                   |
| 3106     | Material selectable options.                         |
| 3107     | Filtered single material listing.                    |
| 4100     | Substance was added successfully.                    |
| 4501     | The requested note resource was not found.           |
| 4501     | Single note listing.                                 |
| 4502     | Note created successfully.                           |
| 4503     | The note could not be created.                       |
| 4507     | Filtered single note listing.                        |
| 5001     | The requested accessory resource was not found.      |
| 5100     | List of record accessories.                          |
| 5101     | Single accessory listing.                            |
| 5102     | Accessory created successfully.                      |
| 5105     | Filtered list of record accessories.                 |
| 5107     | Filtered single accessory listing.                   |
| 6001     | The requested VOC resource was not found.            |
| 6101     | Record VOC listing.                                  |
| 6102     | VOC created successfully.                            |
| 6107     | Filtered single VOC listing.                         |
| 6108     | This record already has a VOC entry.                 |
| 7001     | The requested certification resource was not found.  |
| 7100     | List of record certifications.                       |
| 7101     | Single certification listing.                        |
| 7102     | Certification created successfully.                  |
| 7106     | Certification selectable options.                    |
| 8001     | The requested reference resource was not found.      |
| 8101     | Single reference listing.                            |
| 8102     | Reference created successfully.                      |
| 8103     | The reference could not be created.                  |
| 8107     | Filtered single reference listing.                   |
| 9000     | Viewing my user info.                                |
| 9001     | The current token is not authorized for this action. |
| 9002     | List of active Companies.                            |
| 9003     | Completeness Summary for Record.                     |
| 9100     | Special Conditions selectable options.               |
| 9101     | Special Condition material created successfully.     |
| 9102     | Special condition substance was added successfully.  |
| 9500     | The requested details resource was not found.        |
| 9501     | Details listing for record.                          |
| 9502     | Filtered detail listing.                             |
| 9503     | The detail could not be created.                     |
| 9504     | Detail created successfully.                         |
| 9505     | The requested detail resource was not found.         |
| 9506     | Please submit filters with this endpoint.            |
