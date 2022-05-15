## Digital-simulation
College project
**Simulation of blood donation center (C++)**

If number of blood samples gets below **R** then center orders **N** of new samples. Time of delivery is a random number of exponential distribution with mean **Z**. Delivered blood samples have **T1** expiration date. After passing of expiration date the blood is sent for utilisation.

Time between arrival of patients for blood transfusion is a random number of exponential distribution with mean **P**. Number of blood samples given to each patient is a random number of geometric distribution with mean **1/W**.

If number of needed blood samples in the center is bigger than number of samples needed at the moment then emergency order for **Q** samples is placed. Delivery time of that order is random number of normal distribution with mean **E** and variance **E(W^2)**.

There are also local donors who donate one blood samples to center. Time between arrival of each donor is random number of exponential distribution with mean **L**. Expiration date of blood samples from donors is **T2** (T1<T2).

Patient cab be either of blood group A or B and they can use only blood of their group. Probability of patient/donor to have certain blood group is 60% for A and 40% for B. Orders are placed separatelly for each blood group.

The goal of the simulation was to find values of **R** and **N** for which the probability of emergency order is smaller than **A**.

Given values:
- Z = 1900;
- T1 = 300;
- T2 = 500;
- P = 150;
- 1/W = 0.23;
- Q = 12;
- E = 400;
- E(W^2) = 0.1;
- L = 850;
- A = 0.07;

# Classes
List of C++ classes and their description/atrributes

| Class name  | Description | Atrributes  |
| ------------- | ------------- | ------------- |
| bloodCentre  | Blood donation center. Contains most of simulation elements  | blood storage; queue of patients; transfusion point; examination flags; random number generators|
| bloodStorage  | Stores blood samples. Samples are ordered starting with those with shortest expiration date. Delivery flags inform us if order has been sent  | bumber of stored blood samples (type A and B); delivery flags |
| patient  | Patient  | number of needed blood samples; blood group  |
| donator  | Blood donor  | blood group |
| delivery  | Delivers blood order  | delivery type (normal or emergency); number of delivered blood samples |
| bloodSample  | Blood sample  | expiration date (integer)  |
| proces  | Represents events that can happen (new blood donor, delivery, blood utilisation etc.).  Classes patient, donator, delivery, research, bloodSample inherint from this one  | pointer event; pointer to agenda list; pointer to system clock  |
| event  | Connector between proces and Agenda list  | pointer to proces of origin;   |
| AgendaList  | Represents lists of events  | stored event; pointer to next event; pointer to previous event |

# Generators
There have been 6 generators used:
- uniform distribution generator;
- exponential generator;
- Bernoulli generator;
- normal distribution generator;
- geometric distribution generator;
- uniform distribution generator with range from 5 to 10;

Algorithms for those generators come from book "Symulacja cyfrowa" J. Tyszer 1990

Generators are independent of each other. Each generator uses its own uniform distribution generator. Each generator starts with different seed (10 for each generator). Seeds are stored in file **seeds.h**

# Results
Final project runs 10 independent simulations with 10 different sets of seeds for generators.
The final values of **R** and **N** are:
 - R = 250
 - N = 54
