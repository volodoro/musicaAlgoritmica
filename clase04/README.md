```
# Welcome to Sonic Pi
live_loop :maestro do
  cue [:uno, :uno, :dos, :tres, :tres].choose
  sleep 0.125  
end


live_loop :uno do
  
  sync :uno
  sample :loop_amen, onset: choose
  
end

live_loop :dos do
  
  sync :dos
  sample :loop_mehackit1, onset: choose
  
end

live_loop :tres do
  
  sync :tres
  sample :loop_compus, onset: choose
end
```
