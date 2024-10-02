## What is an API Sandbox?

An **API sandbox** is a simulated environment where developers can safely test and experiment with an Application Programming Interface (API) without affecting live production systems. It mimics the real-world functionality of the API, allowing developers to:

- **Test API calls**: You can make requests, experiment with different inputs, and observe responses without real-world consequences.
- **Validate integrations**: It helps in verifying how an application interacts with the API.
- **Learn and explore**: Developers can explore the API's functionality, understand its endpoints, and practice how to handle responses and errors.
  
Key features of an API sandbox typically include:
- **Safe environment**: The sandbox environment does not affect real data or services.
- **Mock data**: The responses from the sandbox are often pre-configured or based on test data, simulating realistic scenarios.
- **Rate limits**: API sandboxes usually have relaxed or separate rate limits compared to production environments.

It's a valuable tool during development and testing to ensure everything works correctly before going live with actual data.

## How to use the Sandbox?

Using an API sandbox involves a few common steps that apply to most APIs, although the specifics can vary depending on the API provider. Here's a general guide on how to use a sandbox:

### 1. **Sign Up or Get API Access**
   - **Register for an API key**: Log into your ATRIP portal and navigate to "Profile --> My Profile --> Company Information." Click on the "Generate" button and your sandbox credentials will be created. This key will be used to authenticate your requests in the sandbox environment.
   - **Locate sandbox-specific endpoints**: The sandbox-specific endpoints are available in the section "API Document --> Shopping and Ticketing --> Specific Request". Please check the information for each request to get it's endpoint. 

### 2. **Read the Documentation**
   - Every API will have documentation outlining the available endpoints, request method, parameters, and expected responses. Be sure to read the sandbox-specific instructions, as some behavior may differ from production.

### 3. **Make API Requests**
   - Use tools like **Postman** to send requests to the API.
     
   - **Postman** is a user-friendly tool to send API requests:
     1. Install and open Postman.
     2. Create a new request.
     3. Enter the sandbox API endpoint.
     4. Set the request method (PUT, POST, etc.).
     5. Add your API key in the headers or authentication section.
     6. Send the request and check the response.

### 4. **Use Mock or Test Data**
   - In a sandbox environment, real-world data is not available. Instead, the sandbox provides **mock data**. This data mimics real-world scenarios, allowing you to test the behavior of your application without affecting live systems.
   - You might receive hard-coded responses or be limited to specific test scenarios (like "successful request," "invalid data," etc.).
   - All prices are *mock* prices. Fare comparison should not be done using the sandbox environment. 

### 5. **Experiment and Handle Responses**
   - Test different requests and check how your app handles success and error responses.

### 6. **Debug and Improve**
   - Use the sandbox to debug your application’s API integration by reviewing request logs, responses, and error messages.
   - You can continue adjusting your requests and refining your code until it behaves as expected.

### 7. **Transition to Production**
   - Once you’re comfortable with the sandbox and your integration works as expected, you can complete the UAT certification scenarios and get access to the **production environment**.
   - Make sure to update:
     - The API endpoint (switch from `sandbox` to `production`).
     - Your API key (you’ll need a production key for real data). Atlas will activate this section in ATRIP after certification.

### Example with Postman
   - Open Postman, set up the request like this:
     - **Endpoint**: `https://search-sg.atriptech.com/search.do`
     - **Method**: `POST`
     - **Headers**: Add Authorization (AK/SK)
     - **Body**: Define any required body parameters in JSON.
     - Click **Send** and check the response.

### Tips for Sandbox Usage:
- **Handle errors carefully**: The sandbox is a great place to practice how your application handles unexpected responses or errors.
- **Monitor for changes**: Sandbox environments might differ slightly from production, so verify your app behaves the same once you switch to production.
