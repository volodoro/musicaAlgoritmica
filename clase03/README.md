# Clase 03, Intro a Sonic Pi

video para reemplazar partes de pájaros que no se ven tan bien en el video de la tarea 1:
https://www.youtube.com/watch?v=bbIXJNtcH8s

## Herramientas de Síntesis en Sonic pi

```
#play 60 nota MIDI o tambien puede ser c4 o una frecuencia
10.times do #sean dice que esto es una especie de ciclo for
  
  play [:c4, :d4, :e4].choose, amp: 1, pan: [-1,1].tick #amplitud entre o y 1
  sleep 1 #iterar en ciclos de 1 segundo
  
end

#el tick es una especie de indice pero que funciona como
#un array de anillo, es decir que da vueltas sobre si mismo y
#nunca se sale del indice del arreglo
```

### cómo usar una escala

```
live_loop :fantasia do
  
  synth :fm, note: (scale :e3,:minor_pentatonic)[indice en el array],  release: 0.09, amp: rand
  sleep 0.25
  
end
```

### estructura if

```
live_loop :fantasia do
  
  a = [1,0,1,0].tick
  puts a
  
  if a == 1 then
    
    
    synth :tb303, note: (scale :d3,:minor_pentatonic).choose,  release: 0.1
    
  else
    sample :perc_bell, amp: 0.5
    
    
  end
  
  sleep 0.25
```

### imitación de "piano phase" de steve reich (pero usando tiempo)

```
lista = [:E4, :Fs4, :B4, :Cs5, :D5, :Fs, :E4, :Cs5, :B4, :Fs4, :D5, :Cs5]
s = :piano

live_loop :lento do
  
  synth s, note: lista.tick, pan: -1, release: 0.2
  sleep 0.300
end

live_loop :rapido do
  
  synth s, note: lista.tick, pan: 1, release: 0.2
  sleep 0.295
  
end
```

### imitación de "piano phase" de steve reich (real)

```
lista = [:E4, :Fs4, :B4, :Cs5, :D5, :Fs, :E4, :Cs5, :B4, :Fs4, :D5, :Cs5]
s = :piano
n = 0
use_bpm = 120

live_loop :playerUno do
  
  synth s, note: lista.tick, pan: 0, release: 0.2
  sleep 0.300
end



live_loop :playerDos do
  
  8.times do #leer compás normal
    12.times do
      
      synth s, note: lista.rotate(n).tick, pan: 0, release: 0.2
      sleep 0.300
      
    end
  end
  n = n + 1
end
```
### cómo desfasar arreglos
```
# Welcome to Sonic Pi
lista = [1,2,3,4]

puts lista.rotate(0)

puts lista.rotate(1) #estoy desfasando por la cantidad de elementos del paréntesis
```

# ARTE GENERATIVO 

Se denomina generativo o procedural al arte que parcialmente o en su totalidad ha sido creado usando un sistema autónomo.

• B. S. Johnson ---> The unfortunates
Publica en 27 hojas separadas en una caja excepto la primera y la última página que están pegadas.

• Hans Haacke ---> Condensation Cube

La escritura automatica o el fluir de conciencia es el proceso o resultado de la escritura que no proviene de los pensamientos conscientes.

• Cadaver Exquisito ---> Técnica usada por los surrealistas en 1925, y se basa en un juego de consecuencias.

• Hubert Duprat ---> Larvas de libélula en un acuario

# Cómo usar Samples

```
with_fx :reverb do
  
  
  live_loop :audioLindo do
    
    sample :perc_bell, rate: rrand(-1,1), amp: rand, pan: rrand(-1,1)
    
    sleep rrand(0.1,1)
    
  end
end
```

# se pueden plantear las estructuras if al revés

```
load_sample clap

mano = [1,1,1,0,1,1,0,1,0,1,1,0]

live_loop :playerUno do
  
  sample clap if mano.tick == 1
  sleep 0.25
  
  
end
```


