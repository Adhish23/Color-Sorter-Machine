# Color-Sorter-Machine

**Abstract**:
For sorting object in industry optical sorting is very much convenient. Color and size are the most important features for accurate classification and sorting of product which can be done by using some optical sensors or analyzing their pictures. The color sorting machine is mainly a device that can sense the different color of the object and assert them into different containers. When the object moves from one place to another with the rotation of motor, sensors as the input devices will send signal to microcontroller where microcontroller as the controller will give command to the actuator to do action. 

This project describes a working prototype designed for automatic sorting of objects based on the color. OPT101 sensor was used to detect the color of the product and the STM microcontroller was used to control the overall process. The identification of the color is based on the ADC value of the output of OPT101 sensor. Two Servo motors were used, each controlled by the microcontroller. The first motor is used for carrying the product to be analyzed by the color sensor, and the second motor is used for sorting the product according to the reading taken by the color sensor, into the separate containers.

![IMG-20190506-WA0014](https://user-images.githubusercontent.com/37892206/172301080-9342593d-5b27-4b58-b4d2-1b896c979fe4.jpg)


**Motivation**: 
The main advantages of this system is it requires less time to sort the product, as the whole system is performed by machine there is less possibility of mistake, less man power required. If the industry can produce the product within the required range then the demand of the product will be increased. So, the company will be benefited.Since in order to reduce the human labor and avoid the negligence caused by them in case of hurry this automatic color sorter machine can easily can provide ease to the problem and sort the product accordingly thus giving a good efficiency and accurate results.

**Results and Discussions**:

The final result was quite satisfactory. The color detecting sensors worked well and it was able to detect different color object quite nicely and change the direction of servo on right and left side to sort the object in proper place. 

**Dimensional analysis*:-
The prototype is designed for sorting objects of any shape but having fixed sizes of 1cm diameter. We can of course change this parameter by adjusting the frame of the color sensor. But one may note that it usually results in a change in the light ambience forcing us to do further frequency analysis of the sensor output for test colors. The prototype will get more complicated as we increase the number of colors that have to be detected.
The placement of the object on the first servo guide is very crucial. It must be so placed that the center of the object and that of the sensor should be aligned with the same vertical plane, so that perfect detection takes place.

_**Time Cost**_:-
The object once placed on the first servo guide it takes less than half a second to reach the sensor. It takes another 2ms for the sensor to detect the color. An additional 0.6secs is required if to position the product into the correct compartment in the sorting container, which implies that an additional 0.6secs will be consumed to reposition the container back the normal position on the second. Of course, these time values are dependent on the speed of the servo motors used.

**Conclusion**:

The color detecting sensors worked well and it was able to detect different color object quite nicely and change the direction of servo on right and left side to sort the object in proper place. The guide through second motor moved from starting point to the end point without conflicting with the walls. The system performed well as programmed and detected the object according to their color and sorted accordingly

**Future Work**:

The model can be improved by making some changes in the program and components. Some suggestions are given below.

• We can add a load cell for measurement and control of weight of the product.
• We can also add a counter for counting the number of products.
• Speed of the system can be increased accounting to the speed of production.
• The system can be used as a quality controller by adding more sensors.
• The sensor can be changed according to the type of product.
• The servo motor can be replaced with stepper motor.
• The STM can be replaced with PLC.

Thank you!




