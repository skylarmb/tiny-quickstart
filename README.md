# README

### Overview

This is a minimal app that implements Plaid using a very basic HTML/vanilla JS frontend with an Express/Node backend. After linking a sample bank account, the app retrieves balance information associated with the account and renders it on the home page. 

If you're looking for a more fully-featured quickstart, covering more API endpoints, available in more languages, and with explanations of the underlying flows, see the official [Plaid Quickstart](https://www.plaid.com/docs/quickstart). 

### Running the app

#### Clone the app

Clone the app to your machine and cd into the project directory:

```bash
git clone https://github.com/plaid/tiny-quickstart && cd tiny-quickstart
```

#### Set up your environment

This app uses the latest stable version of Node. At the time of writing, the latest stable version is v16.14.0. It's recommended you use this version of Node to run the app. For information on installing Node, see [How to install Node.js](https://nodejs.dev/learn/how-to-install-nodejs).

#### Install dependencies

Install the necessary dependencies:

```bash
npm install
```

#### Equip the app with credentials

Run the following command to copy the included **.env.example** to a file called **.env**.

```bash
cp .env.example .env
```

Fill out the contents of the **.env** file with the [client ID and Sandbox secret in your Plaid dashboard](https://dashboard.plaid.com/team/keys). Don't place quotes (`"`) around the credentials (i.e., `PLAID_CLIENT_ID=adn08a280hqdaj0ad`). Use the "Sandbox" secret when setting the `PLAID_SECRET` variable.

#### Start the server

Start the app by running the following command:

```bash
npm start
```

The app will run on port 8080. To use the app, navigate to `localhost:8080` in your browser. 

### Using the app

The app allows you to link a sample bank account at an OAuth bank or a non-OAuth bank. For more information on how to link accounts at both types of banks, see the sections below.

#### Non-OAuth banks

Most banks returned by Link in the app are non-OAuth banks. When connecting a non-OAuth bank account, use the following sample credentials:

- Username: `user_good`
- Password: `pass_good`

If you select a bank that requires multi-factor authentication, enter the following code to proceed: `1234`

#### OAuth banks

With OAuth banks, end users temporarily leave Link to authenticate and permission data using the bank's website (or mobile app) instead. Afterward, they're redirected back to Link to complete the Link flow and return control to the application where the account is being linked. In this app, "Platypus OAuth Bank" is an OAuth bank.

To experience an OAuth flow in this app:

1. Navigate to [**Team Settings > API**](https://dashboard.plaid.com/team/api) in your Plaid account.

2. In the **Allowed redirect URIs** section, click "Configure".

3. Add `http://localhost:8080/oauth` as a redirect URI and save your changes.

4. Navigate to the **.env** file in your project directory. Add the following line of code to the end of the file:

```bash
PLAID_SANDBOX_REDIRECT_URI=http://localhost:8080/oauth
```

5. Save your changes to the file and restart your local server (i.e., end the current server process and run `npm start` again).

6. Navigate to `localhost:8080` and proceed to link an account.

7. On the "Select your bank" screen, type "oauth" into the search bar. Select "Platypus OAuth Bank".

8. On the next screen, select the first instance of "Platypus OAuth Bank". Click "Continue" when prompted. You'll be redirected to the login page for "First Platypus Bank". Credentials are not necessary for this bank. Simply click "Sign in" to proceed.

9. Continue through the subsequent screens. Link will connect the account at the OAuth bank, prompt you to continue, and then redirect you back to the home page.

For more information on OAuth with Plaid, see the [OAuth Guide](https://plaid.com/docs/link/oauth/) in Plaid's documentation.

### Troubleshooting

#### MISSING_FIELDS error

If you encounter a **MISSING_FIELDS** error, it's possible you did not properly fill out the **.env** file. Be sure to add your client ID and Sandbox secret to the corresponding variables in the file.

#### OAuth flow fails to start

Ensure you've added the redirect URI present in the **.env** file as a [configured URI in your Plaid account](https://dashboard.plaid.com/team/api). The two values should be identical.
