# PROGRESO DE LA TAREA 2 HASTA EL 02/06

``` ruby
use_random_seed 888

set :comienzo_kalimba, true
set :tarros_iniciado, false

set :ultimo_indice_secuencia, nil
set :ultimo_indice_patron_kick, nil

# Variables de activación global
set :activar_sinte, false
set :activar_sinte_2, false
set :activar_kick, false
set :activar_movimiento_estereo, false
set :activar_sinte_mono, false
set :activar_sinte_stereo, false
set :activar_tonica_y_quinta, false

set :tocar_sinte_mono_serie, false

# Contador estructural
set :serie_global, 0

indices_sinte_2 = [1, 3, 5]
pasos_sinte_mono = [14, 17, 19, 21]

secuencias = [
  [:cs5, :fs5, :b4, :e5, :as4, :ds4, :gs4], # si mayor o sol# menor
  [:fs4, :b4, :e4, :a4, :ds4, :gs4, :cs4], # mi mayor o do# menor
  [:a4, :d5, :g4, :c5, :fs4, :b4, :e4],   # sol mayor o mi menor
  [:d4, :g4, :c4, :f4, :b3, :e3, :a3]      # do mayor o la menor
]

acordes = [
  [
    [:b3, :ds4, :fs4],        # si mayor
    [:b3, :ds4, :fs4, :as4],  # siMaj7
    [:gs3, :b3, :ds4]         # sol# menor
  ],
  
  [
    [:e4, :gs4, :b4],         # mi mayor
    [:e4, :gs4, :b4, :ds5],   # miMaj7
    [:cs4, :e4, :gs4]         # do# menor
  ],
  
  [
    [:g3, :b3, :d4],          # sol mayor
    [:g3, :b3, :d4, :fs4],    # solMaj7
    [:e4, :g4, :b4]           # mi menor
  ],
  
  [
    [:c4, :e4, :g4],          # do mayor
    [:c4, :e4, :g4, :b5],     # doMaj7
    [:a3, :c4, :e4]           # la menor
  ]
]

patronesKickAndBass = [
  [0, 1, 3, 5],       # patrón original
  [1, 3, 5, 6]        # segundo patrón
]

live_loop :director do
  
  sync :fin_serie
  
  serie = tick(:serie)
  set :serie_global, serie
  
  puts "===================="
  puts "SERIE GLOBAL:"
  puts serie
  puts "===================="
  
  case serie
  
  when 1
    
    set :activar_sinte, true
    set :activar_sinte_mono, true
    puts "Entra sinte principal y sinte mono"
    
  when 2
    
    set :activar_movimiento_estereo, true
    puts "Entra movimiento estéreo"
    
  when 3
    
    set :activar_sinte_stereo, true
    puts "Entra sinte stereo"
    
  when 4
    
    set :activar_tonica_y_quinta, true
    puts "Entra tónica y quinta"
    
  when 6
    
    set :activar_sinte_2, true
    puts "Entra sinte 2"
    
  when 8
    
    set :activar_kick, true
    puts "Entra kick y bajo"
    
  when 11
    
    puts "Cambio de atmósfera"
    
  end
  
end

live_loop :tarros do
  
  # Pre-roll inicial: retrasa el inicio global sin desfasar nada,
  # porque el director espera :fin_serie.
  if !get(:tarros_iniciado)
    set :tarros_iniciado, true
    sleep 1
  end
  
  use_synth :kalimba
  
  if get(:comienzo_kalimba)
    
    ultimo_indice = get(:ultimo_indice_secuencia)
    opciones = (0...secuencias.length).to_a
    
    if ultimo_indice != nil
      opciones = opciones - [ultimo_indice]
    end
    
    indice = opciones.choose
    secuencia = secuencias[indice]
    
    set :ultimo_indice_secuencia, indice
    
    grupo_acordes = acordes[indice]
    indice_acorde = rrand_i(0, grupo_acordes.length - 1)
    acorde = grupo_acordes[indice_acorde]
    
    set :acorde_actual, acorde
    
    fundamental_bajo = acorde[0]
    fundamental_midi = note(fundamental_bajo)
    
    serie = get(:serie_global)
    
    if serie < 4
      set :tocar_sinte_mono_serie, true
    else
      set :tocar_sinte_mono_serie, one_in(2)
    end
    
    # =========================
    # Elegir patrón kick/bajo sin repetición
    # =========================
    
    ultimo_patron = get(:ultimo_indice_patron_kick)
    opciones_patron = (0...patronesKickAndBass.length).to_a
    
    if ultimo_patron != nil
      opciones_patron = opciones_patron - [ultimo_patron]
    end
    
    indice_patron = opciones_patron.choose
    patronKickActual = patronesKickAndBass[indice_patron]
    
    set :ultimo_indice_patron_kick, indice_patron
    
    puts "Secuencia elegida:"
    puts secuencia
    
    puts "Acorde elegido:"
    puts acorde
    
    puts "Patrón kick elegido:"
    puts patronKickActual
    
    cue :bloque_kalimba,
      indice: indice,
      indice_acorde: indice_acorde
    
    if get(:activar_movimiento_estereo)
      cue :movimiento_estereo,
        fundamental_midi: fundamental_midi
    end
    
    4.times do |repeticion|
      
      secuencia.each_with_index do |nota, i|
        
        paso_stereo = repeticion * secuencia.length + i
        
        cue :tick_stereo,
          paso: paso_stereo,
          fundamental: fundamental_midi
        
        if pasos_sinte_mono.include?(paso_stereo)
          cue :marca_sinte_mono,
            paso: paso_stereo
        end
        
        if get(:activar_kick)
          if patronKickActual.include?(i)
            cue :triggerKick,
              indiceTrigger: i,
              fundamental_midi: fundamental_midi
          end
        end
        
        if get(:activar_sinte_2)
          if indices_sinte_2.include?(i)
            cue :nota_sinte_2,
              nota: note(nota)
          end
        end
        
        play nota,
          release: 0.75
        
        play nota + 12,
          amp: 1,
          release: 0.75
        
        sleep 0.25
        
      end
      
    end
    
    cue :fin_serie
    
  else
    
    sleep 0.25
    
  end
  
end

live_loop :sinte do
  
  datos = sync :bloque_kalimba
  
  if get(:activar_sinte)
    
    use_synth :saw
    
    indice = datos[:indice]
    indice_acorde = datos[:indice_acorde]
    
    grupo_acordes = acordes[indice]
    acorde = grupo_acordes[indice_acorde]
    
    with_fx :echo, phase: 0.5 do
      with_fx :reverb, mix: 0.9, room: 0.9 do
        
        play acorde,
          amp: 0.2,
          attack: 1.3,
          decay: 0.3,
          sustain: 2,
          release: 3.6,
          cutoff: 85
        
      end
    end
    
  end
  
end

live_loop :sinte_estereo do
  
  datos = sync :tick_stereo
  
  if get(:activar_sinte_stereo)
    
    use_synth :fm
    use_octave 1
    
    acorde = get(:acorde_actual)
    
    tonica = note(acorde[0])
    tercera = note(acorde[1])
    
    paso = datos[:paso]
    
    total_pasos = 28
    ultimo_paso = total_pasos - 1
    
    peak = 18
    curva_release = 1.5
    
    if paso <= peak
      amp_env = paso.to_f / peak
    else
      fade_out = (ultimo_paso - paso).to_f / (ultimo_paso - peak)
      amp_env = fade_out ** curva_release
    end
    
    amp_env = [[amp_env, 0].max, 1].min
    
    amp_general = 1.0
    
    with_fx :reverb, mix: 0.5, room: 0.96 do
      
      play tonica,
        pan: -1,
        amp: 0.1 * amp_env * amp_general,
        release: 0.15,
        cutoff: 90
      
      play tonica + 12,
        pan: -1,
        amp: 0.1 * amp_env * amp_general,
        release: 0.15,
        cutoff: 90
      
      play tercera,
        pan: 1,
        amp: 0.1 * amp_env * amp_general,
        release: 0.15,
        cutoff: 90
      
      play tercera + 12,
        pan: 1,
        amp: 0.1 * amp_env * amp_general,
        release: 0.15,
        cutoff: 95
      
    end
    
  end
  
  use_octave 0
  
end

live_loop :sinte_mono do
  
  sync :marca_sinte_mono
  
  if get(:activar_sinte_mono) and get(:tocar_sinte_mono_serie)
    
    acorde = get(:acorde_actual)
    
    tonica = note(acorde[0])
    tercera = note(acorde[1])
    
    paneo = rrand(-1, 1)
    
    use_synth :chipbass
    
    with_fx :reverb, mix: 0.75, room: 0.8 do
      with_fx :echo, mix: 0.2 do
        
        play [tonica,
              tercera,
              tonica + 12,
              tercera + 12],
          amp: 0.15,
          attack: 0,
          release: 0.5,
          pan: paneo,
          cutoff: 60
        
      end
    end
    
  end
  
end

live_loop :sinte_2 do
  
  datos = sync :nota_sinte_2
  
  use_synth :prophet
  use_octave 1
  
  nota = datos[:nota]
  
  with_fx :reverb do
    with_fx :hpf, cutoff: 65 do
      
      play nota,
        amp: 0.05,
        cutoff: 95,
        release: 1.5
      
    end
  end
  
  use_octave 0
  
end

live_loop :kickAndBass do
  
  datos = sync :triggerKick
  
  indiceTrigger = datos[:indiceTrigger]
  fundamental_midi = datos[:fundamental_midi]
  
  sample :bd_haus,
    cutoff: 79,
    amp: 0.75
  
  use_synth :tb303
  
  play fundamental_midi - 24,
    amp: 0.085,
    release: 0.6,
    cutoff: 78,
    res: 0.85
  
end

live_loop :tonica_y_quinta do
  
  datos = sync :tick_stereo
  
  if get(:activar_tonica_y_quinta)
    
    fundamental = datos[:fundamental]
    quinta = fundamental + 7
    
    use_synth :blade
    
    with_fx :reverb, mix: 0.35 do
      
      play fundamental,
        amp: 0.08,
        release: 0.2,
        cutoff: 80,
        pan: -1
      
      play quinta,
        amp: 0.08,
        release: 0.2,
        cutoff: 90,
        pan: 1
      
    end
    
  end
  
end

direccion = 1

live_loop :movimiento_estereo do
  
  datos = sync :movimiento_estereo
  
  fundamental = datos[:fundamental_midi]
  
  with_fx :reverb, mix: 0.6 do
    
    with_fx :slicer,
      phase: 0.125,
      mix: 0.5,
      smooth: 0.2,
      wave: 1 do
      
      with_fx :slicer,
        phase: 0.25,
        smooth: 0.1,
        wave: 1 do
        
        inicio = direccion == 1 ? -1 : 1
        final  = direccion == 1 ? 1 : -1
        
        use_octave -1
        
        s = synth :mod_fm,
          note: fundamental,
          amp: 0.1,
          attack: 0.75,
          release: 8,
          pan: inicio,
          pan_slide: 5
        
        use_octave 1
        
        s1 = synth :pretty_bell,
          note: fundamental + 7,
          amp: 0.1,
          attack: 0.25,
          release: 8,
          pan: inicio,
          pan_slide: 5
        
        control s, pan: final
        control s1, pan: final
        
        direccion = direccion * -1
        
      end
    end
  end

```
  
  use_octave 0
  
end
