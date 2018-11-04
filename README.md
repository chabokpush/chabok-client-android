<p align="center"> 
  <img src="https://raw.githubusercontent.com/chabokpush/chabok-assets/master/sdk-logo/Java.png">
</p>

# Chabok Push for Java

Blow some breath to your app with Chabok realtime messaging and receive push notifications cross any platform with zero code.
Know your users's better, push them content based on their location or track their presence/location withoud headache.


## Usage

Create chabok account and use chabok credential keys in setting page of sandbox or production panel to init method.
### Initialize
```java
import com.chabokpush.*;

ChabokClient chabok = new ChabokClient(  
        APP_ID,  //Sandbox or Production environment APP_ID
        API_KEY, //Sandbox or Production environment API_KEY
        USERNAME,//Sandbox or Production environment USERNAME
        PASSWORD //Sandbox or Production environment PASSWORD
);
```
#### Environment
To change chabok enviroment (Sandbox or Production) use `setDevelopment` method.
```java
chabok.setDevelopment(true);
```
#### Callback

```java
chabok.setCallback(new ChabokCallback(){  
	@Override  
	public void onConnectError(Throwable cause) {  
		System.err.println("ConnectError " + cause);  
	}  
  
	@Override  
	public void onConnect() {  
		System.out.println("Connected to chabok");  
	}  
  
	@Override  
	public void onDisconnect(Throwable cause) {  
		System.out.println("Disconnected " + cause);  
	}  
  
	@Override  
	public void onMessage(PushMessage message) {  
		System.out.println("Got message: " + message.toJson());  
	}
	
	@Override  
	public void onEvent(EventMessage eventMessage) {  
		System.out.println("Got event: " + eventMessage);  
	}  
});
```

### Connect
For connecting to the chabok use `connect` method
```java
chabok.connect("NODE_ID");
```

### Publish

#### Publish message
```java
PushMessage message = new PushMessage();  
message.setUser("*");  //Require, For public channel use *
message.setChannel("CHANNEL_NAME");  //Optional, Channel name.
message.setBody("Hello world..."); //Require.
  
chabok.publish(message, new Callback() {  
    @Override  
  public void onSuccess(Object value) {  
        System.out.println("Published successfully");  
  }  
  
    @Override  
  public void onFailure(Throwable value) {  
		System.err.println("Fail to publish message");  
  }  
});
```

#### Publish event
```java
JSONObject data = new JSONObject();  

//Custom data
data.put("tripId", 123456);  
data.put("lat",54.2222);  
data.put("lng", 32.222);  
  
chabok.publishEvent("shareTrip", data, new Callback() {  
    @Override  
	public void onSuccess(Object value) {  
        System.out.println("Published event successfully");  
	}  
  
    @Override  
	public void onFailure(Throwable value) {  
        System.err.println("Fail to publish event");  
	}  
});
```

### Channel

#### Subscribe
```java
chabok.subscribe("private/default", new Callback() {  
    @Override  
	public void onSuccess(Object value) {  
		System.out.println("Subscribe on default channel");  
	}  
  
    @Override  
	public void onFailure(Throwable value) {  
        System.err.println("Couldn't subscribe on channel");  
	}  
});
```

#### Unsubscribe

```java
chabok.unsubscribe("private/default", new Callback() {  
    @Override  
	public void onSuccess(Object value) {  
        System.out.println("Unsubscribe to default channel");  
	}  
  
    @Override  
	public void onFailure(Throwable value) {  
        System.err.println("Couldn't unsubscribe on channel");  
	}  
});
```

### Event

#### Subscribe on event
```java
chabok.subscribeEvent("shareTrip", new Callback() {  
    @Override  
	public void onSuccess(Object value) {  
        System.out.println("Subscribe on shareTrip event");  
	}  
  
    @Override  
	public void onFailure(Throwable value) {  
        System.err.println("Couldn't subscribe on shareTrip event");  
	}  
});
```

####  Unsubscribe to event

```java
chabok.unsubscribeEvent("shareTrip", new Callback() {  
    @Override  
	public void onSuccess(Object value) {  
        System.out.println("Unsubscribe to shareTrip event");  
	}  
  
    @Override  
	public void onFailure(Throwable value) {  
        System.err.println("Couldn't unsubscribe on event");  
	}  
});
```


## Support
Please visit [Issues](https://github.com/chabokpush/chabok-java/issues).
