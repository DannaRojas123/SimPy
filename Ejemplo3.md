# Taller con fallas
Una máquina fabrica piezas que tardan 10 minutos cada una, pero puede sufrir fallas aleatorias en cualquier momento (incluso a medio fabricar una pieza), lo que obliga a repararla durante 15 minutos antes de continuar. El objetivo es medir cuántas piezas se logran terminar en un turno y cuántas veces el proceso se ve interrumpido por fallas, para estimar el impacto real del mantenimiento no planeado en la producción.

## Codigo
```
import simpy
import random

RANDOM_SEED = 42
TIEMPO_PIEZA = 10
PROB_FALLA_POR_PIEZA = 0.2
TIEMPO_REPARACION = 15

piezas_terminadas = 0
piezas_interrumpidas = 0

def maquina(env, taller):
    global piezas_terminadas, piezas_interrumpidas
    while True:
        tiempo_restante = TIEMPO_PIEZA
        while tiempo_restante > 0:
            inicio = env.now
            with taller.request(priority=1) as req:
                yield req
                try:
                    yield env.timeout(tiempo_restante)
                    tiempo_restante = 0
                except simpy.Interrupt:
                    tiempo_restante -= (env.now - inicio)
                    piezas_interrumpidas += 1
                    print(f"Pieza interrumpida en t={env.now:.1f}, faltan {tiempo_restante:.1f} min")
        piezas_terminadas += 1
        print(f"Pieza #{piezas_terminadas} terminada en t={env.now:.1f}")

def generador_fallas(env, taller):
    while True:
        yield env.timeout(random.expovariate(1.0 / (TIEMPO_PIEZA / PROB_FALLA_POR_PIEZA)))
        with taller.request(priority=0) as req:
            yield req
            print(f"!! Falla detectada en t={env.now:.1f}, reparando...")
            yield env.timeout(TIEMPO_REPARACION)
            print(f"!! Reparacion terminada en t={env.now:.1f}")

random.seed(RANDOM_SEED)
env = simpy.Environment()
taller = simpy.PreemptiveResource(env, capacity=1)
env.process(maquina(env, taller))
env.process(generador_fallas(env, taller))
env.run(until=150)

print(f"\nPiezas terminadas: {piezas_terminadas}")
print(f"Interrupciones por falla: {piezas_interrumpidas}")
```

## Ejecucion
```
Pieza #1 terminada en t=10.0
Pieza #2 terminada en t=20.0
Pieza #3 terminada en t=30.0
Pieza #4 terminada en t=40.0
Pieza #5 terminada en t=50.0
Pieza interrumpida en t=51.0, faltan 9.0 min
!! Falla detectada en t=51.0, reparando...
!! Reparacion terminada en t=66.0
Pieza interrumpida en t=67.3, faltan -7.3 min
Pieza #6 terminada en t=67.3
!! Falla detectada en t=67.3, reparando...
!! Reparacion terminada en t=82.3
Pieza #7 terminada en t=92.3
Pieza interrumpida en t=98.4, faltan 3.9 min
!! Falla detectada en t=98.4, reparando...
!! Reparacion terminada en t=113.4
Pieza #8 terminada en t=117.3
Pieza interrumpida en t=126.0, faltan 1.3 min
!! Falla detectada en t=126.0, reparando...
!! Reparacion terminada en t=141.0
Pieza #9 terminada en t=142.3

Piezas terminadas: 9
Interrupciones por falla: 4
```

## Puntos clave
#### 1. simpy.PreemptiveResource(env, capacity=1):
A diferencia de un Resource normal, este permite que un proceso de mayor prioridad interrumpa a uno que ya está corriendo, en vez de esperar su turno.
request(priority=0) vs request(priority=1): las fallas piden el recurso con prioridad 0 (más alta = número menor), así que le "quitan" la máquina a la fabricación de piezas (prioridad 1) aunque esté a medias.
try / except simpy.Interrupt: así el código de la pieza detecta cuando fue interrumpida a medio proceso, calcula cuánto tiempo de trabajo le faltaba, y retoma justo ahí después de la reparación — en vez de perder todo el progreso.
tiempo_restante -= (env.now - inicio): es lo que permite que el trabajo parcial no se pierda; simula el escenario realista donde una pieza a medio hacer sigue "a medio hacer" después de arreglar la máquina.
