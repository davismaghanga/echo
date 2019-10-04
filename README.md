# comments-engine
laravel app for real time commenting engine using pusher

//instructions on how to configure laravel websockets


/*----------Installation--------------*/
1.  a. Create pusher account
	b. Move to App Keys to see your credentials
2. We require pusher php library thus:
	a. composer require pusher/pusher-php-server // this library allows us to push the event in the web server 		to the pusher (socket) server
3. Install npm dependencies
	npm install --save pusher-js //this is the javascript version of the pusher library

4. Install laravel echo // a client side js library
	npm install laravel-echo


/*-----------Configuring laravel server side------*/

5. go to config/app.php to the application service providers and uncomment the BroadcastServiceProvider

6. go to config/broadcasting.php here is where you configure all of the connections for ur socket servers. Under connections array:

		'pusher' => [
            'driver' => 'pusher',
            'key' => env('PUSHER_APP_KEY'),
            'secret' => env('PUSHER_APP_SECRET'),
            'app_id' => env('PUSHER_APP_ID'),
            'options' => [
                'cluster'=>env('PUSHER_APP_CLUSTER'),
                'encrypted'=>true
            ],
        ],
Add the cluster and encrypted key values as shown above.

7. move to env file and add the pusher_app_cluster along with the other pusher configs

8. grab the credentials ur pusher account and fill the env file accordingly in the pusher category

		PUSHER_APP_ID=****
		PUSHER_APP_KEY=****
		PUSHER_APP_SECRET=****
		PUSHER_APP_CLUSTER=****

9.Ensure to set the broadcast driver as pusher instead of log in the env file.


/*-----------Configuring laravel client side------*/

10. move to resources/assets/js/bootstrap.js and uncomment laravel echo to make it
available to every single page once we compile the app.js file

example:
import Echo from 'laravel-echo'

window.Pusher = require('pusher-js');

//fill accordingly and make sure not to display the secret key. Only use the public key as shown
below
window.Echo = new Echo({
    broadcaster: 'pusher',
    key: '',
    cluster:'',
    encrypted: 
});


11. run npm run dev to complie the app.js file and display it in the public directory.
this means that laravel echo is now available on every page of our application
