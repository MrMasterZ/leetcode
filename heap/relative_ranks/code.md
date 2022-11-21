### Code

    public String[] findRelativeRanks(int[] score) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());  // для того, чтобы упорядочить по убыванию очков ( сделать соответствие с рангом)
        HashMap<Integer,Integer> map = new HashMap<>();                               // в map мы сохранм первоначальный порядок: score--i
        int n= score.length;
        int val=0;
        int index=0;
        String[] answer = new String[n]; 
        for(int i=0;i<n;i++)
        {
            map.put(score[i],i);
            pq.add(score[i]);
        }
        
                      
             if(pq.size()>=1)
             {
                 for( int i=1;i<=n;i++)                                            // индекс призового места участников соревнований
                 {
                    val= pq.remove();                                              // извлекаем из очереди количество очков (начиная с максимального)
                    index= map.get(val);                                           // в соответствии с этим количеством очков определяем первоначальный порядок в int[] score
                     
                     if(i==1)
                     {
                        answer[index]="Gold Medal";
                      }
                      else if(i==2)
                      {
                         answer[index]="Silver Medal";
                      }
                     
                      else if(i==3)
                      {
                         answer[index]="Bronze Medal";
                      }
                
                      else
                      {
                          answer[index]=String.valueOf(i);
                      }
                   }
                }
           
             return answer;
          }
