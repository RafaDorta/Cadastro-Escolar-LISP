# Cadastro-Escolar-LISP



(defun vincular-disc-curso (DISCIPLINA CURSO BD)




    (if (eq BD nil)

        nil

        (if (eq DISCIPLINA (caaar BD))

            (if (eq (cdaar BD) nil)
            
            
            

                (cons 
                                    
                (cons (cons (caaar BD) CURSO) (cons 
                 (cadar BD)
                (cons (cons  (car(caddar BD)) nil) nil))) 
                (vincular-disc-curso DISCIPLINA CURSO (cdr BD))
                )



                (cons 
                (car BD) 
                (vincular-disc-curso DISCIPLINA CURSO (cdr BD))
                
                
                )

                
            )

            (cons 
                (car BD) 
                (vincular-disc-curso DISCIPLINA CURSO (cdr BD))
                
                
                )

        )

    )


)



(DEFUN VINCULAR (PROFESSORES DISCIPLINAS BD)
    
    (if (eq BD nil )

        (if (eq(car DISCIPLINAS) nil)
           
           
            nil

        
        

            (cons 
                (cons (cons (car DISCIPLINAS) nil) (cons 
                (cons nil nil) 
                (cons PROFESSORES nil)  ) ) 

                (VINCULAR PROFESSORES (cdr DISCIPLINAS) 
                    (cdr BD))
            )   
        )

        (if (eq (caaar BD) (car DISCIPLINAS))
            (if (eq (car(caddar bd)) nil)
                (cons 
                    (cons (cons (caaar BD)  (cdaar BD)) 
                    (cons 
                    (cadar BD)  
                    (cons   PROFESSORES nil))) 
                    (VINCULAR PROFESSORES (cdr DISCIPLINAS) 
                    (cdr BD))
                )

                (cons 
                      (cons 
                    
                        (cons (caaar BD)  (cdaar BD)) 
                        
                        (cons  
                            (cadar BD) 
                                
                    (cons (adiciona-aluno (caddar BD) PROFESSORES) 
                               nil ) 
                           
                        ) 
                      ) 
                    (VINCULAR PROFESSORES (cdr DISCIPLINAS) (cdr BD))
                )
            )
            
            (cons (car bd) (VINCULAR PROFESSORES DISCIPLINAS (cdr BD)))
        )

    )
    


)





(defun adiciona-aluno (BD AD)

      (if (eq AD nil)


              nil

              (if (eq BD nil)

                  (cons  (car AD)  (adiciona-aluno  BD  (cdr AD)) )

                  (cons  (car BD)  (adiciona-aluno  (cdr BD) AD) )

              )




      )
)






(DEFUN MATRICULAR (ALUNOS DISCIPLINAS BD)
    

    (if (eq BD nil )

        (if (eq(car DISCIPLINAS) nil)
           
           
            nil

        
        

            (cons 
                (cons (cons (car DISCIPLINAS) nil) (cons 
                 (adiciona-aluno nil ALUNOS)  
                (cons (cons nil nil) nil )  ) ) 

                (matricular ALUNOS (cdr DISCIPLINAS) (cdr BD))
            )   
        )

        (if (eq (caaar BD) (car DISCIPLINAS))
            (if (eq (caadar bd) nil)
                (cons 
                    (cons (cons (caaar BD)  (cdaar BD)) (cons 
                     ALUNOS  
                    (cons (caddar BD) nil))) 
                    (matricular ALUNOS (cdr DISCIPLINAS) (cdr BD))
                )

                (cons 
                    (cons (cons (caaar BD)  (cdaar BD)) 
                    (cons  (adiciona-aluno (cadar bd) ALUNOS)
                    (cons (caddar BD) nil )  ) ) 
                    (matricular ALUNOS (cdr DISCIPLINAS) (cdr BD))
                )
            )
            
            (cons (car bd) (matricular ALUNOS DISCIPLINAS (cdr BD)))
        )

    )
)






