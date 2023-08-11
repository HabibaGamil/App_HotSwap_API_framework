# App HotSwap API
This project uses Java Springboot to design an application framework for an app whose API's can be changed without any downtime. The two primary Java features I used to implement hotswapping in Java are Reflection and the JVM's Class Loader subsytem which dynamically loads classes.
## Test App
This test app is a demo for the HotSwap API
### API design
The API is designed based on the Command Pattern. The app is designed as a set of commands meaning each API endpiont is implemented as a single Command Class. The app uses Java reflection to save a list of the current available commands (user requests) and the classes responsible for fullfilling these commands. The app does this through a dedicated commands hashtable which saves the pairs of user action string and Class object that handles it. When the app recieved a request, it retrieves the Class currently responsible for this command from the hashtable and reflectively executes its execute function.
## Controller App
The controller app externally controls the test app through a message queue. Since apps are likely to have multiple instances running, the controller acts as a centralized control piont through which app deployed instances of an app could be controlled. The controller. Administrative functions of the controller include:
### Add Command
This controller request dictates an app to add a new API endpiont and sends the new command class bytecode with the request. The app recieves the the bytes and loads it using its customized class loader then saves the new request/Class pair in its commands hashtable,
### Update Command
This controller request dictates an app to update an API endpiont and sends the updated command class bytecode with the request. The app recieves the the bytes and loads it using its customized class loader then saves the updated request/Class pair in its commands hashtable.
### Delete command
This controller request dictates an app to remove an API endpiont. This causes the app to remove the API entry from the commands hashtable.

