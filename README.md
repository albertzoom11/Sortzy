## Inspiration

A huge issue that the up and coming generation is facing is climate change. According to the United States Environmental Protection Agency (EPA), "75% of the American waste stream is recyclable, but we only recycle about 30% of it". We felt that, a lot of times, people aren't purposefully trying to harm the environment when they don't recycle, but rather they either don't want to put in the effort to think about or they don't know whether it is recyclable. This is how we came up for the idea of Sortzy.

## What it does

Sortzy is a self-sorting trash can that uses computer vision to determine whether an inputted object is recyclable or not, sorts it, and then relays the information to be tracked remotely. To start, an object is placed on a platform which is attached through two arduino servo motors. These servo motors along with all other sensors and hardware run through a Raspberry Pi 3 Model B+. Once the object is placed, an ultrasonic sensor will detect that something is on the platform and will trigger a webcam to take a snapshot of the object. This image is run through the Clarifai API which categorizes the object by its materials. We then determine whether the item is recyclable through the result of the API. Based on whether the object is recyclable or not, the servo motors are programmed to then dump the object into the appropriate bin. Information on the object type (recyclable or not), the specific date and time the object was dumped, the percentage full of each bin, and the image are sent to our back-end server. This server stores the information locally in a firebase and communicates it to a Swift iOS app. This app will have options to display local leaderboards (among neighbors for how many objects recycled), percentage full of each bin (ultrasonic sensors), percentage recycled of all objects dumped, and history of all items dumped (with date and time). All of this allows for a convenient way to recycle that also allows you to regularly check your recycling statistics.

## How we built it

For the hardware, we used a Raspberry Pi 3 Model B+ to handle all sensors and computing. We used cardboard to construct the prototype box, with hot glue and electrical tape to attach all components. 

For the server, we used express.js and node.js to handle requests. When a request is received, the parameters are parsed and subsequent actions are taken and the results are returned. For many requests, asynchronous access to the cloud hosted Firebase are required to access user data and ensure the user gets accurate information. 

For the app, we used XCode IDE and programmed it in Swift. The app has 4 main functionalities - Trash Storage, User Statistics, Leaderboard, and History. Each feature utilizes asynchronous API calls to the public server we created to access the user data from the cloud hosted Firebase database. All results are displayed to the user and under the history section, users can view all previously analyzed photos

For the Raspberry Pi, we used Python and Raspbian to code the project. We controlled the servo motors, ultrasonic sensors, and the webcam through the Raspberry Pi which computes the process for the trash can.

## Challenges we ran into

Wiring was a major issue because of the fact that we had so man sensors that had to wrap around this trash can while not inhibiting the rotation of the sorter platform. Another issue was dealing with the ultrasonic sensors which acted quite inconsistently throughout testing. In terms of the software, a big issue was passing the image as a parameter through python to the firebase. We overcame these challenges by thoroughly troubleshooting and repeated testing.

## Accomplishments that we're proud of

We are proud of the way we managed to use the Raspberry Pi to analyze images and categorize them accurately. Both our prototype and the hardware are functional and consistent.

## What we learned

Throughout this project we learned skills involving the Raspberry Pi. Specifically, we learned how to send images between the Raspberry and the server which proved to be a huge difficulty for us. We also learned how to work around issues involving hardware that seems sporadic and random.

## What's next for Sortzy

In the future, we may look to add more statistics features in the app as well as provide more consistent readings for percent full through more consistent ultrasonics. Also, we will look to expand upon our leaderboard idea to add more of a competitive multiplayer interactive nature to the recycling app.
