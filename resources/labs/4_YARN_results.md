- Run this script from your edge node
  Check it first: there are 1-2 things wrong with it
    
    * Output directory /results not available and user has no rights to create it => make it relative, meaning /user/roedelk/results
    * Size too small 100000 is 10MB instead of 10GB as the filename indicates.

    
- Modify the script to echo the parameter values for each run
  Incorporate the time command to report how long each job takes to finish
   
- Change the mapper, reducer, and container memory parameters to emulate different resource demands
  Run the script: your most demanding job should try to max out the cluster
  
=> Unfortunately mistake in duration computation, only gen correct!

duration for 2 map, 1 red, 2048 MB RAM:      gen: 58s   sort: -1479418959s   total: -1479418901s
duration for 2 map, 1 red, 4096 MB RAM:      gen: 54s   sort: -1479419013s   total: -1479418959s
duration for 2 map, 2 red, 512 MB RAM:       gen: 63s   sort: -1479419076s   total: -1479419013s
duration for 2 map, 2 red, 1024 MB RAM:      gen: 64s   sort: -1479419140s   total: -1479419076s
duration for 2 map, 2 red, 2048 MB RAM:      gen: 60s   sort: -1479419200s   total: -1479419140s
duration for 2 map, 2 red, 4096 MB RAM:      gen: 58s   sort: -1479419258s   total: -1479419200s
duration for 2 map, 4 red, 512 MB RAM:       gen: 63s   sort: -1479419321s   total: -1479419258s
duration for 2 map, 4 red, 1024 MB RAM:      gen: 72s   sort: -1479419393s   total: -1479419321s
duration for 2 map, 4 red, 2048 MB RAM:      gen: 60s   sort: -1479419453s   total: -1479419393s
duration for 2 map, 4 red, 4096 MB RAM:      gen: 58s   sort: -1479419511s   total: -1479419453s
duration for 2 map, 8 red, 512 MB RAM:       gen: 63s   sort: -1479419574s   total: -1479419511s
duration for 2 map, 8 red, 1024 MB RAM:      gen: 72s   sort: -1479419646s   total: -1479419574s
duration for 2 map, 8 red, 2048 MB RAM:      gen: 64s   sort: -1479419710s   total: -1479419646s
duration for 2 map, 8 red, 4096 MB RAM:      gen: 62s   sort: -1479419772s   total: -1479419710s
duration for 4 map, 1 red, 512 MB RAM:       gen: 62s   sort: -1479419834s   total: -1479419772s
duration for 4 map, 1 red, 1024 MB RAM:      gen: 65s   sort: -1479419899s   total: -1479419834s
duration for 4 map, 1 red, 2048 MB RAM:      gen: 61s   sort: -1479419960s   total: -1479419899s
duration for 4 map, 1 red, 4096 MB RAM:      gen: 61s   sort: -1479420021s   total: -1479419960s
duration for 4 map, 2 red, 512 MB RAM:       gen: 68s   sort: -1479420089s   total: -1479420021s
duration for 4 map, 2 red, 1024 MB RAM:      gen: 66s   sort: -1479420155s   total: -1479420089s
duration for 4 map, 2 red, 2048 MB RAM:      gen: 64s   sort: -1479420219s   total: -1479420155s
duration for 4 map, 2 red, 4096 MB RAM:      gen: 55s   sort: -1479420274s   total: -1479420219s
duration for 4 map, 4 red, 512 MB RAM:       gen: 66s   sort: -1479420340s   total: -1479420274s
duration for 4 map, 4 red, 1024 MB RAM:      gen: 67s   sort: -1479420407s   total: -1479420340s
duration for 4 map, 4 red, 2048 MB RAM:      gen: 63s   sort: -1479420470s   total: -1479420407s
duration for 4 map, 4 red, 4096 MB RAM:      gen: 57s   sort: -1479420527s   total: -1479420470s
duration for 4 map, 8 red, 512 MB RAM:       gen: 75s   sort: -1479420602s   total: -1479420527s
duration for 4 map, 8 red, 1024 MB RAM:      gen: 70s   sort: -1479420672s   total: -1479420602s
duration for 4 map, 8 red, 2048 MB RAM:      gen: 67s   sort: -1479420739s   total: -1479420672s
duration for 4 map, 8 red, 4096 MB RAM:      gen: 74s   sort: -1479420813s   total: -1479420739s
duration for 8 map, 1 red, 512 MB RAM:       gen: 66s   sort: -1479420879s   total: -1479420813s
duration for 8 map, 1 red, 1024 MB RAM:      gen: 68s   sort: -1479420947s   total: -1479420879s
duration for 8 map, 1 red, 2048 MB RAM:      gen: 62s   sort: -1479421009s   total: -1479420947s
duration for 8 map, 1 red, 4096 MB RAM:      gen: 73s   sort: -1479421082s   total: -1479421009s
duration for 8 map, 2 red, 512 MB RAM:       gen: 71s   sort: -1479421153s   total: -1479421082s
duration for 8 map, 2 red, 1024 MB RAM:      gen: 69s   sort: -1479421222s   total: -1479421153s
duration for 8 map, 2 red, 2048 MB RAM:      gen: 64s   sort: -1479421286s   total: -1479421222s
duration for 8 map, 2 red, 4096 MB RAM:      gen: 64s   sort: -1479421350s   total: -1479421286s
duration for 8 map, 4 red, 512 MB RAM:       gen: 69s   sort: -1479421419s   total: -1479421350s
duration for 8 map, 4 red, 1024 MB RAM:      gen: 66s   sort: -1479421486s   total: -1479421420s
duration for 8 map, 4 red, 2048 MB RAM:      gen: 64s   sort: -1479421550s   total: -1479421486s
duration for 8 map, 4 red, 4096 MB RAM:      gen: 66s   sort: -1479421616s   total: -1479421550s
duration for 8 map, 8 red, 512 MB RAM:       gen: 72s   sort: -1479421688s   total: -1479421616s
duration for 8 map, 8 red, 1024 MB RAM:      gen: 74s   sort: -1479421762s   total: -1479421688s
duration for 8 map, 8 red, 2048 MB RAM:      gen: 62s   sort: -1479421824s   total: -1479421762s
duration for 8 map, 8 red, 4096 MB RAM:      gen: 78s   sort: -1479421902s   total: -1479421824s

