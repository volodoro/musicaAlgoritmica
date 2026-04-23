# cómo leer un texto

``` processing
# Welcome to Sonic Pi

texto = File.open ("C:/Users/Mediateca/Downloads/aleph.txt")
carpeta = "C:/Users/Mediateca/Downloads/ACEE361-003_material_docente_23-04-2026"

aleph = texto.read.chars


live_loop :lector do
  puts aleph.tick, tick(:marcador)
  look(:marcador)
  
  if look(:marcador) == 10 then
    
    use_octave 2
    
  end
  
  if look(:marcador) == 35 then
    
    
    use_octave -1
    
    
  end
  
  
  
  case aleph.look
  
  
  when "a"
    
    synth :fm, note: :a2, release: 0.1
    
    sample carpeta, "a", rate: rrand(0.8,1.2)
    
  when "b"
    synth :fm, note: :b2, release: 0.1
    
    
  when "c"
    
    synth :fm, note: :c3, release: 0.1
    
  when "d"
    
    synth :fm, note: :d3, release: 0.1
    
  when "e"
    
    synth :fm, note: :a2, release: 0.1
    sample carpeta, "e", rate: rrand(0.8,1.2)
    
  when "i"
    sample carpeta, "i", rate: rrand(0.8,1.2)
    
  when "o"
    sample carpeta, "o", rate: rrand(0.8,1.2)
    
  when "u"
    sample carpeta, "u", rate: rrand(0.8,1.2)
    
    
    
  else
    
    sample :drum_tom_lo_hard, amp: rrand(0.1, 0.8), pan: [-1,1].choose
    
  end
  
  
  sleep 0.500
  
  
end

```

## Para separar por caracteres

```processing
# Welcome to Sonic Pi

texto = File.open ("C:/Users/Mediateca/Downloads/aleph.txt")


aleph = texto.read.split(" ")

live_loop :lector2 do
  
  puts aleph.tick
  
  if aleph.look == "murió," then
    
    sample :perc_bell
    
  elsif aleph.look.end_with?("d")
    sample :perc_snap
    
  elsif aleph.look.start_with?("a")
    
    sample :perc_swash
    
  elsif
    
    sample :elec_bong
    
  else
    
    sample :elec_blip
    
  end
  
  
  sleep 0.5
  
end


```
# bongaso electrico

```processing
# Welcome to Sonic Pi

texto = File.open ("C:/Users/Mediateca/Downloads/aleph.txt")


aleph = texto.read.split(" ")

live_loop :lector2 do
  
  puts aleph.tick
  
    if aleph.look == "murió," then
  
      sample :perc_bell
  
    elsif aleph.look.end_with?("d")
      sample :perc_snap
  
    elsif aleph.look.start_with?("a")
  
      sample :perc_swash
  
    elsif aleph.look.include?("f")
  
      sample :elec_bong
  
    else
  
      sample :elec_blip
  
    end
  

  
  sleep 0.5
  
end


```
# Codigo tweets

```

require "csv"

data = CSV.read("C:/Users/Mediateca/Desktop/tweets.csv/tweets.csv")


live_loop :lectorDeTuits do
  tick
  
  puts data[look+1][1]
  
  
  
  if data[look+1][1].include?("China")
    
    sample :elec_bong, rate: rrand(0.8,1.2)
  end
  
  if  data[look+1][1].include?("Obama")
    
    sample :drum_cymbal_hard, pan: [-1,0,1].choose
  end
  
  
  if data[look+1][1].include?("Biden")
    
    sample :drum_cowbell, rate: rrand(0.8,1.2)
  end
  
  
  if data[look+1][1].include?("war")
    
    sample :drum_snare_hard, rate: rrand(0.8,1.2)
  end
  
  
  if data[look+1][1].include?("fraud")
    
    sample :perc_bell, rate: rrand(0.6,1.5), pan: rrand(-1,1)
  end
  
  if data[look+1][1].include?("Democrats")
    
    sample :elec_blip2, rate: rrand(0.6,1.5), pan: rrand(-1,1)
    
    
    
  end
  
  
  sleep 0.1
  
end

```
