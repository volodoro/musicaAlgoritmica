# Clase 02 (02.04.2026)

## Horario Memoria Ignacio Mariño: Jueves 10:00 - 11:30   


### Repaso efectos en BeepComp

### Para ADSR

Attacktime
peaktime
peaklevel
decaytime
sustainlevel

### Fall Effect

Es como un glissando hacia abajo

se escribe 

@1
Fallspeed=1200
fallwait=500

Se activa con la coma

ej: O4 B, GE B, GE B,G etc

### Risespeed glissando hacia arriba

risespeed=2400
riserange=200

se activa colocando un asterisco antes de la nota

ej: O4 *BGE *BGE BG etc.

### Beef Up!

Sean dice que es como una distorsión. Va desde 0 a 100.
Es como un clipping??

se anota:

BBEFUP=0 {NOTAS}
BEEFUP=25 {NOTAS}
ETC...

### RINGMOD

SE PUEDEN MODULAR DOS VOCES ENTRE ELLAS CON MODULACION DE ANILLO

# CÓMO PARTIR DESDE UN PUNTO EN ESPECÍFICO DE LA PIEZA

Yendo a cualquiera de las partes y colocando "%%".

ej: 

    O4 B, GE B, GE B,G etc
 %% O4 B, GE B, GE B,G etc
    O4 B, GE B, GE B,G etc
### LFO
PARÁMETROS

LFO = ON/OFF
LFOSPEED
LFORANGE
LFOWAIT

### Astro effect

Inspirado en el videojuego Astro Wars

ASTRO=NUMERO

## Bateria

@D

PINKNOISE ---> SONIDO MAS GRAVE PARA TODA LA BATERIA
KICKNOISE=PINK ---> SOLO EL BOMBO SE OPACA

### NIVEL DE RUIDO

LOS SONIDOS SON UNA COMBINACIÓN DE ONDA CUADRADA Y RUIDO, POR LO QUE SUS PARÁMETROS SE PUEDEN CAMBIAR

PARÁMETROS:

SQUARELEVEL=NUMERO
NOISELEVEL=NUMERO

ESTOS PARÁMETROS SE PUEDEN CAMBIAR EN CUALQUIER PARTE DE LA PIEZA ABARCANDO LAS NOTAS QUE ESTÁN DESPUÉS DEL COMANDO

### DRUM SOUND SHAPING

SNAREPITCH=NUMERO
KICKPITCH=NUMERO
RESETDRUMS ---> VUELVEN TODOS LOS PARÁMETROS AL DEFAULT

LARGO DE LAS NOTAS
DEFAULT:
KICK=40
SNARE=140
HH=20

PARÁMETROS:

KICKLENGHT=
SNARELENGHT=
HIHATLENGHT=

### DELAY

EXISTE UN DELAY STEREO QUE SE AÑADE A TODA LA PISTA

PARÁMETROS:

DELAY=ON/OFF
DELAYTIME=
DELAYLEVEL 50



































