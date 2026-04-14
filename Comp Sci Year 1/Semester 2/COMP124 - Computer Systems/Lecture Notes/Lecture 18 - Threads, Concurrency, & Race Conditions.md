## Concurrent Programming
>Stuart was talking about the type of exam questions we could get on this, and he said that we could be asked to determine how many units of time we can get a program down to by executing instructions concurrently. 
>
>This mainly just requires determining which operations are independent and which operations depend on other operations. If $x$ is the number of independent operations and $y$ is the number of dependant operations (and the first of these depends on an independent operation), the minimal time for these are $x+y$ units of time.