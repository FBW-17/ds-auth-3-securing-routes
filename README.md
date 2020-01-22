# Authentication - Exercise #3 - Securing routes

In the previous exercise we allowed users to login and receive an access token (JWT - JSON Web Token).

In this exercise we now want to setup secured routes which are only allowed to call by an identified user.

We do protection by only allowing requests which provide a valid JWT token in a special HTTP header: the "Authorization" header 


## Setup a protected route

* Create a GET route /users
    * Show here a list of all your signed up users

* Create a middleware for that route by using:
    `app.get('/users', (req, res, next) => {...})`

* Secure your /users route in that middleware
    * Read the JWT token from the header "Authorization"
        * use req.header() function to fetch it
    * Validate the token using jwt.verify() and save the returned data in variable
    * On error:
        * Send an error message that verification failed
    * On success:
        * Allow passing to the desired route /users by calling the next() function

* Test your token authorization
    * Perform a login via your login form
    * Copy the token to the clipboard and save it to a file
    * Open the browser console
        * Write a fetch statement to call your /users route
        * Append the "Authorization" header to your fetch
        * Use your saved jwt token as value for this header:
            * `headers: { "Authorization": yourJwtToken }`


### Bonus Task - Tokens after signup

Adapt your signup process. On succesful registration:

* Create a token here too on the CREATED user (use jwt.sign method again)
* Send the token back to the user instead of the user object


### Bonus task - More helpful authorization error messages

* Handle three error cases - Check if the user got rejected because of:
    * missing token
    * invalid token (wrong hash)
    * expired token
* Provide different error messages for both cases so the user knows better what went wrong and why
* Test expiry
    * Reduce your JWT expiry time to 2 minutes (use "2m" as expiry string)
    * Login to fetch a fresh token 
    * Save the token
    * Open the browser console and load your previous fetch statement
    * Replace the old token in the "Authentication" header by the new one
    * Test if login works
    * Wait until the 2 minutes have passed
    * Check the expiry


