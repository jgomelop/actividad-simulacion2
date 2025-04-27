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
   Coloque aqui su respuerta
   </details>
   <br>

4. Craft a workload with two jobs and scheduler parameters so that one job takes advantage of the older Rules 4a and 4b (turned on
with the -S flag) to game the scheduler and obtain 99% of the CPU over a particular time interval.

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

5. Given a system with a quantum length of 10 ms in its highest queue, how often would you have to boost jobs back to the highest priority level (with the `-B` flag) in order to guarantee that a single longrunning (and potentially-starving) job gets at least 5% of the CPU?

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

6. One question that arises in scheduling is which end of a queue to add a job that just finished I/O; the -I flag changes this behavior
for this scheduling simulator. Play around with some workloads and see if you can see the effect of this flag.

   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

## Conclusions

Coloque aqui las conclusiones...


### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
- [x] Sección con las conclusiones de los experimentos realizados.
