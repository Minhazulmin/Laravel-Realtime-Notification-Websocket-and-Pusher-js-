# Laravel real time notification with websocket & pusher js
**Websocket:** </br>
In many modern web applications, WebSockets are used to implement realtime, live-updating user interfaces. When some data is updated on the server, a message is typically sent over a WebSocket connection to be handled by the client. WebSockets provide a more efficient alternative to continually polling your application's server for data changes that should be reflected in your UI.

**Pusher js:** </br>
Pusher works as a real-time communication layer between the server and the client. It maintains persistent connections at the client using WebSockets, as and when new data is added to your server. If a server wants to push new data to clients, they can do it instantly using Pusher.

Watch video on YouTube: https://www.youtube.com/minit61 </br>
Watch video on Facebook: https://www.facebook.com/minit61</br>
**For Sponsor WhatsApp me +8801751337061**

## 🛠 Skills Required
PHP Laravel, Basic Knowledge of Pusher js and Websocket, HTML, CSS, Bootstrap, Laravel Command.



## Output
![App Screenshot]()


## Installation

**[Step - 1]** **Create Laravel new Project:**<br/>
(Open any terminal in your local machine and put this command)
 ```bash
    composer create-project --prefer-dist laravel/laravel lara-realtime-notification
```
**[Step - 2]** **Create pusher account and app for app key and id using url:**
```bash
    https://pusher.com/
```

**[Step - 3]** **Database Configuration:** </br> Open **.env** and replace the code.
```bash
    PUSHER_APP_ID="1815667"
    PUSHER_APP_KEY="7e19e7ef996cecbd845f"
    PUSHER_APP_SECRET="f80f3471a8635f40a09b"
    PUSHER_HOST=
    PUSHER_PORT=443
    PUSHER_SCHEME=https
    PUSHER_APP_CLUSTER=mt1
```
**[Step - 4]** **Database Migration**</br>
Connect Database with DB - DB name like: lara_realtime_notifications; Then 

**[Step - 5]** **Migrate using command**</br>
```bash
    php artisan migrate
```

**[Step - 6]** **Install Pusher:**</br> Using command
```bash
    composer require pusher/pusher-php-server
```

**[Step - 7]** **Install Laravel Echo and others** 
```bash
    npm install --save laravel-echo pusher-js
```

**[Step - 6]** **After installation, we need to uncomment the below line in config/app.php file:** 
```bash
    App\Providers\BroadcastServiceProvider::class,
```

**[Step - 7]** **Now open the .env file and update the broadcast driver to pusher** 
```bash
 BROADCAST_DRIVER=pusher
```
**[Step - 7]** **Open the resources/js/bootstrap.js and uncomment the following line:** 
```bash

    import Echo from 'laravel-echo';

        import Pusher from 'pusher-js';
        window.Pusher = Pusher;

        window.Echo = new Echo({
                broadcaster: 'pusher',
                key: import.meta.env.VITE_PUSHER_APP_KEY,
                cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER ?? 'mt1',
                wsHost: import.meta.env.VITE_PUSHER_HOST ? import.meta.env.     VITE_PUSHER_HOST : `ws-${import.meta.env.VITE_PUSHER_APP_CLUSTER}.pusher.com`,
                wsPort: import.meta.env.VITE_PUSHER_PORT ?? 80,
                wssPort: import.meta.env.VITE_PUSHER_PORT ?? 443,
                forceTLS: (import.meta.env.VITE_PUSHER_SCHEME ?? 'https') === 'https',
                enabledTransports: ['ws', 'wss'],
        });


```
**[Step - 8]** **Create Event and Dispatch**
</br>
Now we have to create our broadcasting event to fire our broadcasting channel.To do it run the following command:
```bash

 php artisan make:event MyEvent

```
**[Step - 9]** **opy and past on the MyEvent.php** 
```bash
     
    <?php

	namespace App\Events;

	use Illuminate\Broadcasting\Channel;
	use Illuminate\Broadcasting\InteractsWithSockets;
	use Illuminate\Broadcasting\PresenceChannel;
	use Illuminate\Broadcasting\PrivateChannel;
	use Illuminate\Contracts\Broadcasting\ShouldBroadcast;
	use Illuminate\Foundation\Events\Dispatchable;
	use Illuminate\Queue\SerializesModels;

	class MyEvent implements ShouldBroadcast
	{
    		use Dispatchable, InteractsWithSockets, SerializesModels;

    		public $message;
    		/**
     		* Create a new event instance.
     		*/
    		public function __construct($message)
    		{
        		$this->message = $message;

    		}

    		/**
     		* Get the channels the event should broadcast on.
     		*
     		* @return array<int, \Illuminate\Broadcasting\Channel>
     		*/
    		public function broadcastOn(): array
    		{
        		return ['my-channel'];
    		}
    		public function broadcastAs()
    		{
        		return 'my-event';
    		}
	}


```
**[Step - 10]** **Create a new route in route.php** 
```bash
 	 
    Route::get('/send-message', function () {
    		event(new \App\Events\MyEvent('how are you today'));
    		return 'Message send';
	});

```

**[Step - 10]** **Copy and past HTML code into blade file where you want to show message - like welcome.blade.php** 
```bash
 	 
    <!DOCTYPE html>
	<head>
  		<title>Pusher Test</title>
	</head>
	<body>
  		<div id="app">
    			<ul>
      				<li v-for="message in messages">
        				@{{message}}
      				</li>
    			</ul>
  		</div>

  	<script src="https://js.pusher.com/8.2.0/pusher.min.js"></script>
  	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  	<script>
    		// Enable pusher logging - don't include this in production
    		Pusher.logToConsole = true;

    		var pusher = new Pusher('7e19e7ef996cecbd845f', {
      			cluster: 'mt1'
    		});

    		var channel = pusher.subscribe('my-channel');
    		channel.bind('my-event', function(data) {
      			app.messages.push(JSON.stringify(data));
    		});

    		// Vue application
    		const app = new Vue({
      			el: '#app',
      		data: {
        		messages: [],
      			},
    		});
  	</script>
	</body>

```

**[Step - 10]** **Run project and open two window** 
```bash
 	php artisan serve
    	One window - (http://127.0.0.1:8000/)
	Two window - (http://127.0.0.1:8000/send-message)
	

```

Hit on the second window and see on the first window that showing message using
```bash
	http://127.0.0.1:8000/send-message
```
## Authors

- [@minhazulmin](https://www.github.com/minhazulmin)

