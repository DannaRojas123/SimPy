# Gasolinera
Una gasolinera tiene un tanque de 200 litros que se va vaciando conforme llegan autos aleatoriamente a cargar gasolina, usando una sola bomba. Cuando el nivel del tanque baja de cierto umbral (25%), se debe pedir un camión de reabastecimiento que tarda 30 minutos en llegar y recargar el tanque. El objetivo es simular si el tanque se queda sin gasolina antes de que llegue el camión, y decidir con qué anticipación conviene pedir el reabastecimiento.

## Codigo:
```
import simpy
import random

RANDOM_SEED = 42
CAPACIDAD_TANQUE = 200
NIVEL_UMBRAL = 25
VELOCIDAD_BOMBEO = 2
TIEMPO_REABASTECIMIENTO = 30
TIEMPO_ENTRE_AUTOS = 5

def auto(nombre, env, gasolinera, bomba):
    litros_necesarios = random.randint(10, 40)
    print(f"{nombre} llega en t={env.now:.1f}, necesita {litros_necesarios}L")
    with bomba.request() as req:
        yield req
        yield gasolinera.get(litros_necesarios)
        yield env.timeout(litros_necesarios / VELOCIDAD_BOMBEO)
        print(f"{nombre} termino de cargar en t={env.now:.1f}, tanque queda en {gasolinera.level:.0f}L")

def monitor_tanque(env, gasolinera):
    while True:
        if gasolinera.level / gasolinera.capacity * 100 < NIVEL_UMBRAL:
            print(f">> Tanque bajo ({gasolinera.level:.0f}L) en t={env.now:.1f}, pidiendo camion")
            yield env.process(reabastecer(env, gasolinera))
        else:
            yield env.timeout(5)

def reabastecer(env, gasolinera):
    yield env.timeout(TIEMPO_REABASTECIMIENTO)
    faltante = gasolinera.capacity - gasolinera.level
    yield gasolinera.put(faltante)
    print(f">> Camion reabastecio {faltante:.0f}L en t={env.now:.1f}")

def generador_autos(env, gasolinera, bomba):
    i = 0
    while True:
        yield env.timeout(random.randint(2, TIEMPO_ENTRE_AUTOS))
        i += 1
        env.process(auto(f"Auto {i}", env, gasolinera, bomba))

random.seed(RANDOM_SEED)
env = simpy.Environment()
bomba = simpy.Resource(env, capacity=1)
gasolinera = simpy.Container(env, CAPACIDAD_TANQUE, init=CAPACIDAD_TANQUE)
env.process(generador_autos(env, gasolinera, bomba))
env.process(monitor_tanque(env, gasolinera))
env.run(until=100)
```

## Ejecucion
```
Auto 1 llega en t=2.0, necesita 33L
Auto 2 llega en t=4.0, necesita 17L
Auto 3 llega en t=8.0, necesita 14L
Auto 4 llega en t=11.0, necesita 31L
Auto 5 llega en t=13.0, necesita 28L
Auto 6 llega en t=15.0, necesita 11L
Auto 1 termino de cargar en t=18.5, tanque queda en 167L
Auto 7 llega en t=20.0, necesita 12L
Auto 8 llega en t=22.0, necesita 17L
Auto 9 llega en t=25.0, necesita 27L
Auto 2 termino de cargar en t=27.0, tanque queda en 150L
Auto 10 llega en t=27.0, necesita 32L
Auto 11 llega en t=30.0, necesita 17L
Auto 3 termino de cargar en t=34.0, tanque queda en 136L
Auto 12 llega en t=35.0, necesita 28L
Auto 13 llega en t=40.0, necesita 35L
Auto 14 llega en t=44.0, necesita 34L
Auto 15 llega en t=46.0, necesita 32L
Auto 16 llega en t=49.0, necesita 20L
Auto 4 termino de cargar en t=49.5, tanque queda en 105L
Auto 17 llega en t=54.0, necesita 14L
Auto 18 llega en t=58.0, necesita 40L
Auto 19 llega en t=61.0, necesita 13L
Auto 5 termino de cargar en t=63.5, tanque queda en 77L
Auto 20 llega en t=65.0, necesita 22L
Auto 21 llega en t=67.0, necesita 21L
Auto 6 termino de cargar en t=69.0, tanque queda en 66L
Auto 22 llega en t=69.0, necesita 29L
Auto 23 llega en t=73.0, necesita 35L
Auto 7 termino de cargar en t=75.0, tanque queda en 54L
Auto 24 llega en t=77.0, necesita 33L
Auto 25 llega en t=79.0, necesita 27L
>> Tanque bajo (37L) en t=80.0, pidiendo camion
Auto 8 termino de cargar en t=83.5, tanque queda en 37L
Auto 26 llega en t=84.0, necesita 39L
Auto 27 llega en t=86.0, necesita 12L
Auto 28 llega en t=91.0, necesita 36L
Auto 29 llega en t=95.0, necesita 28L
Auto 9 termino de cargar en t=97.0, tanque queda en 10L
Auto 30 llega en t=99.0, necesita 32L
```
