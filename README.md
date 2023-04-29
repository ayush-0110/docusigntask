# docusign

This is a project where I've used Docusign API to fetch template and send and send an envelope to any person on his/her email id.
DocuSign is a cloud-based electronic signature technology that enables individuals and businesses to sign, send and manage electronic documents anytime, anywhere, and from any device. With DocuSign, you can securely sign, send, and manage contracts, agreements, and other legally binding documents digitally, reducing paper waste and streamlining business processes. DocuSign offers a wide range of solutions for individuals, small businesses, and large enterprises, including real estate, healthcare, finance, and more. It is widely used in industries that require contracts, approvals, and other types of agreements to be signed and processed quickly and securely.
I've integrated Oauth2.0 for authorisation and authentication in this project. Auth 2.0 is the industry-standard protocol for authorization. OAuth 2.0 focuses on client developer simplicity while providing specific authorization flows for web applications, desktop applications, mobile phones etc.
In simple words, Oauth relieves the pain of the developer and handles authorisation on the server side.

# Key technologies:
1. Nodejs.
2. Expressjs
3. Axios
4. abab(for using btoa() function to convert to base64)
5. Express-session
6. dotenv

# Details about the implementation:

Lets move step by step about how I created the project:

# Step 1:  Registering  application:
To register application with DocuSign and obtain the necessary credentials, follow these steps:
1. Go to the DocuSign Developer Center and sign up for an account.
2. After signing in, navigate to the "My Apps" section and click on "Create App".
3. Choose the type of application we want to create (e.g. Authorization Code Grant).
4. Provide the necessary details for your application, such as name and description.
5. After creating the app, you will be provided with a Client ID and Secret which we will use in application.


In the application, I have stored the client ID and secret key as environment variables using the dotenv package.

# Step 2: Authenticating users:

To authenticate users using OAuth, we have implemented the following flow in our application:
1. When the user clicks on the "Sign In with DocuSign" button, application redirects the user to the DocuSign authorization endpoint.
2. The authorization endpoint prompts the user to log in to their DocuSign account (if not already logged in) and presents the user with the option to authorize the application to access their account.
3. If the user authorizes application, the DocuSign authorization endpoint sends an authorization code to application's redirect URI.
4. The application then exchanges this authorization code for an access token and a refresh token by making a POST request to the DocuSign token endpoint.
5. The token endpoint returns the access token and refresh token in the response body.
6. The application then stores the access token and refresh token in the user's session.

I have implemented this OAuth flow in application using the getAccessToken() and getUserBaseURI() functions.

# Step 3: Handling tokens:
In application, I stored the access token and refresh token in the user's session. Then, app retrieves the access token from the session when making API requests on behalf of the user.

If the access token expires, app uses the refresh token to obtain a new access token. I have not implemented the refresh token functionality in our current code, but I can add it by making a POST request to the DocuSign token endpoint with the refresh token instead of the authorization code.
I  use the createAndSendEnvelope() function to make API requests on behalf of the user. This function includes the access token in the authorization header of the request.

# Challenges faced:

1. Because docusign provides a lot of features so extracting the details for my project's description was a bit tedious and challenging.
2. Intially I tried to use fetch API for fetching data from Docusign but it caused issues after deployment, so had to use Axios and re wrote and re deployed the code, resulting in extra time investment.
3. After implementing the features, on first few runs got some errors. Narrowing down lead me to the real issue of 'code challenge and code challenge method required'. Had to research about this and got the fix finally.


# References:
For implementing above things, I referred the official documentation from Docusign(attaching images of specific parts and code snippets that I referred to and used on my app):

![Screenshot from 2023-04-29 15-04-39](https://user-images.githubusercontent.com/85434037/235313352-2e7642fc-d856-42c7-b909-6610cfa49e0a.png)

![Screenshot from 2023-04-29 15-21-04](https://user-images.githubusercontent.com/85434037/235313367-ec07b7fc-197d-4d30-be21-8c92c2a9aabd.png)

![Screenshot from 2023-04-29 15-26-06](https://user-images.githubusercontent.com/85434037/235313410-67cfccb8-546e-4fdf-94af-0371a52a3ba8.png)

![Screenshot from 2023-04-29 16-00-11](https://user-images.githubusercontent.com/85434037/235313431-babfe5d1-98c2-4e64-ac0e-08b7acbbe257.png)

![Screenshot from 2023-04-29 16-02-46](https://user-images.githubusercontent.com/85434037/235313458-81fd052a-f13b-40bc-821d-7ef1313badc3.png)

![Screenshot from 2023-04-29 16-10-03](https://user-images.githubusercontent.com/85434037/235313470-10c90ba9-b972-4917-a964-84eaa857e270.png)

# Images from application:

Welcome screen :

![Screenshot from 2023-04-29 19-34-17](https://user-images.githubusercontent.com/85434037/235313509-0c15662d-da6c-4215-ac1b-a90d4c3eee8b.png)

Authentication:

![Screenshot from 2023-04-29 19-34-40](https://user-images.githubusercontent.com/85434037/235313535-13a463e1-1322-44d4-8df5-8e26307c4223.png)
![Screenshot from 2023-04-29 19-34-47](https://user-images.githubusercontent.com/85434037/235313545-759e5288-8df9-455b-8fde-873df5128588.png)

After login, sending envelope:

![Screenshot from 2023-04-29 19-34-59](https://user-images.githubusercontent.com/85434037/235313558-e1c39bc9-6df8-42b4-8c99-f18331b4a5da.png)
![Screenshot from 2023-04-29 19-35-10](https://user-images.githubusercontent.com/85434037/235313569-9cde5817-df1f-47c7-8557-abfcef1052bd.png)

After sending envelope:

![Screenshot from 2023-04-29 19-35-23](https://user-images.githubusercontent.com/85434037/235313613-696115cf-9560-42db-b267-d56a39ff1aa1.png)