``` processing
@G
MASTERVOLUME=10
TEMPO=84
LOOP = OF
DELAY=OFFF

V1=8// MELODIA 10
V2= 7//BAJO 10
V3=4 //PIANO GRAVE  6
V4=4//PIANO MEDIO  6
V5=7 //PIANO AGUDO 10
V6=4

VD=15

//------------------BATERIA

@D

SNAREPITCH=50
SNARELENGTH=100

L16 {8:} :S~S S:SS //INTRO 

{{8 H~SH H~SH H~SH H~SH}} //(RIFF  Y MEL A) X2

H~SH H~SH H~SH H~SH 

H~:S S:S: S:HH S:HH     //FILL PARA PASAR A MEL B

//AQUI QUIERO HACER LA CAJA MAS AGUDA

{3 S:HH S:HH S:HH S:HH} 

H~:S S:S: S:HH S:HH  //FILL PARA PASAR A MEL C

{7 S:HH S:HH S:HH S:HH} 

{6 H~SH H~SH H~SH H~SH} //RIFF 
{8 S:HH S:HH S:HH S:HH} //OUTRO
 //ULTIMA VUELTA
:S:SS


@1 // MELODIA
  

//---------------- INTRO -------------------

LFO=ON
LFOSPEED=7
LFORANGE=30
LFOWAIT=180


ATTACKTIME=5
PEAKTIME=50
PEAKLEVEL=90
DECAYTIME=250
SUSTAINLEVEL=50
RELEASETIME=250

{4  O4  L16AAAA O5 C:E:
//CC1
L16EEEE       O4B   O5 :  DE} //CC2





// --------------- MELODIA A ----------------

L16 O4A:: O5  AO6 CECEE: L8 : O5  B O6  D //CC1
L16 O5A:: AO6 CEEEEG L8 :  O5  B  O6 L16  D C//C2
L16 O5 A~ O6 C O5 A 
O6 CEGF#FED C  O5B O6 DC O5B

L16 O5 A~ O6 C O5 A 
O6 CEGF#FED C  O5B O6 DC O5B

L16 O5 A~ O6 C O5 A 
O6 CEGF#FED C  O5B O6 DC O5B

//---------------- RIFF PRINCIPAL-----
A:: O4 A O5 C:E:
//CC1
L16EEEE       O4B   O5 :  DE} //CC2

{3  O4  L16AAAA O5 C:E:
//CC1
L16EEEE       O4B   O5 :  DE} //CC2

//--------------- MELODIA A' ------------------

L16 O4A:: O5  AO6 CECEE: L8 : O5  B O6  D //CC1
L16 O5A:: AO6 CEEEEG L8 :  O5  B  O6 L16  D C//CC2
L16 O5 A~ O6 C O5 A 
O6 CEGF#FED C  O5B O6 DC O5B

L16 O5 A~ O6 C O5 A 
O6 CEGF#FED C  O5B O6 DC O5B

L16 O5 A~ O6 C O5 A 
O6 CEGF#FED C  O5B O6 DC O5B
//-------------- MELODIA B
L16 O5 A:: O5 E A O6 CE~ O5 EG# O6 EE O5 B~ O6 D C O5 A~ O6 C

O5 E A O6 CE~ O5 EG# O6 EE O5 B~ O6 DC O5 A~ O6 C
O5 E A O6 CE~ O5 EG# O6 EE O5 B~ O6 DC O5 A~ O6 C

O5 E A O6 CE~ O5 EG# O6 EE O5 B~ O6 DC O5 A~ O6 :
// --------------- QUIEBRE

O5 A> C:< A:
//-------------- MELODIA C

{3 O5 GGGG  B~ O6  D O5A~AAAO6C~O5A~}
O5 GGGG  B: O6  D: O5A~:O6E
L16 A~E~

//------------- MELODIA D

L16 {3 GGG D G~D A~AA E A~E~}

GGG D G~D~ L4 A{7:}

//------------ RIFF PRINCIPAL

{4  O4  L16AAAA O5 C:E:
//CC1
L16EEEE       O4B   O5 :  DE} //CC2

//----------- OUTRO

L16 O4 A O5 A~ E A~ E A G  BO6 EO5 G : G#~ A

{6 L16 :  O5 A~ E A~ E A G  BO6 EO5 G : G#~ A}

L16 :  O5 A~ E A~ E A G  BO6 EO5 G : G#~ : 

: A: A L2 A 

//---------- FIN




  

@2// BAJO

//---------------- INTRO -------------------


L1: // SILENCIO PRIMER COMPAS 
{3  L8 O2 A: O3  CE O2  E: G#B} // 3 CC INTRO

// --------------- MELODIA A ----------------

{5 L8 O2 A: O3  CE O2  E: G#B} // 

//--------------- RIFF PRINCIPAL ------------

{4  L8 O2 A: O3  CE O2  E: G#B} // 3 CC INTRO

// --------------- MELODIA A' ----------------

{5 L8 O2 A: O3  CE O2  E: G#B} // 

//--------------- MELODIA B

{3  L16 O2 A~: O3  C~:  E~ O2 L8B O3 D O2 G# B }
    L16 O2 A~: O3  C~:  E~ O2 L8B O3 D O2 G# B A 

L8 :::

//--------------- MELODIA C

{3 L8O3 G ODO2BO3D L16 O2 A:O3AA~~E~}
L8O3 G ODO2BO3D L16 O2 L8A:::

//-------------- MELODIA D

{3 L8O2 G : B O3 D L16O2 A: O3 E   C~~ O2 A:} 
L8O2 G : B O3 D 

{6 L8 O2 A: O3  CE O2  E: G#B} // 3 CC INTRO

//------------- OUTRO

{7 L8 O2 A:O3 C E  G :  D C}
L8 O2 A:O3 C E  G :  D : L16 O3 : A:C L2O2 A 

//------------- FIN


//------------- VOCES PIANO------------------


@3 //PIANO VOZ GRAVE

LFO=ON
LFOSPEED=7
LFORANGE=20
LFOWAIT=150


ATTACKTIME=22
PEAKTIME=10
PEAKLEVEL=90
DECAYTIME=33
SUSTAINLEVEL=75
RELEASETIME=250

O4

L1: //CC1

L8 {{6 :E~::G#~:}} //13 CC(INTRO Y MEL A) X2


L8 {5 :E:E:G#:G#} //

//MELODIA B

L4 :: {3 G#~E~}

G#~E: //TRANSICION

//MELODIA C Y D

L8 {7 O4 :G:G :E:E} 

:G:G//FIN MELODIA D

//--------RIFF PRINCIPAL

{6 :E:::G#::}



//------------ PIANO VOZ MEDIA


@4 //PIANO VOZ MEDIA

O4

L1: //CC1

LFO=ON
LFOSPEED=7
LFORANGE=20
LFOWAIT=150

ATTACKTIME=22
PEAKTIME=10
PEAKLEVEL=90
DECAYTIME=33
SUSTAINLEVEL=75
RELEASETIME=250


L8 {{6 :A~::B~:}}//13 CC(INTRO Y MEL A) X2

L8 {5 :A:A:B:B} 

//MELODIA B


L4 ::{3 B~A~}

B~A://TRANSICION


//MELODIA C Y D
L8 {7 :B:B:A:A} 

:B:B
//---------- RIFF PRINCIPAL

{6 :A:::B::}

//------------ PIANO VOZ AGUDA


@5 //PIANO VOZ AGUDA
O4

L1: //CC1

LFO=ON
LFOSPEED=7
LFORANGE=20
LFOWAIT=150

ATTACKTIME=22
PEAKTIME=10
PEAKLEVEL=90
DECAYTIME=33
SUSTAINLEVEL=75
RELEASETIME=250

L8 {{6 :C~::D~:}}//13 CC(INTRO Y MEL A) X2

L8 {5 :C:C:D:D}//

//MELODIA B


L4:: {3 D~C~}

 D~C: //TRANSICION

//---------MELODIA C Y D

%%L8 {7 :D:D:C:C}


:D:D
//---------RIFF PRINCIPAL

{6 :C:::D::}


@6 //SUB
WAVEFORM=5



L1: 

ATTACKTIME=30
PEAKLEVEL=120
PEAKTIME=300
DECAYTIME=120
SUSTAINLEVEL=100
RELEASETIME=400

L16 O1 {{8 O1 A::: :::: E::: :::: }}

L16 O1 A::: :::: E::: :::: A::: ::::
 
L4{3 E~ A~} E~ A:

L4{7 G~ A~} G~ A:


 
```


