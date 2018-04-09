    #define _REENTRANT

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

#include <pthread.h>
#include <semaphore.h>

// The maximum number of customer threads.
#define MAX_CUSTOMERS 25

// Function prototypes...
void *custmr(void *num);
void *barb(void *);

void rndwt(int secs);

// Define the semaphores.

// waitingRoom Limits the # of customers allowed 
// to enter the waiting room at one time.
sem_t wtngRoom;   

// barberChair ensures mutually exclusive access to
// the barber chair.
sem_t barbChair;

// barberPillow is used to allow the barber to sleep
// until a customer arrives.
sem_t barPillow;

// seatBelt is used to make the customer to wait until
// the barber is done cutting his/her hair. 
sem_t stBelt;

// Flag to stop the barber thread when all customers
