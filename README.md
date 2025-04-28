# Actividad de seguimiento - Simulación 2

|Integrante|correo|usuario github|
|---|---|---|
|Juan Pablo Gómez López|juan.gomez148@udea.edu.co|jgomelop|
|Danilo Antonio Tovar Arias|danilo.tovar@udea.edu.co|DaniloTovar|

## Instrucciones

Antes de empezar a realizar esta actividad haga un **fork** de este repositorio y sobre este trabaje en la solución de las preguntas planteadas en la actividad de simulación. Las respuestas deben ser respondidas en español o si lo prefiere en ingles en el lugar señalado para ello (La palabra **answer** muestra donde).


## Homework (Simulation)

This program, [mlfq.py](mlfq.py), allows you to see how the MLFQ scheduler presented in this chapter behaves. See the [README](https://github.com/remzi-arpacidusseau/ostep-homework/blob/master/cpu-sched-mlfq/README.md) for details.


### Questions

1. Run a few randomly-generated problems with just two jobs and two queues; compute the MLFQ execution trace for each. Make your life easier by limiting the length of each job and turning off I/Os.

2. How would you run the scheduler to reproduce each of the examples in the chapter?
   
   <details>
   <summary>Answer</summary>

   **Nota:** Las salidas de cada uno de los comandos a continuación se peuden ver en la carpeta *outputs*

   **Figura 8.2** 

   time slice = allotment = 10ms

   n_jobs = 1

   n_queue = 3 

   ```bash
   python3 ./mlfq.py -l 0,200,0 -a 1 -q 10 -i 0 -c
   ```

   **Figure 8.3 (izquierda)**

   Job B

   - start time = 100

   - run time = 20

   ```bash
   python3 ./mlfq.py -l 0,200,0:100,20,0 -a 1 -q 10 -i 0 -c
   ```

   **Figura 8.3 (derecha)**

   ```bash
   python3 ./mlfq.py -l 0,200,0:50,20,1 -a 1 -q 10 -i 9 -c -S
   ```

   **Figura 8.4 (izquierda)**

   ```bash
   python3 ./mlfq.py -l 0,200,0:100,50,1:100,50,1 -a 1 -q 10 -i 1 -S -c
   ```

   **Figura 8.4 (derecha)**

   ```bash
   python3 ./mlfq.py -l 100,50,1:100,50,1:0,200,0 -a 1 -q 10 -i 1 -S -B 20 -c
   ```

   **Figura 8.5 (izquierda)**

   ```bash
   python3 ./mlfq.py -l 0,200,0:80,100,9 -q 10 -i 1 -S  -c
   ```

   **Figura 8.5 (derecha)**

   ```bash
   python3 ./mlfq.py -l 0,200,0:80,100,9 -q 10 -i 1  -c
   ```

   **Figure 8.6**

   ```bash
   python3 ./mlfq.py -l 0,200,0:0,200,0 -a 2 -Q 10,20,40 -c
   ```
   </details>
   <br>

3. How would you configure the scheduler parameters to behave just like a round-robin scheduler?

   <details>
   <summary>Answer</summary>
      Para replicar el comportamiento de Round-Robin se realizará un llamado a 3 procesos que llegan al mismo tiempo, utilizan 30 momentos para terminar sus actividades y no realizan actividades de I/O. Así mismo, se asigna un quantum de 10 para todos lo trabajos y una única cola.
      
      A través del siguiente comando, ejecutamos la situación anterior:
      
      ```
      py ./mlfq.py -l 0,30,0:0,30,0:0,30,0 -q 10 -n 1 -c
      ```
      Y a continuación podemos observar el resultado obtenido, que concuerda con el comportamiento esperado para Round-Robin.
   
      <details>
      <summary>Output</summary>
         
      ```
      Here is the list of inputs:
      OPTIONS jobs 3
      OPTIONS queues 1
      OPTIONS allotments for queue  0 is   1
      OPTIONS quantum length for queue  0 is  10
      OPTIONS boost 0
      OPTIONS ioTime 5
      OPTIONS stayAfterIO False
      OPTIONS iobump False
      
      
      For each job, three defining characteristics are given:
        startTime : at what time does the job enter the system
        runTime   : the total CPU time needed by the job to finish
        ioFreq    : every ioFreq time units, the job issues an I/O
                    (the I/O takes ioTime units to complete)
      
      Job List:
        Job  0: startTime   0 - runTime  30 - ioFreq   0
        Job  1: startTime   0 - runTime  30 - ioFreq   0
        Job  2: startTime   0 - runTime  30 - ioFreq   0
      
      
      Execution Trace:
      
      [ time 0 ] JOB BEGINS by JOB 0
      [ time 0 ] JOB BEGINS by JOB 1
      [ time 0 ] JOB BEGINS by JOB 2
      [ time 0 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 29 (of 30) ]
      [ time 1 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 28 (of 30) ]
      [ time 2 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 27 (of 30) ]
      [ time 3 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 26 (of 30) ]
      [ time 4 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 25 (of 30) ]
      [ time 5 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 24 (of 30) ]
      [ time 6 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 23 (of 30) ]
      [ time 7 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 22 (of 30) ]
      [ time 8 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 21 (of 30) ]
      [ time 9 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 20 (of 30) ]
      [ time 10 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 29 (of 30) ]
      [ time 11 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 28 (of 30) ]
      [ time 12 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 27 (of 30) ]
      [ time 13 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 26 (of 30) ]
      [ time 14 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 25 (of 30) ]
      [ time 15 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 24 (of 30) ]
      [ time 16 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 23 (of 30) ]
      [ time 17 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 22 (of 30) ]
      [ time 18 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 21 (of 30) ]
      [ time 19 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 20 (of 30) ]
      [ time 20 ] Run JOB 2 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 29 (of 30) ]
      [ time 21 ] Run JOB 2 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 28 (of 30) ]
      [ time 22 ] Run JOB 2 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 27 (of 30) ]
      [ time 23 ] Run JOB 2 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 26 (of 30) ]
      [ time 24 ] Run JOB 2 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 25 (of 30) ]
      [ time 25 ] Run JOB 2 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 24 (of 30) ]
      [ time 26 ] Run JOB 2 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 23 (of 30) ]
      [ time 27 ] Run JOB 2 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 22 (of 30) ]
      [ time 28 ] Run JOB 2 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 21 (of 30) ]
      [ time 29 ] Run JOB 2 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 20 (of 30) ]
      [ time 30 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 19 (of 30) ]
      [ time 31 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 18 (of 30) ]
      [ time 32 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 17 (of 30) ]
      [ time 33 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 16 (of 30) ]
      [ time 34 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 15 (of 30) ]
      [ time 35 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 14 (of 30) ]
      [ time 36 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 13 (of 30) ]
      [ time 37 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 12 (of 30) ]
      [ time 38 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 11 (of 30) ]
      [ time 39 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 10 (of 30) ]
      [ time 40 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 19 (of 30) ]
      [ time 41 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 18 (of 30) ]
      [ time 42 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 17 (of 30) ]
      [ time 43 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 16 (of 30) ]
      [ time 44 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 15 (of 30) ]
      [ time 45 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 14 (of 30) ]
      [ time 46 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 13 (of 30) ]
      [ time 47 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 12 (of 30) ]
      [ time 48 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 11 (of 30) ]
      [ time 49 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 10 (of 30) ]
      [ time 50 ] Run JOB 2 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 19 (of 30) ]
      [ time 51 ] Run JOB 2 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 18 (of 30) ]
      [ time 52 ] Run JOB 2 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 17 (of 30) ]
      [ time 53 ] Run JOB 2 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 16 (of 30) ]
      [ time 54 ] Run JOB 2 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 15 (of 30) ]
      [ time 55 ] Run JOB 2 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 14 (of 30) ]
      [ time 56 ] Run JOB 2 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 13 (of 30) ]
      [ time 57 ] Run JOB 2 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 12 (of 30) ]
      [ time 58 ] Run JOB 2 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 11 (of 30) ]
      [ time 59 ] Run JOB 2 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 10 (of 30) ]
      [ time 60 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 30) ]
      [ time 61 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 30) ]
      [ time 62 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 30) ]
      [ time 63 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 30) ]
      [ time 64 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 30) ]
      [ time 65 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 30) ]
      [ time 66 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 30) ]
      [ time 67 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 30) ]
      [ time 68 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 30) ]
      [ time 69 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 30) ]
      [ time 70 ] FINISHED JOB 0
      [ time 70 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 30) ]
      [ time 71 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 30) ]
      [ time 72 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 30) ]
      [ time 73 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 30) ]
      [ time 74 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 30) ]
      [ time 75 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 30) ]
      [ time 76 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 30) ]
      [ time 77 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 30) ]
      [ time 78 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 30) ]
      [ time 79 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 30) ]
      [ time 80 ] FINISHED JOB 1
      [ time 80 ] Run JOB 2 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 30) ]
      [ time 81 ] Run JOB 2 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 30) ]
      [ time 82 ] Run JOB 2 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 30) ]
      [ time 83 ] Run JOB 2 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 30) ]
      [ time 84 ] Run JOB 2 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 30) ]
      [ time 85 ] Run JOB 2 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 30) ]
      [ time 86 ] Run JOB 2 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 30) ]
      [ time 87 ] Run JOB 2 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 30) ]
      [ time 88 ] Run JOB 2 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 30) ]
      [ time 89 ] Run JOB 2 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 30) ]
      [ time 90 ] FINISHED JOB 2
      
      Final statistics:
        Job  0: startTime   0 - response   0 - turnaround  70
        Job  1: startTime   0 - response  10 - turnaround  80
        Job  2: startTime   0 - response  20 - turnaround  90
      
        Avg  2: startTime n/a - response 10.00 - turnaround 80.00
      ```
      </details>
   </details>
   <br>

5. Craft a workload with two jobs and scheduler parameters so that one job takes advantage of the older Rules 4a and 4b (turned on
with the -S flag) to game the scheduler and obtain 99% of the CPU over a particular time interval.

   <details>
   <summary>Answer</summary>
      Para replicar el comportamiento establecido se realiza un llamado a 2 procesos que llegan al mismo tiempo, el primero utiliza 30 momentos para terminar sus actividades y realiza actividades de I/O cada 10 momentos, y el segundo utiliza 50 momentos para terminar sus actividades y realiza actividades de I/O antes de que se acabe el alojamiento en la cola de alta prioridad (cada 9 momentos). Así mismo, se asigna un quantum de 10 y un tiempo de I/O de 1 para todos lo trabajos.

      A través del siguiente comando, ejecutamos la situación anterior:

      ```
      py ./mlfq.py -l 0,30,10:5,50,9 -q 10 -i 1 -S -c
      ```
      
      Y a continuación podemos observar el resultado obtenido, que concuerda con el comportamiento esperado donde el segundo proceso acapara la mayor parte del tiempo de procesamiento.
   
      <details>
      <summary>Output</summary>
         
      ```
      Here is the list of inputs:
      OPTIONS jobs 2
      OPTIONS queues 3
      OPTIONS allotments for queue  2 is   1
      OPTIONS quantum length for queue  2 is  10
      OPTIONS allotments for queue  1 is   1
      OPTIONS quantum length for queue  1 is  10
      OPTIONS allotments for queue  0 is   1
      OPTIONS quantum length for queue  0 is  10
      OPTIONS boost 0
      OPTIONS ioTime 1
      OPTIONS stayAfterIO True
      OPTIONS iobump False
      
      
      For each job, three defining characteristics are given:
        startTime : at what time does the job enter the system
        runTime   : the total CPU time needed by the job to finish
        ioFreq    : every ioFreq time units, the job issues an I/O
                    (the I/O takes ioTime units to complete)
      
      Job List:
        Job  0: startTime   0 - runTime  30 - ioFreq  10
        Job  1: startTime   5 - runTime  50 - ioFreq   9
      
      
      Execution Trace:
      
      [ time 0 ] JOB BEGINS by JOB 0
      [ time 0 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 29 (of 30) ]
      [ time 1 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 28 (of 30) ]
      [ time 2 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 27 (of 30) ]
      [ time 3 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 26 (of 30) ]
      [ time 4 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 25 (of 30) ]
      [ time 5 ] JOB BEGINS by JOB 1
      [ time 5 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 24 (of 30) ]
      [ time 6 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 23 (of 30) ]
      [ time 7 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 22 (of 30) ]
      [ time 8 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 21 (of 30) ]
      [ time 9 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 20 (of 30) ]
      [ time 10 ] IO_START by JOB 0
      IO DONE
      [ time 10 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 49 (of 50) ]
      [ time 11 ] IO_DONE by JOB 0
      [ time 11 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 48 (of 50) ]
      [ time 12 ] Run JOB 1 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 47 (of 50) ]
      [ time 13 ] Run JOB 1 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 46 (of 50) ]
      [ time 14 ] Run JOB 1 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 45 (of 50) ]
      [ time 15 ] Run JOB 1 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 44 (of 50) ]
      [ time 16 ] Run JOB 1 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 43 (of 50) ]
      [ time 17 ] Run JOB 1 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 42 (of 50) ]
      [ time 18 ] Run JOB 1 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 41 (of 50) ]
      [ time 19 ] IO_START by JOB 1
      IO DONE
      [ time 19 ] Run JOB 0 at PRIORITY 1 [ TICKS 9 ALLOT 1 TIME 19 (of 30) ]
      [ time 20 ] IO_DONE by JOB 1
      [ time 20 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 40 (of 50) ]
      [ time 21 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 39 (of 50) ]
      [ time 22 ] Run JOB 1 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 38 (of 50) ]
      [ time 23 ] Run JOB 1 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 37 (of 50) ]
      [ time 24 ] Run JOB 1 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 36 (of 50) ]
      [ time 25 ] Run JOB 1 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 35 (of 50) ]
      [ time 26 ] Run JOB 1 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 34 (of 50) ]
      [ time 27 ] Run JOB 1 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 33 (of 50) ]
      [ time 28 ] Run JOB 1 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 32 (of 50) ]
      [ time 29 ] IO_START by JOB 1
      IO DONE
      [ time 29 ] Run JOB 0 at PRIORITY 1 [ TICKS 8 ALLOT 1 TIME 18 (of 30) ]
      [ time 30 ] IO_DONE by JOB 1
      [ time 30 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 31 (of 50) ]
      [ time 31 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 30 (of 50) ]
      [ time 32 ] Run JOB 1 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 29 (of 50) ]
      [ time 33 ] Run JOB 1 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 28 (of 50) ]
      [ time 34 ] Run JOB 1 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 27 (of 50) ]
      [ time 35 ] Run JOB 1 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 26 (of 50) ]
      [ time 36 ] Run JOB 1 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 25 (of 50) ]
      [ time 37 ] Run JOB 1 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 24 (of 50) ]
      [ time 38 ] Run JOB 1 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 23 (of 50) ]
      [ time 39 ] IO_START by JOB 1
      IO DONE
      [ time 39 ] Run JOB 0 at PRIORITY 1 [ TICKS 7 ALLOT 1 TIME 17 (of 30) ]
      [ time 40 ] IO_DONE by JOB 1
      [ time 40 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 22 (of 50) ]
      [ time 41 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 21 (of 50) ]
      [ time 42 ] Run JOB 1 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 20 (of 50) ]
      [ time 43 ] Run JOB 1 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 19 (of 50) ]
      [ time 44 ] Run JOB 1 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 18 (of 50) ]
      [ time 45 ] Run JOB 1 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 17 (of 50) ]
      [ time 46 ] Run JOB 1 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 16 (of 50) ]
      [ time 47 ] Run JOB 1 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 15 (of 50) ]
      [ time 48 ] Run JOB 1 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 14 (of 50) ]
      [ time 49 ] IO_START by JOB 1
      IO DONE
      [ time 49 ] Run JOB 0 at PRIORITY 1 [ TICKS 6 ALLOT 1 TIME 16 (of 30) ]
      [ time 50 ] IO_DONE by JOB 1
      [ time 50 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 13 (of 50) ]
      [ time 51 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 12 (of 50) ]
      [ time 52 ] Run JOB 1 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 11 (of 50) ]
      [ time 53 ] Run JOB 1 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 10 (of 50) ]
      [ time 54 ] Run JOB 1 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 9 (of 50) ]
      [ time 55 ] Run JOB 1 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 8 (of 50) ]
      [ time 56 ] Run JOB 1 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 7 (of 50) ]
      [ time 57 ] Run JOB 1 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 6 (of 50) ]
      [ time 58 ] Run JOB 1 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 5 (of 50) ]
      [ time 59 ] IO_START by JOB 1
      IO DONE
      [ time 59 ] Run JOB 0 at PRIORITY 1 [ TICKS 5 ALLOT 1 TIME 15 (of 30) ]
      [ time 60 ] IO_DONE by JOB 1
      [ time 60 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 4 (of 50) ]
      [ time 61 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 3 (of 50) ]
      [ time 62 ] Run JOB 1 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 2 (of 50) ]
      [ time 63 ] Run JOB 1 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 1 (of 50) ]
      [ time 64 ] Run JOB 1 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 0 (of 50) ]
      [ time 65 ] FINISHED JOB 1
      [ time 65 ] Run JOB 0 at PRIORITY 1 [ TICKS 4 ALLOT 1 TIME 14 (of 30) ]
      [ time 66 ] Run JOB 0 at PRIORITY 1 [ TICKS 3 ALLOT 1 TIME 13 (of 30) ]
      [ time 67 ] Run JOB 0 at PRIORITY 1 [ TICKS 2 ALLOT 1 TIME 12 (of 30) ]
      [ time 68 ] Run JOB 0 at PRIORITY 1 [ TICKS 1 ALLOT 1 TIME 11 (of 30) ]
      [ time 69 ] Run JOB 0 at PRIORITY 1 [ TICKS 0 ALLOT 1 TIME 10 (of 30) ]
      [ time 70 ] IO_START by JOB 0
      IO DONE
      [ time 70 ] IDLE
      [ time 71 ] IO_DONE by JOB 0
      [ time 71 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 30) ]
      [ time 72 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 30) ]
      [ time 73 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 30) ]
      [ time 74 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 30) ]
      [ time 75 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 30) ]
      [ time 76 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 30) ]
      [ time 77 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 30) ]
      [ time 78 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 30) ]
      [ time 79 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 30) ]
      [ time 80 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 30) ]
      [ time 81 ] FINISHED JOB 0
      
      Final statistics:
        Job  0: startTime   0 - response   0 - turnaround  81
        Job  1: startTime   5 - response   5 - turnaround  60
      
        Avg  1: startTime n/a - response 2.50 - turnaround 70.50
      ```
      </details>
   </details>
   <br>

7. Given a system with a quantum length of 10 ms in its highest queue, how often would you have to boost jobs back to the highest priority level (with the `-B` flag) in order to guarantee that a single longrunning (and potentially-starving) job gets at least 5% of the CPU?

   <details>
   <summary>Answer</summary>
      Para replicar el comportamiento establecido se realiza un llamado a 3 procesos que llegan al mismo tiempo, el primero utiliza 100 momentos para terminar sus actividades y no realiza actividades de I/O, y los otros dos utilizan 50 momentos para terminar sus actividades y realiza actividades de I/O cada 2 momentos. Así mismo, se asigna un quantum de 10 y un tiempo de I/O de 1 para todos lo trabajos; y adicionalmente se asigna un boost cada 20 momentos.
      
      A través del siguiente comando, ejecutamos la situación anterior:
      
      ```
      py ./mlfq.py -l 0,100,0:0,50,2:0,50,2 -q 10 -i 1 -S -B 20 -c
      ```
      
      Y a continuación podemos observar el resultado obtenido, que establece que realizando un boost cada 20 ms permite al trabajo CPU-Bound realizar sus actividades en vez de quedar starved mientras los otros procesos acaparan la CPU.
      <details>
      <summary>Output</summary>
      
      ```
      Here is the list of inputs:
      OPTIONS jobs 3
      OPTIONS queues 3
      OPTIONS allotments for queue  2 is   1
      OPTIONS quantum length for queue  2 is  10
      OPTIONS allotments for queue  1 is   1
      OPTIONS quantum length for queue  1 is  10
      OPTIONS allotments for queue  0 is   1
      OPTIONS quantum length for queue  0 is  10
      OPTIONS boost 20
      OPTIONS ioTime 1
      OPTIONS stayAfterIO True
      OPTIONS iobump False
      
      
      For each job, three defining characteristics are given:
        startTime : at what time does the job enter the system
        runTime   : the total CPU time needed by the job to finish
        ioFreq    : every ioFreq time units, the job issues an I/O
                    (the I/O takes ioTime units to complete)
      
      Job List:
        Job  0: startTime   0 - runTime 100 - ioFreq   0
        Job  1: startTime   0 - runTime  50 - ioFreq   2
        Job  2: startTime   0 - runTime  50 - ioFreq   2
      
      
      Execution Trace:
      
      [ time 0 ] JOB BEGINS by JOB 0
      [ time 0 ] JOB BEGINS by JOB 1
      [ time 0 ] JOB BEGINS by JOB 2
      [ time 0 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 99 (of 100) ]
      [ time 1 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 98 (of 100) ]
      [ time 2 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 97 (of 100) ]
      [ time 3 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 96 (of 100) ]
      [ time 4 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 95 (of 100) ]
      [ time 5 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 94 (of 100) ]
      [ time 6 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 93 (of 100) ]
      [ time 7 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 92 (of 100) ]
      [ time 8 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 91 (of 100) ]
      [ time 9 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 90 (of 100) ]
      [ time 10 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 49 (of 50) ]
      [ time 11 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 48 (of 50) ]
      [ time 12 ] IO_START by JOB 1
      IO DONE
      [ time 12 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 49 (of 50) ]
      [ time 13 ] IO_DONE by JOB 1
      [ time 13 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 48 (of 50) ]
      [ time 14 ] IO_START by JOB 2
      IO DONE
      [ time 14 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 47 (of 50) ]
      [ time 15 ] IO_DONE by JOB 2
      [ time 15 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 46 (of 50) ]
      [ time 16 ] IO_START by JOB 1
      IO DONE
      [ time 16 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 47 (of 50) ]
      [ time 17 ] IO_DONE by JOB 1
      [ time 17 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 46 (of 50) ]
      [ time 18 ] IO_START by JOB 2
      IO DONE
      [ time 18 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 45 (of 50) ]
      [ time 19 ] IO_DONE by JOB 2
      [ time 19 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 44 (of 50) ]
      [ time 20 ] IO_START by JOB 1
      IO DONE
      [ time 20 ] BOOST ( every 20 )
      [ time 20 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 45 (of 50) ]
      [ time 21 ] IO_DONE by JOB 1
      [ time 21 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 44 (of 50) ]
      [ time 22 ] IO_START by JOB 2
      IO DONE
      [ time 22 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 89 (of 100) ]
      [ time 23 ] IO_DONE by JOB 2
      [ time 23 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 88 (of 100) ]
      [ time 24 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 87 (of 100) ]
      [ time 25 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 86 (of 100) ]
      [ time 26 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 85 (of 100) ]
      [ time 27 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 84 (of 100) ]
      [ time 28 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 83 (of 100) ]
      [ time 29 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 82 (of 100) ]
      [ time 30 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 81 (of 100) ]
      [ time 31 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 80 (of 100) ]
      [ time 32 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 43 (of 50) ]
      [ time 33 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 42 (of 50) ]
      [ time 34 ] IO_START by JOB 1
      IO DONE
      [ time 34 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 43 (of 50) ]
      [ time 35 ] IO_DONE by JOB 1
      [ time 35 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 42 (of 50) ]
      [ time 36 ] IO_START by JOB 2
      IO DONE
      [ time 36 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 41 (of 50) ]
      [ time 37 ] IO_DONE by JOB 2
      [ time 37 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 40 (of 50) ]
      [ time 38 ] IO_START by JOB 1
      IO DONE
      [ time 38 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 41 (of 50) ]
      [ time 39 ] IO_DONE by JOB 1
      [ time 39 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 40 (of 50) ]
      [ time 40 ] IO_START by JOB 2
      IO DONE
      [ time 40 ] BOOST ( every 20 )
      [ time 40 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 39 (of 50) ]
      [ time 41 ] IO_DONE by JOB 2
      [ time 41 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 38 (of 50) ]
      [ time 42 ] IO_START by JOB 1
      IO DONE
      [ time 42 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 79 (of 100) ]
      [ time 43 ] IO_DONE by JOB 1
      [ time 43 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 78 (of 100) ]
      [ time 44 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 77 (of 100) ]
      [ time 45 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 76 (of 100) ]
      [ time 46 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 75 (of 100) ]
      [ time 47 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 74 (of 100) ]
      [ time 48 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 73 (of 100) ]
      [ time 49 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 72 (of 100) ]
      [ time 50 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 71 (of 100) ]
      [ time 51 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 70 (of 100) ]
      [ time 52 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 39 (of 50) ]
      [ time 53 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 38 (of 50) ]
      [ time 54 ] IO_START by JOB 2
      IO DONE
      [ time 54 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 37 (of 50) ]
      [ time 55 ] IO_DONE by JOB 2
      [ time 55 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 36 (of 50) ]
      [ time 56 ] IO_START by JOB 1
      IO DONE
      [ time 56 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 37 (of 50) ]
      [ time 57 ] IO_DONE by JOB 1
      [ time 57 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 36 (of 50) ]
      [ time 58 ] IO_START by JOB 2
      IO DONE
      [ time 58 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 35 (of 50) ]
      [ time 59 ] IO_DONE by JOB 2
      [ time 59 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 34 (of 50) ]
      [ time 60 ] IO_START by JOB 1
      IO DONE
      [ time 60 ] BOOST ( every 20 )
      [ time 60 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 35 (of 50) ]
      [ time 61 ] IO_DONE by JOB 1
      [ time 61 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 34 (of 50) ]
      [ time 62 ] IO_START by JOB 2
      IO DONE
      [ time 62 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 69 (of 100) ]
      [ time 63 ] IO_DONE by JOB 2
      [ time 63 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 68 (of 100) ]
      [ time 64 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 67 (of 100) ]
      [ time 65 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 66 (of 100) ]
      [ time 66 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 65 (of 100) ]
      [ time 67 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 64 (of 100) ]
      [ time 68 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 63 (of 100) ]
      [ time 69 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 62 (of 100) ]
      [ time 70 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 61 (of 100) ]
      [ time 71 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 60 (of 100) ]
      [ time 72 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 33 (of 50) ]
      [ time 73 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 32 (of 50) ]
      [ time 74 ] IO_START by JOB 1
      IO DONE
      [ time 74 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 33 (of 50) ]
      [ time 75 ] IO_DONE by JOB 1
      [ time 75 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 32 (of 50) ]
      [ time 76 ] IO_START by JOB 2
      IO DONE
      [ time 76 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 31 (of 50) ]
      [ time 77 ] IO_DONE by JOB 2
      [ time 77 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 30 (of 50) ]
      [ time 78 ] IO_START by JOB 1
      IO DONE
      [ time 78 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 31 (of 50) ]
      [ time 79 ] IO_DONE by JOB 1
      [ time 79 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 30 (of 50) ]
      [ time 80 ] IO_START by JOB 2
      IO DONE
      [ time 80 ] BOOST ( every 20 )
      [ time 80 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 29 (of 50) ]
      [ time 81 ] IO_DONE by JOB 2
      [ time 81 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 28 (of 50) ]
      [ time 82 ] IO_START by JOB 1
      IO DONE
      [ time 82 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 59 (of 100) ]
      [ time 83 ] IO_DONE by JOB 1
      [ time 83 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 58 (of 100) ]
      [ time 84 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 57 (of 100) ]
      [ time 85 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 56 (of 100) ]
      [ time 86 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 55 (of 100) ]
      [ time 87 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 54 (of 100) ]
      [ time 88 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 53 (of 100) ]
      [ time 89 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 52 (of 100) ]
      [ time 90 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 51 (of 100) ]
      [ time 91 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 50 (of 100) ]
      [ time 92 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 29 (of 50) ]
      [ time 93 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 28 (of 50) ]
      [ time 94 ] IO_START by JOB 2
      IO DONE
      [ time 94 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 27 (of 50) ]
      [ time 95 ] IO_DONE by JOB 2
      [ time 95 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 26 (of 50) ]
      [ time 96 ] IO_START by JOB 1
      IO DONE
      [ time 96 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 27 (of 50) ]
      [ time 97 ] IO_DONE by JOB 1
      [ time 97 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 26 (of 50) ]
      [ time 98 ] IO_START by JOB 2
      IO DONE
      [ time 98 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 25 (of 50) ]
      [ time 99 ] IO_DONE by JOB 2
      [ time 99 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 24 (of 50) ]
      [ time 100 ] IO_START by JOB 1
      IO DONE
      [ time 100 ] BOOST ( every 20 )
      [ time 100 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 25 (of 50) ]
      [ time 101 ] IO_DONE by JOB 1
      [ time 101 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 24 (of 50) ]
      [ time 102 ] IO_START by JOB 2
      IO DONE
      [ time 102 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 49 (of 100) ]
      [ time 103 ] IO_DONE by JOB 2
      [ time 103 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 48 (of 100) ]
      [ time 104 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 47 (of 100) ]
      [ time 105 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 46 (of 100) ]
      [ time 106 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 45 (of 100) ]
      [ time 107 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 44 (of 100) ]
      [ time 108 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 43 (of 100) ]
      [ time 109 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 42 (of 100) ]
      [ time 110 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 41 (of 100) ]
      [ time 111 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 40 (of 100) ]
      [ time 112 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 23 (of 50) ]
      [ time 113 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 22 (of 50) ]
      [ time 114 ] IO_START by JOB 1
      IO DONE
      [ time 114 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 23 (of 50) ]
      [ time 115 ] IO_DONE by JOB 1
      [ time 115 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 22 (of 50) ]
      [ time 116 ] IO_START by JOB 2
      IO DONE
      [ time 116 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 21 (of 50) ]
      [ time 117 ] IO_DONE by JOB 2
      [ time 117 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 20 (of 50) ]
      [ time 118 ] IO_START by JOB 1
      IO DONE
      [ time 118 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 21 (of 50) ]
      [ time 119 ] IO_DONE by JOB 1
      [ time 119 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 20 (of 50) ]
      [ time 120 ] IO_START by JOB 2
      IO DONE
      [ time 120 ] BOOST ( every 20 )
      [ time 120 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 19 (of 50) ]
      [ time 121 ] IO_DONE by JOB 2
      [ time 121 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 18 (of 50) ]
      [ time 122 ] IO_START by JOB 1
      IO DONE
      [ time 122 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 39 (of 100) ]
      [ time 123 ] IO_DONE by JOB 1
      [ time 123 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 38 (of 100) ]
      [ time 124 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 37 (of 100) ]
      [ time 125 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 36 (of 100) ]
      [ time 126 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 35 (of 100) ]
      [ time 127 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 34 (of 100) ]
      [ time 128 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 33 (of 100) ]
      [ time 129 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 32 (of 100) ]
      [ time 130 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 31 (of 100) ]
      [ time 131 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 30 (of 100) ]
      [ time 132 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 19 (of 50) ]
      [ time 133 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 18 (of 50) ]
      [ time 134 ] IO_START by JOB 2
      IO DONE
      [ time 134 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 17 (of 50) ]
      [ time 135 ] IO_DONE by JOB 2
      [ time 135 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 16 (of 50) ]
      [ time 136 ] IO_START by JOB 1
      IO DONE
      [ time 136 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 17 (of 50) ]
      [ time 137 ] IO_DONE by JOB 1
      [ time 137 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 16 (of 50) ]
      [ time 138 ] IO_START by JOB 2
      IO DONE
      [ time 138 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 15 (of 50) ]
      [ time 139 ] IO_DONE by JOB 2
      [ time 139 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 14 (of 50) ]
      [ time 140 ] IO_START by JOB 1
      IO DONE
      [ time 140 ] BOOST ( every 20 )
      [ time 140 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 15 (of 50) ]
      [ time 141 ] IO_DONE by JOB 1
      [ time 141 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 14 (of 50) ]
      [ time 142 ] IO_START by JOB 2
      IO DONE
      [ time 142 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 29 (of 100) ]
      [ time 143 ] IO_DONE by JOB 2
      [ time 143 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 28 (of 100) ]
      [ time 144 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 27 (of 100) ]
      [ time 145 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 26 (of 100) ]
      [ time 146 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 25 (of 100) ]
      [ time 147 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 24 (of 100) ]
      [ time 148 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 23 (of 100) ]
      [ time 149 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 22 (of 100) ]
      [ time 150 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 21 (of 100) ]
      [ time 151 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 20 (of 100) ]
      [ time 152 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 13 (of 50) ]
      [ time 153 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 12 (of 50) ]
      [ time 154 ] IO_START by JOB 1
      IO DONE
      [ time 154 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 13 (of 50) ]
      [ time 155 ] IO_DONE by JOB 1
      [ time 155 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 12 (of 50) ]
      [ time 156 ] IO_START by JOB 2
      IO DONE
      [ time 156 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 11 (of 50) ]
      [ time 157 ] IO_DONE by JOB 2
      [ time 157 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 10 (of 50) ]
      [ time 158 ] IO_START by JOB 1
      IO DONE
      [ time 158 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 11 (of 50) ]
      [ time 159 ] IO_DONE by JOB 1
      [ time 159 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 10 (of 50) ]
      [ time 160 ] IO_START by JOB 2
      IO DONE
      [ time 160 ] BOOST ( every 20 )
      [ time 160 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 9 (of 50) ]
      [ time 161 ] IO_DONE by JOB 2
      [ time 161 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 8 (of 50) ]
      [ time 162 ] IO_START by JOB 1
      IO DONE
      [ time 162 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 19 (of 100) ]
      [ time 163 ] IO_DONE by JOB 1
      [ time 163 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 18 (of 100) ]
      [ time 164 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 17 (of 100) ]
      [ time 165 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 16 (of 100) ]
      [ time 166 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 15 (of 100) ]
      [ time 167 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 14 (of 100) ]
      [ time 168 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 13 (of 100) ]
      [ time 169 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 12 (of 100) ]
      [ time 170 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 11 (of 100) ]
      [ time 171 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 10 (of 100) ]
      [ time 172 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 9 (of 50) ]
      [ time 173 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 8 (of 50) ]
      [ time 174 ] IO_START by JOB 2
      IO DONE
      [ time 174 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 7 (of 50) ]
      [ time 175 ] IO_DONE by JOB 2
      [ time 175 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 6 (of 50) ]
      [ time 176 ] IO_START by JOB 1
      IO DONE
      [ time 176 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 7 (of 50) ]
      [ time 177 ] IO_DONE by JOB 1
      [ time 177 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 6 (of 50) ]
      [ time 178 ] IO_START by JOB 2
      IO DONE
      [ time 178 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 5 (of 50) ]
      [ time 179 ] IO_DONE by JOB 2
      [ time 179 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 4 (of 50) ]
      [ time 180 ] IO_START by JOB 1
      IO DONE
      [ time 180 ] BOOST ( every 20 )
      [ time 180 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 5 (of 50) ]
      [ time 181 ] IO_DONE by JOB 1
      [ time 181 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 4 (of 50) ]
      [ time 182 ] IO_START by JOB 2
      IO DONE
      [ time 182 ] Run JOB 0 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 9 (of 100) ]
      [ time 183 ] IO_DONE by JOB 2
      [ time 183 ] Run JOB 0 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 8 (of 100) ]
      [ time 184 ] Run JOB 0 at PRIORITY 2 [ TICKS 7 ALLOT 1 TIME 7 (of 100) ]
      [ time 185 ] Run JOB 0 at PRIORITY 2 [ TICKS 6 ALLOT 1 TIME 6 (of 100) ]
      [ time 186 ] Run JOB 0 at PRIORITY 2 [ TICKS 5 ALLOT 1 TIME 5 (of 100) ]
      [ time 187 ] Run JOB 0 at PRIORITY 2 [ TICKS 4 ALLOT 1 TIME 4 (of 100) ]
      [ time 188 ] Run JOB 0 at PRIORITY 2 [ TICKS 3 ALLOT 1 TIME 3 (of 100) ]
      [ time 189 ] Run JOB 0 at PRIORITY 2 [ TICKS 2 ALLOT 1 TIME 2 (of 100) ]
      [ time 190 ] Run JOB 0 at PRIORITY 2 [ TICKS 1 ALLOT 1 TIME 1 (of 100) ]
      [ time 191 ] Run JOB 0 at PRIORITY 2 [ TICKS 0 ALLOT 1 TIME 0 (of 100) ]
      [ time 192 ] FINISHED JOB 0
      [ time 192 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 3 (of 50) ]
      [ time 193 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 2 (of 50) ]
      [ time 194 ] IO_START by JOB 1
      IO DONE
      [ time 194 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 3 (of 50) ]
      [ time 195 ] IO_DONE by JOB 1
      [ time 195 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 2 (of 50) ]
      [ time 196 ] IO_START by JOB 2
      IO DONE
      [ time 196 ] Run JOB 1 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 1 (of 50) ]
      [ time 197 ] IO_DONE by JOB 2
      [ time 197 ] Run JOB 1 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 0 (of 50) ]
      [ time 198 ] FINISHED JOB 1
      [ time 198 ] Run JOB 2 at PRIORITY 2 [ TICKS 9 ALLOT 1 TIME 1 (of 50) ]
      [ time 199 ] Run JOB 2 at PRIORITY 2 [ TICKS 8 ALLOT 1 TIME 0 (of 50) ]
      [ time 200 ] FINISHED JOB 2
      
      Final statistics:
        Job  0: startTime   0 - response   0 - turnaround 192
        Job  1: startTime   0 - response  10 - turnaround 198
        Job  2: startTime   0 - response  12 - turnaround 200
      
        Avg  2: startTime n/a - response 7.33 - turnaround 196.67
      ```
      </details>   
   </details>
   <br>

9. One question that arises in scheduling is which end of a queue to add a job that just finished I/O; the -I flag changes this behavior
for this scheduling simulator. Play around with some workloads and see if you can see the effect of this flag.

   <details>
   <summary>Answer</summary>
      Al realizar pruebas con las siguientes opciones, se obtuvo que cuando no se utiliza -I los procesos terminan sus tiempos de alojamiento antes de cambiar al otro proceso, pero que cuando se utiliza -I el proceso que realiza actividades de I/O se vuelve apropiativo y toma prioridad sobre el uso de la CPU.
      
      - Caso 1:
      
      ```
      py ./mlfq.py -l 0,100,0:0,50,10 -q 10 -i 1 -n 1 -c
      ```
      
      <details>
      <summary>Output Caso 1</summary>
         
      ```
         Here is the list of inputs:
         OPTIONS jobs 2
         OPTIONS queues 1
         OPTIONS allotments for queue  0 is   1
         OPTIONS quantum length for queue  0 is  10
         OPTIONS boost 0
         OPTIONS ioTime 1
         OPTIONS stayAfterIO False
         OPTIONS iobump False
         
         
         For each job, three defining characteristics are given:
           startTime : at what time does the job enter the system
           runTime   : the total CPU time needed by the job to finish
           ioFreq    : every ioFreq time units, the job issues an I/O
                       (the I/O takes ioTime units to complete)
         
         Job List:
           Job  0: startTime   0 - runTime 100 - ioFreq   0
           Job  1: startTime   0 - runTime  50 - ioFreq  10
         
         
         Execution Trace:
         
         [ time 0 ] JOB BEGINS by JOB 0
         [ time 0 ] JOB BEGINS by JOB 1
         [ time 0 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 99 (of 100) ]
         [ time 1 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 98 (of 100) ]
         [ time 2 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 97 (of 100) ]
         [ time 3 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 96 (of 100) ]
         [ time 4 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 95 (of 100) ]
         [ time 5 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 94 (of 100) ]
         [ time 6 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 93 (of 100) ]
         [ time 7 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 92 (of 100) ]
         [ time 8 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 91 (of 100) ]
         [ time 9 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 90 (of 100) ]
         [ time 10 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 49 (of 50) ]
         [ time 11 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 48 (of 50) ]
         [ time 12 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 47 (of 50) ]
         [ time 13 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 46 (of 50) ]
         [ time 14 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 45 (of 50) ]
         [ time 15 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 44 (of 50) ]
         [ time 16 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 43 (of 50) ]
         [ time 17 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 42 (of 50) ]
         [ time 18 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 41 (of 50) ]
         [ time 19 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 40 (of 50) ]
         [ time 20 ] IO_START by JOB 1
         IO DONE
         [ time 20 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 89 (of 100) ]
         [ time 21 ] IO_DONE by JOB 1
         [ time 21 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 88 (of 100) ]
         [ time 22 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 87 (of 100) ]
         [ time 23 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 86 (of 100) ]
         [ time 24 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 85 (of 100) ]
         [ time 25 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 84 (of 100) ]
         [ time 26 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 83 (of 100) ]
         [ time 27 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 82 (of 100) ]
         [ time 28 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 81 (of 100) ]
         [ time 29 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 80 (of 100) ]
         [ time 30 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 39 (of 50) ]
         [ time 31 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 38 (of 50) ]
         [ time 32 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 37 (of 50) ]
         [ time 33 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 36 (of 50) ]
         [ time 34 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 35 (of 50) ]
         [ time 35 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 34 (of 50) ]
         [ time 36 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 33 (of 50) ]
         [ time 37 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 32 (of 50) ]
         [ time 38 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 31 (of 50) ]
         [ time 39 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 30 (of 50) ]
         [ time 40 ] IO_START by JOB 1
         IO DONE
         [ time 40 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 79 (of 100) ]
         [ time 41 ] IO_DONE by JOB 1
         [ time 41 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 78 (of 100) ]
         [ time 42 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 77 (of 100) ]
         [ time 43 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 76 (of 100) ]
         [ time 44 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 75 (of 100) ]
         [ time 45 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 74 (of 100) ]
         [ time 46 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 73 (of 100) ]
         [ time 47 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 72 (of 100) ]
         [ time 48 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 71 (of 100) ]
         [ time 49 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 70 (of 100) ]
         [ time 50 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 29 (of 50) ]
         [ time 51 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 28 (of 50) ]
         [ time 52 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 27 (of 50) ]
         [ time 53 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 26 (of 50) ]
         [ time 54 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 25 (of 50) ]
         [ time 55 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 24 (of 50) ]
         [ time 56 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 23 (of 50) ]
         [ time 57 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 22 (of 50) ]
         [ time 58 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 21 (of 50) ]
         [ time 59 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 20 (of 50) ]
         [ time 60 ] IO_START by JOB 1
         IO DONE
         [ time 60 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 69 (of 100) ]
         [ time 61 ] IO_DONE by JOB 1
         [ time 61 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 68 (of 100) ]
         [ time 62 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 67 (of 100) ]
         [ time 63 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 66 (of 100) ]
         [ time 64 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 65 (of 100) ]
         [ time 65 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 64 (of 100) ]
         [ time 66 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 63 (of 100) ]
         [ time 67 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 62 (of 100) ]
         [ time 68 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 61 (of 100) ]
         [ time 69 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 60 (of 100) ]
         [ time 70 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 19 (of 50) ]
         [ time 71 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 18 (of 50) ]
         [ time 72 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 17 (of 50) ]
         [ time 73 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 16 (of 50) ]
         [ time 74 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 15 (of 50) ]
         [ time 75 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 14 (of 50) ]
         [ time 76 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 13 (of 50) ]
         [ time 77 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 12 (of 50) ]
         [ time 78 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 11 (of 50) ]
         [ time 79 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 10 (of 50) ]
         [ time 80 ] IO_START by JOB 1
         IO DONE
         [ time 80 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 59 (of 100) ]
         [ time 81 ] IO_DONE by JOB 1
         [ time 81 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 58 (of 100) ]
         [ time 82 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 57 (of 100) ]
         [ time 83 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 56 (of 100) ]
         [ time 84 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 55 (of 100) ]
         [ time 85 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 54 (of 100) ]
         [ time 86 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 53 (of 100) ]
         [ time 87 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 52 (of 100) ]
         [ time 88 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 51 (of 100) ]
         [ time 89 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 50 (of 100) ]
         [ time 90 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 50) ]
         [ time 91 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 50) ]
         [ time 92 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 50) ]
         [ time 93 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 50) ]
         [ time 94 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 50) ]
         [ time 95 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 50) ]
         [ time 96 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 50) ]
         [ time 97 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 50) ]
         [ time 98 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 50) ]
         [ time 99 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 50) ]
         [ time 100 ] FINISHED JOB 1
         [ time 100 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 49 (of 100) ]
         [ time 101 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 48 (of 100) ]
         [ time 102 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 47 (of 100) ]
         [ time 103 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 46 (of 100) ]
         [ time 104 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 45 (of 100) ]
         [ time 105 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 44 (of 100) ]
         [ time 106 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 43 (of 100) ]
         [ time 107 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 42 (of 100) ]
         [ time 108 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 41 (of 100) ]
         [ time 109 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 40 (of 100) ]
         [ time 110 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 39 (of 100) ]
         [ time 111 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 38 (of 100) ]
         [ time 112 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 37 (of 100) ]
         [ time 113 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 36 (of 100) ]
         [ time 114 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 35 (of 100) ]
         [ time 115 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 34 (of 100) ]
         [ time 116 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 33 (of 100) ]
         [ time 117 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 32 (of 100) ]
         [ time 118 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 31 (of 100) ]
         [ time 119 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 30 (of 100) ]
         [ time 120 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 29 (of 100) ]
         [ time 121 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 28 (of 100) ]
         [ time 122 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 27 (of 100) ]
         [ time 123 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 26 (of 100) ]
         [ time 124 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 25 (of 100) ]
         [ time 125 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 24 (of 100) ]
         [ time 126 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 23 (of 100) ]
         [ time 127 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 22 (of 100) ]
         [ time 128 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 21 (of 100) ]
         [ time 129 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 20 (of 100) ]
         [ time 130 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 19 (of 100) ]
         [ time 131 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 18 (of 100) ]
         [ time 132 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 17 (of 100) ]
         [ time 133 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 16 (of 100) ]
         [ time 134 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 15 (of 100) ]
         [ time 135 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 14 (of 100) ]
         [ time 136 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 13 (of 100) ]
         [ time 137 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 12 (of 100) ]
         [ time 138 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 11 (of 100) ]
         [ time 139 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 10 (of 100) ]
         [ time 140 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 100) ]
         [ time 141 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 100) ]
         [ time 142 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 100) ]
         [ time 143 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 100) ]
         [ time 144 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 100) ]
         [ time 145 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 100) ]
         [ time 146 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 100) ]
         [ time 147 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 100) ]
         [ time 148 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 100) ]
         [ time 149 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 100) ]
         [ time 150 ] FINISHED JOB 0
         
         Final statistics:
           Job  0: startTime   0 - response   0 - turnaround 150
           Job  1: startTime   0 - response  10 - turnaround 100
         
           Avg  1: startTime n/a - response 5.00 - turnaround 125.00
      ```
      
      </details>
      
      - Caso 2:

      ```
      py ./mlfq.py -l 0,100,0:0,50,10 -q 10 -i 1 -n 1 -I -c
      ```
      <details>
      <summary>Output Caso 2</summary>
         
      ```
         Here is the list of inputs:
         OPTIONS jobs 2
         OPTIONS queues 1
         OPTIONS allotments for queue  0 is   1
         OPTIONS quantum length for queue  0 is  10
         OPTIONS boost 0
         OPTIONS ioTime 1
         OPTIONS stayAfterIO False
         OPTIONS iobump True
         
         
         For each job, three defining characteristics are given:
           startTime : at what time does the job enter the system
           runTime   : the total CPU time needed by the job to finish
           ioFreq    : every ioFreq time units, the job issues an I/O
                       (the I/O takes ioTime units to complete)
         
         Job List:
           Job  0: startTime   0 - runTime 100 - ioFreq   0
           Job  1: startTime   0 - runTime  50 - ioFreq  10
         
         
         Execution Trace:
         
         [ time 0 ] JOB BEGINS by JOB 0
         [ time 0 ] JOB BEGINS by JOB 1
         [ time 0 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 99 (of 100) ]
         [ time 1 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 98 (of 100) ]
         [ time 2 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 97 (of 100) ]
         [ time 3 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 96 (of 100) ]
         [ time 4 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 95 (of 100) ]
         [ time 5 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 94 (of 100) ]
         [ time 6 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 93 (of 100) ]
         [ time 7 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 92 (of 100) ]
         [ time 8 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 91 (of 100) ]
         [ time 9 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 90 (of 100) ]
         [ time 10 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 49 (of 50) ]
         [ time 11 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 48 (of 50) ]
         [ time 12 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 47 (of 50) ]
         [ time 13 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 46 (of 50) ]
         [ time 14 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 45 (of 50) ]
         [ time 15 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 44 (of 50) ]
         [ time 16 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 43 (of 50) ]
         [ time 17 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 42 (of 50) ]
         [ time 18 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 41 (of 50) ]
         [ time 19 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 40 (of 50) ]
         [ time 20 ] IO_START by JOB 1
         IO DONE
         [ time 20 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 89 (of 100) ]
         [ time 21 ] IO_DONE by JOB 1
         [ time 21 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 39 (of 50) ]
         [ time 22 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 38 (of 50) ]
         [ time 23 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 37 (of 50) ]
         [ time 24 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 36 (of 50) ]
         [ time 25 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 35 (of 50) ]
         [ time 26 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 34 (of 50) ]
         [ time 27 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 33 (of 50) ]
         [ time 28 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 32 (of 50) ]
         [ time 29 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 31 (of 50) ]
         [ time 30 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 30 (of 50) ]
         [ time 31 ] IO_START by JOB 1
         IO DONE
         [ time 31 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 88 (of 100) ]
         [ time 32 ] IO_DONE by JOB 1
         [ time 32 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 29 (of 50) ]
         [ time 33 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 28 (of 50) ]
         [ time 34 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 27 (of 50) ]
         [ time 35 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 26 (of 50) ]
         [ time 36 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 25 (of 50) ]
         [ time 37 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 24 (of 50) ]
         [ time 38 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 23 (of 50) ]
         [ time 39 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 22 (of 50) ]
         [ time 40 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 21 (of 50) ]
         [ time 41 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 20 (of 50) ]
         [ time 42 ] IO_START by JOB 1
         IO DONE
         [ time 42 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 87 (of 100) ]
         [ time 43 ] IO_DONE by JOB 1
         [ time 43 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 19 (of 50) ]
         [ time 44 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 18 (of 50) ]
         [ time 45 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 17 (of 50) ]
         [ time 46 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 16 (of 50) ]
         [ time 47 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 15 (of 50) ]
         [ time 48 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 14 (of 50) ]
         [ time 49 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 13 (of 50) ]
         [ time 50 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 12 (of 50) ]
         [ time 51 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 11 (of 50) ]
         [ time 52 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 10 (of 50) ]
         [ time 53 ] IO_START by JOB 1
         IO DONE
         [ time 53 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 86 (of 100) ]
         [ time 54 ] IO_DONE by JOB 1
         [ time 54 ] Run JOB 1 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 50) ]
         [ time 55 ] Run JOB 1 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 50) ]
         [ time 56 ] Run JOB 1 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 50) ]
         [ time 57 ] Run JOB 1 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 50) ]
         [ time 58 ] Run JOB 1 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 50) ]
         [ time 59 ] Run JOB 1 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 50) ]
         [ time 60 ] Run JOB 1 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 50) ]
         [ time 61 ] Run JOB 1 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 50) ]
         [ time 62 ] Run JOB 1 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 50) ]
         [ time 63 ] Run JOB 1 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 50) ]
         [ time 64 ] FINISHED JOB 1
         [ time 64 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 85 (of 100) ]
         [ time 65 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 84 (of 100) ]
         [ time 66 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 83 (of 100) ]
         [ time 67 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 82 (of 100) ]
         [ time 68 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 81 (of 100) ]
         [ time 69 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 80 (of 100) ]
         [ time 70 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 79 (of 100) ]
         [ time 71 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 78 (of 100) ]
         [ time 72 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 77 (of 100) ]
         [ time 73 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 76 (of 100) ]
         [ time 74 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 75 (of 100) ]
         [ time 75 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 74 (of 100) ]
         [ time 76 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 73 (of 100) ]
         [ time 77 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 72 (of 100) ]
         [ time 78 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 71 (of 100) ]
         [ time 79 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 70 (of 100) ]
         [ time 80 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 69 (of 100) ]
         [ time 81 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 68 (of 100) ]
         [ time 82 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 67 (of 100) ]
         [ time 83 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 66 (of 100) ]
         [ time 84 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 65 (of 100) ]
         [ time 85 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 64 (of 100) ]
         [ time 86 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 63 (of 100) ]
         [ time 87 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 62 (of 100) ]
         [ time 88 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 61 (of 100) ]
         [ time 89 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 60 (of 100) ]
         [ time 90 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 59 (of 100) ]
         [ time 91 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 58 (of 100) ]
         [ time 92 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 57 (of 100) ]
         [ time 93 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 56 (of 100) ]
         [ time 94 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 55 (of 100) ]
         [ time 95 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 54 (of 100) ]
         [ time 96 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 53 (of 100) ]
         [ time 97 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 52 (of 100) ]
         [ time 98 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 51 (of 100) ]
         [ time 99 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 50 (of 100) ]
         [ time 100 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 49 (of 100) ]
         [ time 101 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 48 (of 100) ]
         [ time 102 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 47 (of 100) ]
         [ time 103 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 46 (of 100) ]
         [ time 104 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 45 (of 100) ]
         [ time 105 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 44 (of 100) ]
         [ time 106 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 43 (of 100) ]
         [ time 107 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 42 (of 100) ]
         [ time 108 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 41 (of 100) ]
         [ time 109 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 40 (of 100) ]
         [ time 110 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 39 (of 100) ]
         [ time 111 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 38 (of 100) ]
         [ time 112 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 37 (of 100) ]
         [ time 113 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 36 (of 100) ]
         [ time 114 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 35 (of 100) ]
         [ time 115 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 34 (of 100) ]
         [ time 116 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 33 (of 100) ]
         [ time 117 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 32 (of 100) ]
         [ time 118 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 31 (of 100) ]
         [ time 119 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 30 (of 100) ]
         [ time 120 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 29 (of 100) ]
         [ time 121 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 28 (of 100) ]
         [ time 122 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 27 (of 100) ]
         [ time 123 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 26 (of 100) ]
         [ time 124 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 25 (of 100) ]
         [ time 125 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 24 (of 100) ]
         [ time 126 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 23 (of 100) ]
         [ time 127 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 22 (of 100) ]
         [ time 128 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 21 (of 100) ]
         [ time 129 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 20 (of 100) ]
         [ time 130 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 19 (of 100) ]
         [ time 131 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 18 (of 100) ]
         [ time 132 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 17 (of 100) ]
         [ time 133 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 16 (of 100) ]
         [ time 134 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 15 (of 100) ]
         [ time 135 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 14 (of 100) ]
         [ time 136 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 13 (of 100) ]
         [ time 137 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 12 (of 100) ]
         [ time 138 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 11 (of 100) ]
         [ time 139 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 10 (of 100) ]
         [ time 140 ] Run JOB 0 at PRIORITY 0 [ TICKS 9 ALLOT 1 TIME 9 (of 100) ]
         [ time 141 ] Run JOB 0 at PRIORITY 0 [ TICKS 8 ALLOT 1 TIME 8 (of 100) ]
         [ time 142 ] Run JOB 0 at PRIORITY 0 [ TICKS 7 ALLOT 1 TIME 7 (of 100) ]
         [ time 143 ] Run JOB 0 at PRIORITY 0 [ TICKS 6 ALLOT 1 TIME 6 (of 100) ]
         [ time 144 ] Run JOB 0 at PRIORITY 0 [ TICKS 5 ALLOT 1 TIME 5 (of 100) ]
         [ time 145 ] Run JOB 0 at PRIORITY 0 [ TICKS 4 ALLOT 1 TIME 4 (of 100) ]
         [ time 146 ] Run JOB 0 at PRIORITY 0 [ TICKS 3 ALLOT 1 TIME 3 (of 100) ]
         [ time 147 ] Run JOB 0 at PRIORITY 0 [ TICKS 2 ALLOT 1 TIME 2 (of 100) ]
         [ time 148 ] Run JOB 0 at PRIORITY 0 [ TICKS 1 ALLOT 1 TIME 1 (of 100) ]
         [ time 149 ] Run JOB 0 at PRIORITY 0 [ TICKS 0 ALLOT 1 TIME 0 (of 100) ]
         [ time 150 ] FINISHED JOB 0
         
         Final statistics:
           Job  0: startTime   0 - response   0 - turnaround 150
           Job  1: startTime   0 - response  10 - turnaround  64
         
           Avg  1: startTime n/a - response 5.00 - turnaround 107.00
      ```
      </details>
   </details>
   <br>

## Conclusions

Existen multiples casos a tener en cuenta cuando se desarrollan las reglas para la asignacion de tiempos de los procesos, y así mismo existen conjuntos de reglas que favorecen cierto tipo de procesos, por lo que es de vital importancia entender los procesos con los que se trabaja para utilizar un conjunto de reglas adecuadas que sean justas y permitan tiempos de respuesta y finalización óptimos.


### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
- [x] Sección con las conclusiones de los experimentos realizados.
