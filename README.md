## A sleep analysis system on NodeMCU as a Master's dissertation
I just will leave it here :smile: I want to show you how I tried to solve my problem, what I have used and what problems I faced with. And in the end I will sum up what decisions was bad or good during developing the device.
Also don't pay a lot of attention to the grammar mistakes, mainly I've used Google translator,

The goal of the project is to develop a sleep analysis system, which will be able to measure data of ECG during sleep, analyze heart rate and act in accordance with the specified program. It has to collect data, analyze, store and transfer it to a smartphone. It was looked at and carried out try to create a bio-alarm clock and an alarm clock that helps you to wake up in a dream.

## Structure


## Automated system for monitoring and analyzing sleep parameters "SMAS"
So what do I mean by the title of this topic and what I want to achieve.

**Object of research:** Human sleep.
**Research subject**: Sleep measurement methods and its analysis.
**List of questions to be developed:**
1. **Characteristics of sleep**, its importance and methods of its measurement.;
2. **Lucid dreams**. Parameters, how to enter and how to control it;
3. Determination of **system functionality** and parameters. Sensors and actuators necessary to create a system;
4. Creation of a **functional and electrical scheme**. Development of the PCB.;
5. Implementation of the **software code** for the microcontroller. Methods of **signal processing**;
6. Collection of sleep **data** and their **analysis**. 

# SLEEP AND DREAMS

Sleep is a special genetically determined state of the organism of warm-blooded animals (that is, mammals and birds), which is characterized by a regular sequential change of certain poly(somno)graphic **patterns in the form of cycles, phases and stages**.

**Somnology** is the science of sleep, one of the most dynamically developing areas of modern medicine. With the beginning of the 20th century, somnology took a stormy start in the 21st century, starting with ideas about the orexin-hypocretin hypothalamic system. Modern somnology is a science with its own special goals and objectives, research methods, fundamental and clinical achievements.

### What is polysomnography and hypnogram

The main method of studying human sleep is **polysomnography** (PSG). This is a method of recording vital signs during sleep. The name is formed from the words poly-plural, somnos - sleep, grapho - write. The PSG is usually performed during nighttime sleep. The purpose of conducting a polysomnographic study is the objectification of the body's activity during sleep. For this, a number of indicators are registered. **The most important of them are:**
- **Electroencephalogram** (EEG) - recording of electrical activity of the brain;
- **Electrooculogram** (EOG) - recording of eye movements;
- **Electromyogram** (EMG) - recording of muscle tension (usually the chin).

The combination of these three indicators allows you to determine in which stage of sleep a person is at any moment of time. Based on the results of the sleep recording, a time schedule of sleep is built - **a hypnogram**.

![Sleep hypnogram](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/Sleep_Hypnogram.png)

In order to obtain data not only about the structure of sleep, but also diseases related to sleep, several more indicators are registered with PSG:
- Flow of exhaled air from the mouth and nostrils;
- Respiratory movements of the chest and abdomen;
- Breathing noise (snoring);
- Blood oxygen saturation level;
- Body position in bed;
- The number of heart contractions.

### The structure of sleep

The structure of human sleep includes two phases: slow sleep (**Non-REM**) and rapid sleep (**REM** – Rapid Eye Movement).

![cycles](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/cycles_of_sleep.jpg)

