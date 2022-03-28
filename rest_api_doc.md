


REST API REFERENCE GUIDE










Version	Draft V1
Date	28-Mar-2022
Status	Final
Owner	ORGANIZATION
Approved	In-Review

 

Table of Contents

Change History	3
1. Document	4
1.1 Validity	4
2. Generic Status Code	4
2.3 Common Error Codes	5
2.4 Common Event Logs	7
2.5 Common Request Headers	9
2.6 Common Response Headers	9
3. What is REST API	10
4. Common Method	10












 


Change History

Version	Section	Date	Change from previous	 Author	     Reviewed By
R0	All	28-Mar-2022	Document Created	Bhupesh Rathore	YTD


 
1.   Document
1.1 Validity 
This document serves as an API reference guide for ORGANIZATION to assist the client application developers to understand the request response behavior of the RESTful APIs exposed by the ORGANIZATION. This document provides a complete description of all the API entities and functions details.
This ORGANIZATION API Protocol is built using Web APIs specification. The developer should have a basic understanding of HTTP/1.1 and experience writing HTTP-based client software before she/he can implement the API.
2.   Generic Status Code

Response Status Codes
    
Status Code	Description
HTTP/1.1 201 Created 	Session Created successfully.
401 Unauthorized
UNAUTHORIZED_ACCESS	Authorization has been denied for this request.
401 Unauthorized
INVALID_BASIC_CREDENTIALS	Invalid Basic – base64 string provided.
401 Unauthorized
UNAUTHORIZED_ACCESS	AccountType is missing or invalid.


Logging
Response Code	Event Level	Event ID	Task Category	Message Content	Use Case
201	Success Audit	10001	Session Basic	•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Client IP
•	Account Type	Success
401	Failure Audit	30002	Session Basic	•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Client IP
•	Account Type	No Authorization Header
401	Failure Audit	30004	Session Basic	•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Client IP
•	Account Type
•	Decision Tree to identify User Access Permission	User does not have access to the connector due to denied access based on the User and Groups Policy settings.
401	Failure Audit	30005	Session Basic	•	Fully Qualified User Name
•	Client IP
•	Account Type	Account Type mismatch.
401	Failure Audit	30023	Session Basic	•	Fully Qualified User Name
•	Client IP
•	Account Type	Network Share Feature Flag value mismatch.
401	Failure Audit	30024	Session Basic	•	Fully Qualified User Name
•	Client IP
•	Account Type	SharePoint Share Feature flag value mismatch.

2.3 Common Error Codes
The following error codes are common to all the Fishbowl API’s.

Status Code	Error Code	Description
400 Bad Request	INVALID_CHARACTERS_FOUND	File/Folder name contains invalid characters.
400 Bad Request	NAME_EXCEEDED_MAXLENGTH	The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.
400 Bad Request	BAD_REQUEST	The request could not be parsed successfully because of a syntactically or semantically incorrect URI.
401 Unauthorized	UNAUTHORIZED_ACCESS	Invalid Credentials or Unauthorized Access.
401 Unauthorized	NO_AUTHORIZATION_HEADER	No Authorization Header was pass in the Request.
401 Unauthorized	SESSIONTOKEN_MISSING	In case Basic token provided to any API other than the Open Session API, a 401 Unauthorized status is returned with the message “
Authorization <token> header is required”.
401 Unauthorized	SESSION_EXPIRED	Session Token specified does not exist, has timed out or the specific session was not created by the requesting user.
403 Forbidden	STORAGEQUOTA_LIMIT_EXCEEDED	Unable to perform the operation, because the Folder has exceeded the storage quota limit.
403 Forbidden	NO_PERMISSION	User does not have enough permission to access the resources.
404 Record Not Found	RESOURCE_NOT_FOUND	The request contains a resource which doesn’t exist for the given Folder.

406 Not Acceptable	INVALID_REQUEST_FORMAT	The requested format specified in the accept header cannot be satisfied for the entity/entity container/entity set.
500 Internal Server Error	SERVER_ERROR	The system has returned an internal server error. 
501 Not Implemented	NOT_IMPLEMENTED	The requested behaviour has not been implemented.

NOTE: Error Response Body in JSON format
HTTP/1.1 <Status Code>
Cache-Control: private
Content-Type: application/json; charset=utf-8
{
   “errors”: [
      {
         “code”:”<error code>“,
         “message”:”<error message>“
      }
   ]
}

2.4 Common Event Logs

Logging
Response Code	Event Level	Event ID	Task Category	Message Content	Use Case
401	Failure Audit	30002	<HTTP Method and the name of the Last Entity in the request URI>	•	Client IP
•	Fully Qualified Request URI	No Authorization Header
400	Failure Audit	30010	<HTTP Method and the name of the Last Entity in the request URI>	•	Client IP
•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Request Payload (if applicable).
•	Net Exception Error Code
•	.Net Exception Error Message
•	.Net Exception Stack Trace	Invalid Characters found in Folder or File Path in Request URI
400	Failure Audit	30011	<HTTP Method and the name of the Last Entity in the request URI>	•	Client IP
•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Request Payload (if applicable)
•	.Net Exception Error Code
•	.Net Exception Error Message
•	.Net Exception Stack Trace	Name exceeds max length.
403	Failure Audit	30012	<HTTP Method and the name of the Last Entity in the request URI>	•	Client IP
•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Request Payload (if applicable)
•	.Net Exception Error Code
•	.Net Exception Error Message
•	.Net Exception Stack Trace	The user does not have permission to execute the request.
404	Failure Audit	30009	<HTTP Method and the name of the Last Entity in the request URI>	•	Client IP
•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Request Payload (if applicable)	The resource (Folder or File) requested in the Request URI does not exist
500	Error	40001	<HTTP Method and the name of the Last Entity in the request URI>	•	Client IP
•	Fully Qualified User Name
•	Fully Qualified Request URI
•	Request Payload (if applicable)
•	.Net Exception Error Code
•	.Net Exception Error Message
•	.Net Exception Stack Trace	Handled or Un-handled Exception Publishing


2.5 Common Request Headers

Header 	Sample Value
Content-Type	application/json
Host	Host:[portno]
E.g.:
access. ORGANIZATION API host URL:443
Content-Length	<integer value depends on the Request body length>
Authorization	Token b3a82f09-f8ac-4a17-a165-294171bc078a

Should be included for all the subsequent requests after opening new session.

2.6 Common Response Headers

Header 	Sample Value 
Date	Thu, 28 Mar 2022 12:11:53 GMT
Content-Length	1297
Content-Type	application/json; charset=utf-8

 
3.   What is REST API

REST APIs act as a bridge between the two services, it helps two different modules to understand and speaks to each other. It is a framework which makes the web application process easier. User can make calls from one machine to another with ease. It uses HTTP for making the calling process easier instead of considering complicated mechanisms. With the help of HTTP, REST can create, delete, read and even update their different operations.
Major advantages of REST API.
•	Reusability.
•	Independent to any language.
•	User friendly and easy to understand by developer.
•	Scalability.

4.   Common Method

The common HTTP methods of REST API are as follows:
GET: This method is used to fetch the data from database, as per the inputs provided.
POST: This method is used to post the data to the API server to create and update the resource.
PUT: This method is used update the existing recourse.
DELETE: This method is used delete the resource.
PATCH: This method is used partially update the resource.
PULL: This method is used 




