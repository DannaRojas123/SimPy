# Tienda de 2 cajeros
Se está resolviendo un problema clásico de teoría de colas: dado un banco al que llegan clientes de forma aleatoria (en promedio cada 5 minutos) y solo hay 2 cajeros disponibles para atenderlos (cada atención toma en promedio 8 minutos), la simulación busca estimar cuánto tiempo espera un cliente en fila antes de ser atendido, permitiendo así evaluar si la capacidad actual (2 cajeros) es suficiente para mantener tiempos de espera razonables, o si haría falta agregar más cajeros para reducir la congestión.

## Codigo:
```
import simpy
import random

RANDOM_SEED = 42
NUM_CAJEROS = 2
TIEMPO_LLEGADA_PROMEDIO = 5
TIEMPO_ATENCION_PROMEDIO = 8
TIEMPO_SIMULACION = 120

tiempos_espera = []

def cliente(env, nombre, banco):
    llegada = env.now
    with banco.request() as req:
        yield req
        espera = env.now - llegada
        tiempos_espera.append(espera)
        print(f"{nombre} espero {espera:.2f} min, atendido en t={env.now:.2f}")
        tiempo_atencion = random.expovariate(1.0 / TIEMPO_ATENCION_PROMEDIO)
        yield env.timeout(tiempo_atencion)
        print(f"{nombre} termino en t={env.now:.2f}")

def generador_clientes(env, banco):
    i = 0
    while True:
        yield env.timeout(random.expovariate(1.0 / TIEMPO_LLEGADA_PROMEDIO))
        i += 1
        env.process(cliente(env, f"Cliente {i}", banco))

random.seed(RANDOM_SEED)
env = simpy.Environment()
banco = simpy.Resource(env, capacity=NUM_CAJEROS)
env.process(generador_clientes(env, banco))
env.run(until=TIEMPO_SIMULACION)

print(f"\nClientes atendidos: {len(tiempos_espera)}")
print(f"Espera promedio: {sum(tiempos_espera)/len(tiempos_espera):.2f} min")
```

## Ejecucion
```
Cliente 1 espero 0.00 min, atendido en t=5.10
Cliente 2 espero 0.00 min, atendido en t=5.23
Cliente 1 termino en t=7.67
Cliente 3 espero 1.18 min, atendido en t=7.67
Cliente 2 termino en t=15.90
Cliente 4 espero 3.76 min, atendido en t=15.90
Cliente 4 termino en t=21.53
Cliente 5 espero 8.94 min, atendido en t=21.53
Cliente 3 termino en t=25.49
Cliente 6 espero 10.16 min, atendido en t=25.49
Cliente 5 termino en t=27.83
Cliente 7 espero 12.34 min, atendido en t=27.83
Cliente 7 termino en t=27.88
Cliente 8 espero 11.16 min, atendido en t=27.88
Cliente 6 termino en t=38.75
Cliente 9 espero 21.90 min, atendido en t=38.75
Cliente 8 termino en t=40.99
Cliente 10 espero 23.03 min, atendido en t=40.99
Cliente 10 termino en t=41.77
Cliente 11 espero 18.56 min, atendido en t=41.77
Cliente 9 termino en t=42.04
Cliente 12 espero 17.59 min, atendido en t=42.04
Cliente 11 termino en t=42.58
Cliente 13 espero 13.68 min, atendido en t=42.58
Cliente 13 termino en t=49.99
Cliente 14 espero 15.10 min, atendido en t=49.99
Cliente 12 termino en t=57.08
Cliente 15 espero 20.11 min, atendido en t=57.08
Cliente 14 termino en t=63.15
Cliente 16 espero 25.34 min, atendido en t=63.15
Cliente 15 termino en t=63.23
Cliente 17 espero 9.66 min, atendido en t=63.23
Cliente 16 termino en t=66.96
Cliente 18 espero 6.85 min, atendido en t=66.96
Cliente 17 termino en t=69.65
Cliente 19 espero 0.00 min, atendido en t=78.19
Cliente 18 termino en t=81.11
Cliente 20 espero 0.00 min, atendido en t=83.01
Cliente 20 termino en t=92.77
Cliente 21 espero 5.45 min, atendido en t=92.77
Cliente 19 termino en t=94.02
Cliente 22 espero 6.47 min, atendido en t=94.02
Cliente 21 termino en t=95.37
Cliente 23 espero 6.53 min, atendido en t=95.37
Cliente 22 termino en t=97.65
Cliente 24 espero 7.10 min, atendido en t=97.65
Cliente 23 termino en t=99.07
Cliente 25 espero 8.10 min, atendido en t=99.07
Cliente 24 termino en t=99.53
Cliente 26 espero 7.24 min, atendido en t=99.53
Cliente 26 termino en t=107.05
Cliente 27 espero 14.22 min, atendido en t=107.05
Cliente 27 termino en t=108.47
Cliente 28 espero 10.60 min, atendido en t=108.47
Cliente 28 termino en t=112.29
Cliente 29 espero 12.86 min, atendido en t=112.29

Clientes atendidos: 29
Espera promedio: 10.27 min
```
SimPy simula eventos discretos: en vez de avanzar el tiempo segundo a segundo, salta directo al siguiente evento importante (una llegada, el fin de una atención, etc). El env es el reloj/motor que coordina todo.

## Puntos clave
#### 1. simpy.Resource(env, capacity=2)
Representa los 2 cajeros. Es lo que limita cuántos clientes pueden ser atendidos al mismo tiempo, la pieza central que genera la fila.

#### 2. banco.request() + yield req
Así un cliente pide un cajero. Si ambos están ocupados, esta línea pausa al cliente hasta que se libere uno. Esa pausa es literalmente la espera en fila.

#### 3. env.timeout(...)
Se usa dos veces con propósitos distintos:

- En generador_clientes: controla cuánto tiempo pasa entre llegadas de clientes.
- En cliente: controla cuánto dura la atención una vez que el cliente tiene cajero.

#### 4. random.expovariate(1/promedio)
Genera los tiempos aleatorios (llegadas y atenciones) usando distribución exponencial, la forma estándar de modelar "tiempo entre eventos" en teoría de colas.

#### 5. env.process(...)
Lanza cada cliente como un proceso independiente que corre en paralelo con los demás, todos compitiendo por los mismos 2 cajeros. Sin esto no habría concurrencia.

#### 6. env.run(until=120)
El motor que avanza el reloj simulado evento por evento (no en tiempo real) hasta el minuto 120.

El Resource crea la restricción de capacidad, los yield crean las pausas (espera y atención), y env.process permite que múltiples clientes existan al mismo tiempo compitiendo por ese recurso limitado.
