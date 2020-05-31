# utl-student-imdividual-exam-score-versus-the-class-average-without-students-score
Student imdividual exam score versus the class average without students score 
    Student individual exam score versus the class average without students score                                                 
                                                                                                                                  
    github                                                                                                                        
    https://tinyurl.com/y9jns5sg                                                                                                  
    https://github.com/rogerjdeangelis/utl-student-individual-exam-score-versus-the-class-average-without-students-score          
                                                                                                                                  
    *_                   _                                                                                                        
    (_)_ __  _ __  _   _| |_                                                                                                      
    | | '_ \| '_ \| | | | __|                                                                                                     
    | | | | | |_) | |_| | |_                                                                                                      
    |_|_| |_| .__/ \__,_|\__|                                                                                                     
            |_|                                                                                                                   
    ;                                                                                                                             
                                                                                                                                  
    data have;                                                                                                                    
       set sashelp.class(obs=3 keep=name height rename=height=score);                                                             
       score=round(score);                                                                                                        
    run;quit;                                                                                                                     
                                                                                                                                  
    *            _               _                                                                                                
      ___  _   _| |_ _ __  _   _| |_                                                                                              
     / _ \| | | | __| '_ \| | | | __|                                                                                             
    | (_) | |_| | |_| |_) | |_| | |_                                                                                              
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                             
                    |_|                                                                                                           
    ;                                                                                                                             
                                                                                                                                  
                                                                                                                                  
    WORK.WANT total obs=3                                                                                                         
                                                                                                                                  
                                                       | RULES                                                                    
                                                       | =====                                                                    
    Obs      ME      MYSCORE    MEANOTHER    DIFOTHERS |                                                                          
                                                       |                                                                          
     1     Alice        57         53.5          3.5   | MeanOther = (51+56)/2             = 53.5                                 
                                                       | DifOthers = 57 - 53.5(meanother)  =  3.5                                 
     2     Joyce        51         56.5         -5.5   |                                                                          
     3     Louise       56         54.0          2.0   |                                                                          
                                                                                                                                  
    *          _       _   _                                                                                                      
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                           
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                          
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                         
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                         
                                                                                                                                  
    ;                                                                                                                             
                                                                                                                                  
    proc sql;                                                                                                                     
      create                                                                                                                      
         table want as                                                                                                            
      select                                                                                                                      
        me                                                                                                                        
       ,myscore                                                                                                                   
       ,mean(otherscore) as meanother                                                                                             
       ,myscore - calculated meanother as difothers                                                                               
      from                                                                                                                        
          (                                                                                                                       
          select                                                                                                                  
             l.name   as me                                                                                                       
            ,l.score  as myscore                                                                                                  
            ,r.name   as other                                                                                                    
            ,r.score  as otherscore                                                                                               
          from                                                                                                                    
            have as r, have as l                                                                                                  
          where                                                                                                                   
            l.name ne r.name                                                                                                      
          )                                                                                                                       
      group                                                                                                                       
        by me, myscore                                                                                                            
                                                                                                                                  
    ;quit;                                                                                                                        
                                                                                                                                  
                                                                                                                                  
