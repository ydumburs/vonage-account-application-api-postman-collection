Overview
======================
This Postman collection is designed for the Vonage Application API, allowing you to manage Vonage Applications and Users. It provides a set of pre-configured authentications and requests to interact with Application API endpoints efficiently.  

REST API reference: https://developer.vonage.com/en/api/application.v2#User

How It Works
======================
## **Using Postman Variables**  
In this collection, items enclosed in `{{ }}` are variables (e.g., `{{application_id}}`). You can either replace these placeholders with your own values or set them as variables in Postman. For more information about Postman Collection variable, visit: https://learning.postman.com/docs/sending-requests/variables/variables/#defining-collection-variables. 

## **Authentication for Managing Vonage Applications**  
To manage Vonage Applications (e.g., creating an application, retrieving application details, or updating applications), you need to use basic authentication. This requires a Vonage API key and secret, which must be Base64 encoded. For more information, see the https://developer.vonage.com/en/getting-started/concepts/authentication#basic-authentication.

In this Collection, requests are pre-configured with basic authentication using the Vonage API key and secret stored in the Collection variables. These credentials are automatically encoded in Base64 format.  
<img width="600" alt="Screenshot 2024-08-31 at 1 41 30 PM" src="https://github.com/user-attachments/assets/6f01dff4-74dc-4965-ba4b-a58ff54ad883">


## **Authentication for Managing Users**  
To manage Vonage Users (e.g., creating or updating a user), you need to use Bearer Authentication with a JWT generated from your Application ID and Private Key. 

JWT Generation Options:  
1. You can create a JWT using the Vonage's onlie tool: https://developer.vonage.com/en/getting-started/concepts/authentication#using-the-vonage-api-online-tool-to-generate-a-jwt.
2. You can also create a JWT using the Vonage server SDK: https://developer.vonage.com/en/getting-started/concepts/authentication#using-the-server-sdks. For convenience, configure the endpoint using the SDK and use the `Generate a JWT` request at the top of the Collection. This request includes a Postman post-request script that automatically stores the returned JWT in a Collection variable upon completion.
```
// Postman Post-request script
const response = pm.response.json(); 
if (response.token) {
    pm.collectionVariables.set("jwt", response.token); 
    console.log("JWT has been set to collection variable:", response.token);
} else {
    console.error("JWT token not found in the response");
}
```
3. In addition to those options, there are several other ways to generate JWTs. For more information, please refer to the  https://developer.vonage.com/en/getting-started/concepts/authentication#generating-jwts

## **User Management Request URLs**  
The request URL for user management varies by region. We have separate endpoints for the US, EU, and AP regions. For detailed information, please visit https://developer.vonage.com/en/voice/voice-api/concepts/regions.
<img width="269" alt="Screenshot 2024-08-31 at 1 39 47 PM" src="https://github.com/user-attachments/assets/26cd8db2-a56d-416a-8da3-461f5d17fa44">

How to Use
======================
1. **Create a Vonage Account**  
   If you don’t have a Vonage account, sign up: https://www.vonage.co.uk/communications-apis/ to start building with free credit.
2. **Install Postman**  
   Download the Postman desktop app: https://www.postman.com/downloads/. You can also use the Web version: https://blog.postman.com/announcing-postman-for-the-web-now-in-open-beta/.
3. **Import the Collection**  
   Import the `Vonage Application API.postman_collection.json` into Postman. For guidance, check out: https://learning.postman.com/docs/getting-started/importing-and-exporting-data/#importing-postman-data.
4. **Configure credentials**  
   Add your Vonage API key and secret to the Collection variables and save your changes. Refer to: https://community.postman.com/t/how-do-i-set-a-collection-variable/5466 for instructions.
5. **Add JWT for User Management**  
   For user management, you need a JWT. For a JWT generation, please see https://github.com/ydumburs/vonage-application-api-postman-collection/blob/main/README.md#authentication-for-managing-users. Save your JWT in the `jwt` Collection variable or replace `{{jwt}}` in the Auth tab with your token.
6. **Send Requests**  
   Modify the request body as needed and click the `Send` button.

