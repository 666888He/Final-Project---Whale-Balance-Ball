# Final-Project---Whale-Balance-Ball
Final Project for Creative Making: Advanced Visualisation and Computational Environments .

Team Member: Rui Cai 22008912; Yujie Gao 22016089; Qihe Liu 21010891; Yuhang He 22010754;

Link to Demonstration Video: https://youtu.be/VrU-t2BdlO4

Due to the Blueprint plugin, the UE5 files have failed to pack several times, so only the Content and Plugins of the UE5 files are available here. If you need to experience the game, you can download these two files above, put them into your local project's folder, replace the Content file in it, and put the Plugins file in the project's root directory, then go into that project in UE5, open Explorer, go to Content/Finalwork/Map/Map_1, and double-click the map to enter the game.

<img width="827" alt="Screenshot 2023-06-11 at 15 13 22" src="https://github.com/666888He/Final-Project---Whale-Balance-Ball/assets/118990959/55ab3122-8a51-4904-a7ba-8a4bff0ed78e">


PROCESS DETAIL - HOW TO MAKE A GAME LIKE THIS :)

A more detailed process has been provided in the video above, which can be used in conjunction if required.

The UE5 UDP signal reception plugin used in the following article can be downloaded by clicking here: [https://getnamo/UDP-Unreal](https://github.com/getnamo/UDP-Unreal)

<img width="823" alt="Screenshot 2023-06-11 at 15 24 31" src="https://github.com/666888He/Final-Project---Whale-Balance-Ball/assets/118990959/93236057-4e8c-4941-92e1-3bfbf6a007d5">



We created a game called Whale Balancing Ball, using arduino in combination with Unreal Engine, using the capacitive touch pins that come with the ESP32 and using the UDP protocol to communicate with UE5 to achieve a game of balancing ball by touching the fruit to control the whale in the game.

In the live demo above, you can see that by tapping the fruit we can control the movement of the whale in the game.As the ESP32 comes with its own capacitive touch pins, you can freely change the fruit used for the control, which can be an apple, an orange, a mango or even a small tomato.

![Uploading Screenshot 2023-06-11 at 15.25.55.png…]()


First you need to buy the ESP32 board, you can see that the version I use is ESP32-WROOM-32, this is because the ESP32 comes with capacitive touch pins, and the ESP32's WIFI function can achieve UDP communication with the UE5, so you can receive the board's signal through the computer port inside the UE5. Of course if you are a UE4, you can connect the UE directly to the Arduino via a plug-in, such as the UE4Duino.



Once you have connected your ESP32 to your computer, you need to open arduino, find the development board manager and search for esp32, then click install. If you can't find esp32 here, you need to enter this URL:https://dl.espressif.com/dl/package_esp32_index.json in the development board manager URL in the preferences, then repeat the installation steps above.



Once you have installed it, you can find the ESP32 arduino in the development board and find DEVKIT V1 in it, follow my settings below to set it up.



Next you need to test the WIFI functionality of your ESP32, find wifi in the example, go in and select WiFi client. These two lines need to be entered with your wifi name and password, enter them and upload the code to your board. After a successful upload turn on the serial monitor and press the reset button on the board, when the connection is successful the serial monitor will display the network information.



Important: Do not use wifi that requires a secondary login, such as the public wifi in your flat, as this will prevent your board from connecting to the network and therefore not being able to use it, as there is no way for the board to login to these WiFis.

Once everything is in place we need to modify the code to enable it to send UDP signals to the computer via WIFI and we need to identify the ports on which the computer will accept these signals, which need to be the same as the ports used in UE5 later. Here I'm using apples and oranges as controls, so I've entered apples and oranges as values here, and this you can change at will. The IP address of the computer can be viewed in the command prompt via the wifi-config command. Here I have set pins 4 and 12 to receive apples and oranges respectively



The most crucial step now is to download and install the UDP protocol plugin for UE5, which can be found on Github by searching for UDP-Unreal, it's really great! getnamo/UDP-Unreal

Next go into UE5 to create your game world, without going into detail on this part, you need to build your scene your character, your blueprint. It is important to note that I recommend converting the two characters you will be using to control, into static meshes to avoid unnecessary hassle. Once everything is ready, we need to make our main characters able to be controlled by the signal. What we need to know here is that we cannot add a component to the level blueprint that reads UDP signals, so we need to create a new blueprint control-BP.





Next we edit the blueprint, ctrl+E to go to the blueprint page, find the UDP component in the top left corner under add, put it in the blueprint and add two static mesh body components, here I named them apples and oranges to keep it all the way through. Note that we need to keep the same UDP signal port in the arduino and UE5, here I have set port 3002. Next are some general settings to allow the UE5 to feedback and print different objects when it receives a signal and depending on the pin, in this case I set the bound object to move 20 units along the Z axis once the signal is received.



Next you just need to place your blueprint inside the map and have it bound to the two characters you need to control in the detail in the bottom right corner.

That's basically all there is to it, next you just need to do an overall test to see if the ESP32 can control your characters, or of course you can control them to move more freely, or add more pins to output signals.

