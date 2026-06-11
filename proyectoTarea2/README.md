# VERDION FINAAL

```ruby
use_random_seed 56765678987678

use_debug false
use_sched_ahead_time 1

set :comienzo_kalimba, true
set :tarros_iniciado, false

set :ultimo_indice_secuencia, nil
set :ultimo_indice_patron_kick, nil

set :activar_sinte, false
set :activar_sinte_2, false
set :activar_kick, false
set :activar_movimiento_estereo, false
set :activar_sinte_mono, false
set :activar_sinte_stereo, false
set :activar_tonica_y_quinta, false
set :activar_sinte_2_complemento, false

set :tocar_sinte_mono_serie, false
set :modo_secuencias, :primeras
set :modo_kick_bajo, :patrones
set :modo_sinte_2, :fijo
set :modo_movimiento_estereo, :alternado
set :tocar_movimiento_estereo_serie, true

set :activar_bajo_corcheas_azar, false
set :bajo_corcheas_serie, false

set :panear_sintes_2, false
set :sinte_2_release, 1.5
set :sinte_2_complemento_release, 1.5
set :activar_hihat_contratiempo, false


set :activar_secuencias_espejo, false

set :activar_sustraccion_kalimba, false
set :indices_kalimba_silenciados, []

set :serie_global, 0

indices_sinte_2 = [1, 3, 5]
pasos_sinte_mono = [14, 17, 19, 21]

secuencias = [
  [:cs5, :fs5, :b4, :e5, :as4, :ds4, :gs4], # 0 - si mayor o sol# menor
  [:fs4, :b4, :e4, :a4, :ds4, :gs4, :cs4], # 1 - mi mayor o do# menor
  [:a4, :d5, :g4, :c5, :fs4, :b4, :e4],   # 2 - sol mayor o mi menor
  [:d4, :g4, :c4, :f4, :b3, :e3, :a3],     # 3 - do mayor o la menor
  
  [:b4, :cs5, :gs5, :e5, :fs5, :as5, :ds5], # 4 - si mayor o sol# menor
  [:e4, :fs4, :cs5, :a4, :b4, :ds5, :gs4], # 5 - mi mayor o do# menor
  [:g4, :a4, :e5, :c5, :d5, :fs5, :b4],    # 6 - sol mayor o mi menor
  [:c4, :d4, :a4, :f4, :g4, :b4, :e4]      # 7 - do mayor o la menor
]

acordes = [
  [
    [:b3, :ds4, :fs4],        # si mayor
    [:b3, :ds4, :fs4, :gs4],        # si mayor6
    [:b3, :ds4, :fs4, :as4],  # siMaj7
    [:gs3, :b3, :ds4],         # sol# menor
    [:gs3, :b3, :fs4],         # sol# menor 7
    
  ],
  
  [
    [:e4, :gs4, :b4],         # mi mayor
    [:e4, :gs4, :b4, :cs5],         # mi mayor6
    [:e4, :gs4, :b4, :ds5],   # miMaj7
    [:cs4, :e4, :gs4],         # do# menor
    [:cs4, :e4, :bf4],         # do# menor 7
    
    
  ],
  
  [
    [:g3, :b3, :d4],          # sol mayor
    [:g3, :b3, :d4, :e4],          # sol mayor6
    [:g3, :b3, :d4, :fs4],    # solMaj7
    [:e4, :g4, :b4],          # mi menor
    [:e4, :g4, :b4, :d5],           # mi menor7
    
  ],
  
  [
    [:c4, :e4, :g4],          # do mayor
    [:c4, :e4, :g4, :a4],          # do mayor6
    [:c4, :e4, :g4, :b5],     # doMaj7
    [:a3, :c4, :e4],           # la menor
    [:a3, :c4, :e4, :g4],           # la menor7
    
  ]
]

patronesKickAndBass = [
  [0, 1, 3, 5],       # patrón original
  [1, 3, 5, 6],        # segundo patrón
  [0, 1, 3, 6]
]

live_loop :director do
  
  sync :fin_serie
  
  serie = tick(:serie)
  set :serie_global, serie
  
  puts "SERIE GLOBAL:"
  puts serie
  
  case serie
  when 1
    set :activar_sinte, true
    
    
  when 2
    set :activar_sinte_mono, true
    
  when 4
    set :activar_movimiento_estereo, true
    
    
  when 6
    set :activar_sinte_stereo, true
    
    
  when 7
    set :activar_tonica_y_quinta, true
    set :activar_sinte_2, true
    
  when 8
    set :activar_kick, true
    
  when 12
    set :modo_secuencias, :segundas
    set :activar_sinte_stereo, false
    set :activar_kick, false
    set :activar_sinte, false
    set :activar_sinte_2, false
    set :activar_sinte_mono, false
    set :activar_tonica_y_quinta, false
    
    
  when 13
    
    set :activar_sinte_stereo, true
    
    
    
  when 14
    set :activar_kick, true
    set :activar_sinte_mono, true
    set :modo_sinte_2, :aleatorio
    set :modo_movimiento_estereo, :aleatorio
    
    
    
    
  when 16
    set :modo_kick_bajo, :negras
    set :activar_sinte_2_complemento, true
    set :activar_sinte_2, true
    set :panear_sintes_2, true
    set :activar_sinte, true
    set :sinte_2_release, 0.9
    set :sinte_2_complemento_release, 0.65
    ##| puts "Kick/bajo a negras + complemento sinte 2"
    set :activar_secuencias_espejo, true
    ##| puts "Se activan secuencias espejo"
    
    
  when 18
    set :activar_bajo_corcheas_azar, true
    set :activar_tonica_y_quinta, false
    set :activar_hihat_contratiempo, true
    
  when 22
    
    set :activar_sustraccion_kalimba, true
    set :activar_bajo_corcheas_azar, false
    
    
  when 23
    
    set :activar_tonica_y_quinta, true
    set :activar_hihat_contratiempo, false
    
    
  when 24
    
    set :activar_sinte_mono, false
    set :activar_kick, false
    
  when 25
    
    set :activar_sinte, false
    set :activar_movimiento_estereo, false
    
    
  when 27
    
    
    set :activar_tonica_y_quinta, false
    
  when 28
    set :activar_sinte_stereo, false
    
    
    
    
  end
  
end

live_loop :tarros do
  
  if !get(:tarros_iniciado)
    set :tarros_iniciado, true
    sleep 1
  end
  
  use_synth :kalimba
  
  if get(:comienzo_kalimba)
    
    ultimo_indice = get(:ultimo_indice_secuencia)
    modo_secuencias = get(:modo_secuencias)
    
    case modo_secuencias
    when :primeras
      opciones = [0, 1, 2, 3]
    when :segundas
      opciones = [4, 5, 6, 7]
    when :todas
      opciones = (0...secuencias.length).to_a
    else
      opciones = [0, 1, 2, 3]
    end
    
    if ultimo_indice != nil
      opciones = opciones - [ultimo_indice]
    end
    
    indice = opciones.choose
    secuencia_original = secuencias[indice]
    
    if get(:activar_secuencias_espejo) and one_in(2)
      secuencia = secuencia_original.reverse
      secuencia_espejo = true
    else
      secuencia = secuencia_original
      secuencia_espejo = false
    end
    
    if get(:activar_sustraccion_kalimba)
      
      silenciados = get(:indices_kalimba_silenciados)
      disponibles = (0...secuencia.length).to_a - silenciados
      
      if disponibles.length > 0
        nuevo_silencio = disponibles.choose
        silenciados = silenciados + [nuevo_silencio]
        set :indices_kalimba_silenciados, silenciados
      end
      
    else
      
      set :indices_kalimba_silenciados, []
      
    end
    
    
    
    
    set :ultimo_indice_secuencia, indice
    
    
    indice_armonico = indice % 4
    grupo_acordes = acordes[indice_armonico]
    indice_acorde = rrand_i(0, grupo_acordes.length - 1)
    acorde = grupo_acordes[indice_acorde]
    set :acorde_actual, acorde
    
    fundamental_midi = note(acorde[0])
    
    if get(:modo_kick_bajo) == :negras and get(:activar_bajo_corcheas_azar)
      set :bajo_corcheas_serie, one_in(2)
    else
      set :bajo_corcheas_serie, false
    end
    
    serie = get(:serie_global)
    
    if serie < 8
      set :tocar_sinte_mono_serie, true
    else
      set :tocar_sinte_mono_serie, one_in(2)
    end
    
    ultimo_patron = get(:ultimo_indice_patron_kick)
    opciones_patron = (0...patronesKickAndBass.length).to_a
    
    if ultimo_patron != nil
      opciones_patron = opciones_patron - [ultimo_patron]
    end
    
    indice_patron = opciones_patron.choose
    patronKickActual = patronesKickAndBass[indice_patron]
    set :ultimo_indice_patron_kick, indice_patron
    
    modo_sinte_2 = get(:modo_sinte_2)
    
    if modo_sinte_2 == :aleatorio
      indices_sinte_2_actuales = (0...secuencia.length).to_a.shuffle.take(3)
    else
      indices_sinte_2_actuales = indices_sinte_2
    end
    
    indices_sinte_2_complemento = (0...secuencia.length).to_a - indices_sinte_2_actuales
    
    
    cue :bloque_kalimba,
      indice: indice_armonico,
      indice_acorde: indice_acorde
    
    if get(:activar_movimiento_estereo)
      
      modo_mov = get(:modo_movimiento_estereo)
      
      if modo_mov == :aleatorio
        if one_in(2)
          cue :movimiento_estereo,
            fundamental_midi: fundamental_midi,
            pan_inicio: rrand(-1, 1),
            pan_final: rrand(-1, 1)
        end
      else
        cue :movimiento_estereo,
          fundamental_midi: fundamental_midi
      end
      
    end
    
    
    4.times do |repeticion|
      
      secuencia.each_with_index do |nota, i|
        
        paso_stereo = repeticion * secuencia.length + i
        
        cue :tick_stereo,
          paso: paso_stereo,
          fundamental: fundamental_midi,
          indice_patron: indice_patron,
          bajo_corcheas: get(:bajo_corcheas_serie)
        
        
        if pasos_sinte_mono.include?(paso_stereo)
          cue :marca_sinte_mono,
            paso: paso_stereo
        end
        
        if get(:activar_kick)
          
          modo_kick_bajo = get(:modo_kick_bajo)
          
          if modo_kick_bajo == :negras
            tocar_kick = (paso_stereo % 2 == 0)
          else
            tocar_kick = patronKickActual.include?(i)
          end
          
          if tocar_kick
            cue :triggerKick,
              indiceTrigger: i,
              fundamental_midi: fundamental_midi
          end
          
        end
        
        if get(:activar_hihat_contratiempo)
          
          if get(:modo_kick_bajo) == :negras
            
            if paso_stereo % 2 == 1
              cue :triggerHihat,
                paso: paso_stereo
            end
            
          end
          
        end
        
        
        
        silenciados = get(:indices_kalimba_silenciados)
        nota_activa = !silenciados.include?(i)
        
        if nota_activa
          
          if get(:activar_sinte_2)
            if indices_sinte_2_actuales.include?(i)
              cue :nota_sinte_2,
                nota: note(nota)
            end
          end
          
          if get(:activar_sinte_2_complemento)
            if indices_sinte_2_complemento.include?(i)
              cue :nota_sinte_2_complemento,
                nota: note(nota)
            end
          end
          
          play nota, amp: 1, release: 0.75
          play nota + 12, amp: 1, release: 0.75
          play nota + 24, amp: 0.9, release: 0.75
          
        end
        
        
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
    acorde = acordes[indice][indice_acorde]
    
    with_fx :echo, phase: 0.5 do
      with_fx :reverb, mix: 0.9, room: 0.9 do
        play acorde,
          amp: 0.15,
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
    amp_general = 0.8
    
    with_fx :reverb, mix: 0.5, room: 0.96 do
      
      play tonica, pan: -1, amp: 0.1 * amp_env * amp_general, release: 0.15, cutoff: 90
      play tonica + 12, pan: -1, amp: 0.1 * amp_env * amp_general, release: 0.15, cutoff: 90
      play tercera, pan: 1, amp: 0.1 * amp_env * amp_general, release: 0.15, cutoff: 90
      play tercera + 12, pan: 1, amp: 0.1 * amp_env * amp_general, release: 0.15, cutoff: 95
      
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
        play [tonica, tercera, tonica + 12, tercera + 12],
          amp: 0.18,
          attack: 0,
          release: 0.5,
          pan: paneo,
          cutoff: 52
      end
    end
    
  end
  
end

live_loop :sinte_2 do
  
  datos = sync :nota_sinte_2
  
  use_synth :prophet
  use_octave 1
  
  nota = datos[:nota]
  
  if get(:panear_sintes_2)
    pan_sinte = -0.75
    release_sinte = get(:sinte_2_release)
  else
    pan_sinte = 0
    release_sinte = 1.5
  end
  
  with_fx :reverb do
    with_fx :hpf, cutoff: 50 do
      play nota,
        amp: 0.07,
        cutoff: 100,
        release: release_sinte,
        pan: pan_sinte
    end
  end
  
  use_octave 0
  
end

live_loop :sinte_2_complemento do
  
  datos = sync :nota_sinte_2_complemento
  
  use_synth :square
  use_octave 1
  
  nota = datos[:nota]
  
  if get(:panear_sintes_2)
    pan_sinte = 0.75
    release_sinte = get(:sinte_2_complemento_release)
  else
    pan_sinte = 0
    release_sinte = 1.5
  end
  
  with_fx :reverb do
    with_fx :hpf, cutoff: 60 do
      play nota,
        amp: 0.055,
        cutoff: 95,
        release: release_sinte,
        pan: pan_sinte
    end
  end
  
  use_octave 0
  
end

live_loop :kick do
  
  sync :triggerKick
  
  sample :bd_haus,
    cutoff: 79,
    amp: 0.6
  
end

live_loop :bass do
  
  datos = sync :tick_stereo
  
  if get(:activar_kick)
    
    fundamental_midi = datos[:fundamental]
    paso = datos[:paso]
    indice_patron = datos[:indice_patron]
    bajo_corcheas = datos[:bajo_corcheas]
    
    i = paso % 7
    modo_kick_bajo = get(:modo_kick_bajo)
    
    if indice_patron != nil
      patron = patronesKickAndBass[indice_patron]
    else
      patron = []
    end
    
    use_synth :tb303
    
    if bajo_corcheas
      
      play fundamental_midi - 24,
        amp: 0.1,
        attack: 0,
        release: 0.35,
        cutoff: 76,
        res: 0.8
      
    else
      
      if modo_kick_bajo == :negras
        tocar_bajo = (paso % 2 == 0)
      else
        tocar_bajo = patron.include?(i)
      end
      
      if tocar_bajo
        play fundamental_midi - 24,
          amp: 0.1,
          attack: 0,
          release: 0.5,
          cutoff: 76,
          res: 0.8
      end
      
    end
    
  end
  
end


live_loop :tonica_y_quinta do
  
  datos = sync :tick_stereo
  
  if get(:activar_tonica_y_quinta)
    
    fundamental = datos[:fundamental]
    quinta = fundamental + 7
    
    use_synth :blade
    
    with_fx :reverb, mix: 0.35 do
      play fundamental, amp: 0.08, release: 0.2, cutoff: 80, pan: -1
      play quinta, amp: 0.08, release: 0.2, cutoff: 90, pan: 1
    end
    
  end
  
end

direccion = [-1, 1].choose

live_loop :movimiento_estereo do
  
  datos = sync :movimiento_estereo
  
  fundamental = datos[:fundamental_midi]
  modo_mov = get(:modo_movimiento_estereo)
  
  if modo_mov == :aleatorio
    inicio = datos[:pan_inicio]
    final = datos[:pan_final]
  else
    inicio = direccion == 1 ? -1 : 1
    final = direccion == 1 ? 1 : -1
  end
  
  with_fx :reverb, mix: 0.6 do
    with_fx :slicer, phase: 0.125, mix: 0.5, smooth: 0.2, wave: 1 do
      with_fx :slicer, phase: 0.25, smooth: 0.1, wave: 1 do
        
        use_octave -1
        
        s = synth :mod_fm,
          note: fundamental,
          amp: 0.05,
          attack: 0.75,
          release: 8,
          pan: inicio,
          pan_slide: 5
        
        use_octave 1
        
        s1 = synth :pretty_bell,
          note: fundamental + 7,
          amp: 0.075,
          attack: 0.25,
          release: 8,
          pan: inicio,
          pan_slide: 5
        
        control s, pan: final
        control s1, pan: final
        
        if modo_mov != :aleatorio
          direccion = direccion * -1
        end
        
      end
    end
  end
  
  use_octave 0
  
end

live_loop :hihat do
  
  datos = sync :triggerHihat
  
  sample :drum_cymbal_closed,
    amp: 0.35,
    cutoff: 105,
    rate: 1.2
  
end
```