**What Happens During Non-REM Sleep?**
There are three phases of non-REM sleep. Each stage can last from 5 to 15 minutes. You go through all three phases before reaching REM sleep ([source)](https://www.webmd.com/sleep-disorders/sleep-101).

**Stage 1:** Your eyes are closed, but it's easy to wake you up. This phase may last for 5 to 10 minutes.
**Stage 2:** You are in light sleep. Your heart rate slows and your body temperature drops. Your body is getting ready for deep sleep. This can last for 10-25 minutes.

**Stages 3:** This is the deep sleep stage. It's harder to rouse you during this stage, and if someone woke you up, you would feel disoriented for a few minutes.

During the deep stages of NREM sleep, the body repairs and regrows tissues, builds bone and muscle, and strengthens the immune system.

As you get older, you sleep more lightly and get less deep sleep. Aging is also linked to shorter time spans of sleep, although studies show you still need as much sleep as when you were younger.

**What Is REM Sleep?**
Usually, REM sleep happens 90 minutes after you fall asleep. The first period of REM typically lasts 10 minutes. Each of your later REM stages gets longer, and the final one may last up to an hour. Your heart rate and breathing quickens.

You can have intense dreams during REM sleep, since your brain is more active. REM is important because it stimulates the areas of the brain that help with learning and  is associated with increased production of proteins

Babies can spend up to 50% of their sleep in the REM stage, compared to only about 20% for adults.

**Comparison of fast and slow phases of sleep**
| Characteristics of sleep  |  Slow  |   Fast |
| ------------ | ------------ | ------------ |
| Vegetative system  | Fast, increased synthesis of hormones is produced by the pituitary gland of GM. Active growth of nails, eyelashes, hair, bones   | The heartbeat is more frequent, the breathing is deeper and more active, the movement of the pupils increases   |
| Dreams  | Dreams are rarely dreamed. But if they happen, then with calm content  | Vivid dreams, violent experiences, with color effects  |
| Breath   | It is rare, superficial, deep, may be without rhythm   | Uneven, happens with a delay. This is a reaction to a dream  |
| Awakening  | Feeling tired, depressed. The process of waking up is difficult  |  Feels lightness, freshness, cheerfulness, energy |
|  Brain temperature |  Decreases | It is increasing  |
| Eye movement  |  Absent or smooth movements | Continuous and chaotic  |

### Circadian rhythms

In ancient times, people lived according to the laws of nature - everything depended on the change of time of day. After all, there were always only two "lights": the sun during the day, the moon at night. This shaped human circadian rhythms.

Circadian rhythms are the **body's internal clock**, which determines the intensity of various biological processes (thermoregulation, digestion, hormone production, etc.).

Circadian periodicity of sleep and wakefulness **depends on light**. Visual receptors respond to the level of illumination and send a signal to the suprachiasmal nucleus of the brain. This initiates the production of two important hormones responsible for sleep and wakefulness: melatonin and cortisol.

**Melatonin** is a sleep hormone. Produced in the pineal gland when it gets dark. It lowers pressure and temperature, calms the body and gives it a signal that it's time to sleep. In the morning, melatonin synthesis stops. The more light, the more cortisol is released into the blood. This hormone wakes us up, gives us vigor and energy for the accomplishments of the new day.

This determines the 24-hour circadian rhythm of sleep and wakefulness: it gets dark - melatonin gives us the opportunity to rest, the sun rises - cortisol wakes us up.

## Lucid dreams (LD)

In many ways, the popularization of the topic is connected with the name of the thinker and writer Carlos Castaneda. In **"The Art of Dreaming"**, he describes practices dating back to Native American shamanism that can be performed in sleep. According to Castaneda's teaching, lucid dreaming is a way to grasp "absolute energetic reality."

That the topic of lucid dreaming can often be associated with psychics, reality trance, or Dianetics (the pseudoscientific and, in the opinion of many, destructive teachings of **Ron Hubbard**), gives it a mixed reputation. Today, however, this phenomenon is being studied in advanced brain and consciousness sciences—and many people who are fascinated by the question are pursuing this experience for personal purposes.

It is believed that the term **"lucid dream" (LD)** was coined in 1913 by the Dutch psychiatrist and writer** Frederik van Eden**. For a long time, he kept a dream diary, as a result of which he achieved the experience of self-awareness in a dream. He laid out his theory in the article "The Study of Dreams". Neurophysiologist **Nathaniel Kleitman**, who in the 1950s described polyphasic sleep, is already considered the founder of the real scientific study of sleep (which today helps to investigate lucid dreams). He also developed the method of polysomnography - a hardware study of the sleeping state. By analyzing indicators (breathing, snoring, body position, its movements, etc.), the method allows you to create a hypnogram - a visual representation of the structure of sleep

### Oneironautics

 Oneironautics is the study of dreams, in particular lucid dreams. The main directions of one-neuronautics are the search for **methods and techniques of controlling dreams**, realizing them.
**Oneuronauts are people** who, in their dreams, do not just rest from their daily routine, but travel through various unknown worlds of dreams, receiving a variety of unique experiences. There are many theories and ideas of oneneuronautics, but the main part of it is practical methods of awareness in sleep and control of dreams. Many domestic and Western scientists, and just amateurs, were engaged in these questions, any searches, discovery and dissemination of methods.

Many cases are known when significant discoveries took place in a dream. It is well known that it was in a dream that **Mendeleev** managed to arrange the Periodic Table of Chemical Elements, **Einstein** was enlightened by the idea of the relationship between
space and time, **Niels Bohr** saw the structure of the atom, and **Fleming** saw the formula of penicillin. According to scientists, such insights are possible because dreams create conditions for self-immersion, subconscious processing of information on which a creative person intensively pondered while awake.

### Techniques of lucid dreams

There are many techniques that recommend what to do to enter a lucid dream. First of all, the techniques of getting into the LD are divided into** direct** (controlled regulation of consciousness) and **indirect** (self-programming methods) techniques. **Let's consider a few of them:**
- **Pendulum technique**. This technique is well depicted in the 2010 film "Inception", where the reality check is a kind of pendulum, or as in the film, a jig that lets you know if you're asleep or not. In real life, it can be any small object that a person carries with him and makes a habit of checking it for reality very often. This technique requires the formation of a habit, which can take from 1 month and does not guarantee the result.
- **M.Raduga's technique**, which requires waking up after 6 hours of sleep, and after some time awake from 3 to 30 minutes, you need to go to sleep with the concentration of attention on waking up without moving the physical body. For better separation, there are techniques: swimming, rotation, observation of images, visualization of hands, phantom rocking. Up to 6 cycles of awakening can occur in one night. 
- **The method of concentrating attention on the physical body**. In this technique, during falling asleep, you need to relax as much as possible and observe
internal sensations of the body. Observation helps the best, over time a part of consciousness will disappear, but the person will get into the US.
- **Sleep test**. The technique is similar to that of the pendulum, but the difference is the absence of a pendulum. A normal sleep check where a person checks objects. For example, a wall cannot be pierced, or the sun does not change color.

**One of the main problems** on the way to falling into lucid dreams is the sleeper's inability to understand that he is sleeping. As you can see, all the considered methods are quite complicated and time-consuming, so the developed **SMAS** will help in this without awakening and exhausting the body.

**Also in the theoretical part of work I covered:** how does polysomnography work, duration of sleep, sleep disorders, consequences of lack of sleep, basic recommendations for improving sleep, ect... You can find it [here]() on ukrainian (original of my work).

# DEVELOPING  SMAS
SMAS - System of Monitoring and Analysis of Sleep

In order to implement the device, you first need to decide on the components of the SMAS. To do this, let's **list the full functionality** in order to take into account all possible variants of the blocks that can be used.

At the moment, the **idea of this device** is as follows (ideal):
- Compact;
- Safe;
- If possible, it is powered by a 3.7V 800mA battery;
- Records ECG and pulse data;
- The possibility of connecting a separate unit for reading pulse and breathing;
- Display of data on the display;
- Transfers data to a smartphone or computer via WI-FI;
- Saves data to an SD card;
- Myostimulation for falling asleep, deepening sleep, lucid dreams;
- Actuators for lucid dreams (sound, light, vibrations);
- Actuators for bio-alarm clock (sound, light, vibrations, natural lighting).

![functional scheme](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/func.png)
`It is divided into the blocks of: sensors, actuators, additional modules, microcontroller and power supply `

**The microcontroller** [NodeMCU](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/MC.png) v3 was chosen because of Wi-Fi.
**Sensor of ECG** [(pic) ](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/ecgsens.png) is build on AD8232 and can meassure ECG with help of 3 electrodes.
**Pulse sensor** [(pic) ](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/pulsesens.png)this is an alternative to previous sensor. This one based on photoplethysmography method.
**Temperature and humidity sensor**  is a cheap digital sensor DHT11.
**To register breathing** we can use microphone and with help of software detect it.
**To determine the position of the body** we can use accelerometer and gyroscope MPU-6050 GY-521.
**Base Actuators** - the goal is to wake up human at a certain time and help to enter lucid dreams. So we can use LED's and piezo speaker or with help of smartphone noticatications.
**Specific actuators** - I wanted to wake up to the light of the sun, so I designed shutter blinds opening system. That consist of H-bridge PCB, hole-effect sensor and gear motor.

![blinds system](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/window.png)

![H-bridgePCB](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/Hbridge.jpg)

I've also learned about electrical mio-stimulator. It works like massager by passing current impulse through your body. So I meant it to use it before sleep like a massager to help relax your body and improve sleep. So I had to make it.

![EMS](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/EMS.jpg)

To connect SMAS to shutter blinds I made **smart-home device**. It was built on NodeMCU as well, and it can control every light source in my room, open/ close blinds, has timers... It has a lot of other features. But it is already another long long story. Scheme is [here](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/scheme_smart_room.png). It has the next menu screens:

![smart-disp](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/smart-display.jpg)

# PHYSICAL IMPLEMENTATION OF THE SMAS 

To create an electrical circuit, we will first create a connection diagram of all components and their power supply. Red and black are the power buses, green is the data bus (I2C, SPI, analog and digital I/O). Blue lines are control lines.

![connections](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/connect.png)

As you can see, to connect the actuators through a direct connection, it is necessary to use the shift register 74HC595, which allows you to increase the number of outputs. 

Fortunately, this shift register works on the SPI interface, so we will connect it to the pins used for the SD card module and one I/O for CS. To increase the number of inputs, a 74HC165 input shift register could be used, which would also allow an unlimited number of digital sensors to be connected.
It is believed that the actuators will be connected using a power key, some of them through a driver. The SD card module, time and shift register will be powered from the power system, and the display and ECG sensor will be powered from the microcontroller.

![Electrical scheme](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/Elecscheme.png)

The scheme is created in the maximum configuration with the expectation of its improvement or modification. We understand that the manufactured device is a prototype and will undoubtedly require drastic changes in the future, but to check its performance and capabilities, this option allows you to reveal all its capabilities.

![PCB look](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/PCB.png)

I wanted to order PCB from JLCPCB, but with war that had started in my country it was impossible. So I did it by myself. Tried to make it with help of negative photoresist, but failed 1st attempt and didn't have enough film for the next. So I was left iron method.

**Steps of making PCB with iron method:**

•** Printing** – it is necessary to print the diluted scheme in certain parameters (reflection, size, color, quality) on a newspaper with glossy paper;
• **Preparation of textolite** - surface cleaning with sandpaper and degreasing with alcohol or acetone;
• **Toner transfer** – the printed image is applied to the copper side of the textolite and transferred with an iron, ironing the newspaper for 30 seconds;
• **Removing the newspaper** - the workpiece must be placed in water to soak the newspaper, to separate the paper from the textolite;
• **Correction** - areas where the toner is poorly applied or absent must be painted over with a marker, or as in my case, contour paint for stained glass windows, which will better protect the copper layer.
• **Etching of tracks** – a solution for etching copper is prepared with 100 ml of hydrogen peroxide, 5 g of salt and 30 g of citric acid;
• **Toner removal **– all available methods were used, namely sodium hydroxide, acetone, sandpaper to remove the toner that protected the copper tracks from etching.
• **Drilling holes**.

![Steps](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/steps.png)

The ready prototype is looking like this:

![Ready](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/ready.png)


# SOFTWARE

To create a SMAS system, you will need software code that will connect all the modules, manage them, calculate the received data and send them. This will be a very large code for me, so I will try to break each part into as many functions as possible. **Let's define the main components of part of the code:**
- Connecting the time module;
- Connecting the SD card module (writing and reading);
- Connection of the shift register;
- Internet connection;
- Connecting the temperature and humidity sensor;
- Connecting an OLED display (interface);
- Analysis of ECG data (filtering, heart rate determination);
- Operation of actuators;
- Control using a smartphone or computer;
- System energy saving.

The main difficulty is that all parts of the code must work stably and detect problems. That is, if the electrodes are not connected to the body, or the contact is bad, we should find out about it, and in turn, this data should not be processed and recorded on the SD card. All data must be correctly calculated, recorded, and read. And with the growth of the number of modules, the number of options that may not be taken into account increases, which will lead to an error in the operation of the device.

All the code will be implemented in the **ArduinoIDE** environment, using libraries and a large number of functions. For more detailed analysis of the data, you can use **Matlab**, but already when the data will be saved to the SD card, which will allow them to be read and analyzed more scrupulously. Debugging the code is done by outputting information to the serial port, which allows you to find out how data is calculated or where an error occurs.

## ECG reading and analysis

Reading is the easiest step, since at the output of the sensor we have an analog value, to get it, you need to use the analogRead(A0) function. We will receive a signal every 2 ms for more stable MK operation.
We will use the serial connection port and get the first received data in graphic form.

![input](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/input%20sig.png)

#### Filtration
As we can see, there are noises and defects in the received data. First of all, this signal can be filtered using certain filters. Several filters were used, namely: **Arithmetic Mean, Moving Average, Optimal Moving Average, Exponential Moving Average, Kalman Filter.** The filters were taken from the AlexGyver site.

![pqrst](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/pqrst.png)

`For a better understanding of the following figures, you will need an image of the PQRST complex`

In each of the subsequent figures, **the input data is marked in blue**, and **the filtered data in red.**

For each filter, it was necessary to select parameters that would best remove noise from our data. In the figures below you can see how each of the filters affected the signal.

Results of every filter are here:
1. [Arithmetic mean](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/mean.jpg)
2. [Optimal moving average](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/opt_mov.jpg)
3. [Exponential moving average](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/exp_mov_av.jpg)
4. [Moving average with an adaptive coefficient](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/mov_av.jpg)
5. [Integer filter](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/intereger.jpg)
6. [Median filter](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/median.jpg)
7. [A simple Kalman filter](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/kalman.jpg)
8. [Combination of two filters: "Kalman" and exponential moving average](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/result.jpg)

#### Finding the pulse rate

Another step was to determine the QRS complex for finding the pulse rate. But take into account various traffic noises and errors to get the right result. This problem was solved as follows: **an array window of 11 elements is highlighted, through each of which a value passes.** When the value of element 5 is more than 200 units compared to elements 0 and 10 and the RR-interval takes a certain time interval compared to the previous one, then it is identified as an R-component. The points of definition of this segment are marked in green, and the duration in yellow of each RR-interval in ms., and in purple - heart rate directly (with such a scale - it is not visible).

![pulse](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/rate.jpg)

Heart rate was measured by the running average of ten measured intervals. This method does not allow the data to "jump" if there is an error and is generally quite reliable, but at the same time it takes some time to get the initial array of data.

#### Removal of the harmonic component

It will be necessary to remove the breathing component, during the measurement you can occasionally notice the presence of a sinusoidal signal, this may be due to the change of the chest, which changes the conductivity between the electrodes, during breathing. To eliminate it, two successive integer filters with the following coefficients (A = 7, B = 1, k = 3) were used.

![sin](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/harmonic.jpg)

Since this filter has the lowest signal delay and is the fastest, it is the best for this purpose. Then subtract this component from the cleaned signal. Red is the selected sine wave, and green is the cleaned signal.

#### Calibration 

The next step will be taring. Taring – drawing a scale of correspondence between a certain indication of the device (for example, the position of the arrow) and the value of the measured quantity.

![taring](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/taring.jpg)

Since the ordinate is an unknown value, you can try to bring it closer to the real value, i.e. tare it. To do this, we will use the map() function, which will proportionally change the range of the current value to the new range. From now on, the measured value can be considered in μV, that is, the R wave reaches 1mV, which corresponds to the value of other electrocardiograms.

#### Compression

The last step will be to compress the signal, since this signal contains 200 counts per second, then storing it on an SD card will not be rational and bulky. So with a simple loop, I will only take each N-signal. As a result, it was possible to reduce the volume by almost 6 times, or rather to 34 counts per second.

![compress](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/filters/compress.jpg)

## Displaying data on the display

To use the SSD1306 OLED 128x64 display, you will need two libraries from Adafruit, they will allow you to display information on the display.

![display](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/display.jpg)

`It has the next screens`

For each of the functions listed above, a software function was implemented that allows you to comfortably configure the code. The size of the code for signal calculation and data output takes about 700 lines.

## DHT11, RTC module and speaker

To use the **DHT11** digital sensor, you need to connect the appropriate library and create a function that will poll the sensor every 5 seconds. The library also supports the calculation of the heat index, which is an indicator that reflects how the temperature feels in combination with humidity

To write data, to read them, it will take time to measure the data. There are several ways to get it. The first with the help of the **DS3231 real-time module**, which has an independent power source and in the event of a power failure, the MK will store data about the current time. The second method is obtaining time from an **NTP server** when connected to Wi-Fi. This method allows you to get the time with an accuracy of several milliseconds. But there is also a drawback, if the Internet disappears, it will not be possible to receive the time variable. 

For the work of **speaker**, it will need the tone() function, which will play the melody that will be recorded in the variables.

## Working with memory card and recording format

To work with the memory card, it will need 2 libraries, the interfaces of which are described in the header files SPI.h and SD.h. The memory card will be used to save the log (measurement and calculation data) for later playback on a smartphone and analysis in the Excel or Matlab environment.

All data will be formatted in such a way that writing to the memory card will occur every second. This means that up to 30,000 rows of data will be generated in 8 hours of device operation.

![SD](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/SD.png)

A new text file is created every night, regardless of the number of runs, there will only be 1 file in the following format: `Night_m(month in numeric format)_d(day).txt`. The identification of a new night occurs after 12 noon. So if you go to bed on February 25th at 12:30 and wake up on February 26th at 10:00 AM, or go to bed at 2:00 AM on February 26th and wake up on February 26th at 10:00 AM, there will only be one file called `Night_m2_d25`.
In the event of a module malfunction, the system will notify you. There is an indicator on the display that indicates the successful saving of data to the storage medium.

## Remote control

There are three ways to manage and monitor system parameters.

**The first** is to create a **mobile application** in the MIT App Inventor environment, which has a user-friendly graphical interface. The connection will be made using the home web server. The disadvantage of this method is the need to use a smartphone with the application installed.

**Another option** is to directly create a **web server** with a graphical interface for access from any device that has access to a Wi-Fi network. The disadvantage is the need to know HTML to create a web page with the necessary parameters.

Usually, the first and second methods can be combined. It should be borne in mind that connecting to SMAS is possible only if the device and the user are connected to the same Wi-Fi network.

![Web server](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/web.jpg)

**The last option** is to create a connection using an **MQTT server**, which will allow you to connect to the network from anywhere in the world. This method was tested by me when I studied under the Erasmus program in another country. During that period, I needed access to a computer and lighting control of the growbox (diploma), so developing an application in the above-mentioned environment, for the period of studying abroad, it was an irreplaceable option. But the disadvantage of this method is the need for a paid subscription to maintain your own MQTT server.

## Actuator control unit (Smart-home)

As I said before, I wanted to make smart-home module.

**It has the next parameters:**
- Connect to the Internet;
- Control devices powered by 220 and 12V networks;
- Control blinds
- Have a customization feature
- Independence of work from the measurement system
- Work in constant mode
- Have a minimum of control buttons
- Display options

This actuator control unit can be considered part of the so-called "smart room". The system can work both independently and with a measurement system.
With the help of the actuator system, you can implement the functions of falling into **lucid dreams and bio-alarm clock**.

In the simplest form, in order to fall into **lucid dreams**, you need to turn on the timer for 5 hours before falling asleep, and after the time expires, with a certain intensity, smoothly control the color of the LED strip controlled by an IR LED. This light effect will allow you to realize yourself in a dream, but if a person is in the phase of REM sleep.

In the best case, the sensor system recognizes the fast phase after 5 hours of sleep and sends a command to the actuator unit. Changing the heart rate and other parameters can give an assessment of the efficiency and, if necessary, the system will increase or decrease the intensity, color and lighting mode.

A similar principle must be used to implement the **bio-alarm system**. That is, you need to wake up the person in the nearest time set on the timer during the transition from the first to the second stage of slow sleep. And the awakening can be provided by opening the window blinds, which will allow sunlight to enter the room, by turning on the lighting or by sound indication. In a simple case, it is a timer that opens the blinds at the set time.

# Analysis of measured data

The created log created 26728 lines of data in 8 hours of work, and occupies 8.26 MB of memory. That is, a 2 GB memory card is enough for more than 200 nights, where each hour of recording takes about 1 MB of memory.

![Heart rate](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/rate.jpg)

In the figure, you can see the change in sleep phases, the REM phase – an increased heart rate (50-55 beats/min), and NON-REM – a low heart rate (40-45 beats/min). With proper filtering and analysis of pulse data, it is possible to realize the function of bio-alarm clock and lucid dream alarm clock.

![DHT11](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/dht11.jpg)

From the graph, you can see how the temperature and humidity changed during the night. The heat index indicates how that temperature felt.

![ECG](https://github.com/dDenVil/SMAS_master_work/blob/main/Readme_assets/ecg.jpg)

`Zoomed graph of the  ECG measurement`