(defun cancelar-matricula (ALUNOS DISCIPLINAS BD)

    (if (eq BD nil )

            nil

            (if (eq (caaar BD) (car DISCIPLINAS))

                (if   (and (eq (car(remove-aluno (cadar bd) ALUNOS)) nil ) 
                 (eq (car(caddar BD))  nil) )

                    (cancelar-matricula ALUNOS (cdr DISCIPLINAS) (cdr BD))


                    (cons 
                        (cons (cons (caaar BD)  (cdaar BD)) 
                        (cons  (remove-aluno (cadar bd) ALUNOS)
                        (cons (caddar BD) nil )  ) ) 
                        (cancelar-matricula ALUNOS (cdr DISCIPLINAS) (cdr BD))
                    )

                )
                (cons (car bd) (cancelar-matricula ALUNOS DISCIPLINAS (cdr BD)))
            )
        )
)


(defun repete (BD AD)

    (if (eq AD nil)

        nil

        (if (eq  (car BD) (car AD) )

            T


            (repete BD (cdr AD))



        )


    )
)




(defun remove-aluno (BD AD)

    (if (eq BD nil)
   
   
        nil
   
        
        (if (repete BD AD)
        
            (remove-aluno (cdr BD) AD)


            (cons  (car BD)  (remove-aluno (cdr BD)  AD) )
        
        )
    

    )

)



(defun remover-vinculo (PROFESSORES DISCIPLINAS BD)

    (if (eq BD nil )

            nil

            (if (eq (caaar BD) (car DISCIPLINAS))

                (if   (and (eq (car(remove-aluno (caddar bd) PROFESSORES)) nil ) 
                 (eq (caadar BD)  nil) )

                    (remover-vinculo PROFESSORES (cdr DISCIPLINAS) (cdr BD))


                    (cons 
                        (cons (cons (caaar BD)  (cdaar BD)) 
                        (cons  (cadar BD)
                        (cons (remove-aluno (caddar bd) PROFESSORES) nil )  ) ) 
                        (remover-vinculo PROFESSORES (cdr DISCIPLINAS) (cdr BD))
                    )

                )
                (cons (car bd) (remover-vinculo PROFESSORES DISCIPLINAS (cdr BD)
                ))
            )
        )
)



(defun alunos? (BD)

    (if (eq BD nil )
    
    nil

    
    (cons (cadar BD) (alunos? (cdr BD)))
    
    )

)

(defun professores? (BD)

    (if (eq BD nil )
    
    nil

    
    (cons (caddar BD) (professores? (cdr BD)))
    
    
    )

)

(defun DISCIPLINAS? (BD)

    (if (eq BD nil )
    
    nil

    
    (cons (caar BD) (DISCIPLINAS? (cdr BD)))
    
    
    )

)


(defun vinculados? (DISCIPLINA BD)

    (if (eq BD nil )
    
        nil

    

        (if (eq (car DISCIPLINA) (caaar bd))

                (caddar BD)

                (vinculados? DISCIPLINA (cdr bd))
        
        )
    )

)

(defun disc-curso? (DISCIPLINA BD)

    (if (eq BD nil )
    
        nil

    

        (if (eq (car DISCIPLINA) (caaar bd))

                (cdaar bd)

                (disc-curso? DISCIPLINA (cdr bd))
        
        )
    )

)

(defun matriculados? (DISCIPLINA BD)

    (if (eq BD nil )
    
        nil

    

        (if (eq (car DISCIPLINA) (caaar bd))

                (cadar BD)

                (matriculados? DISCIPLINA (cdr bd))
        
        )
    )

)


(defun cursa? (ALUNO BD)

    (if (eq BD nil )
    
        nil

    
        (if (repete ALUNO (cadar BD) )
        
            (cons (caaar bd) (cursa? ALUNO  (cdr bd)   ))


            (cursa? ALUNO  (cdr bd) )
        
        )
        
    )

)

(defun MINISTRA? (PROFESSOR BD)

    (if (eq BD nil )
    
        nil

    
        (if (repete PROFESSOR (caddar BD) )
        
            (cons (caaar bd) (MINISTRA? PROFESSOR  (cdr bd)   ))


            (MINISTRA? PROFESSOR  (cdr bd) )
        
        )
        
    )

)


