import random
from itertools import zip_longest

class ga:
           def __init__(self,maxmin,type,range,population_size):
                   if maxmin.lower()=='maxima' or maxmin.lower()=='minima':
                                self.condition = maxmin.lower()
                   else:
                           self.condition = random.choice(['maxima','minima'])
                   if type.lower()=='logic'or type.lower()=='heuristic':
                                self.type=type.lower()
                   else:
                        self.type = random.choice(['heuristic','logic'])
                   if len(range)!=2:
                           print('please enter proper range')
                   else:
                        self.range = range
                   self.population_size = population_size
                   self.driver()

           def function(self,x):
                return (x**2)*(x-1)*(x-2)*(x-4)*(x-2)*(x)

           def create(self):
               self.genepool=[]
               increment = round(len(self.range)/self.population_size,2)
               i = self.range[0]
               while i<=(self.range[-1]):
                      i = round(i,2)
                      self.genepool.append(i)
                      i+=increment
               return self.genepool

           def Heurisitic_crossmut(self,gen):
                child = []
                p1 = bin(int(10*random.choice(gen)))
                p2 = bin(int(10*random.choice(gen)))
                if random.random()<1:
                    if len(p1)>len(p2):
                          p2+=(len(p1)-len(p2))*'0'
                    else:
                          p1+=(len(p2)-len(p1))*'0'
                    rndpt1= random.choice(range(len(p1)))
                    rndpt2= random.choice(range(len(p2)))

                    if rndpt1>rndpt2:
                        if random.random()<0.7:
                          child.append(p1[0:rndpt2]+p2[rndpt2:rndpt1]+p1[rndpt1:0])
                        else:
                          child.append(p1[0:rndpt2]+p2[rndpt2:rndpt1]+p1[rndpt1:0])
                    elif rndpt1<rndpt2:
                        if random.random()<0.3:
                          child.append(p1[0:rndpt1]+p2[rndpt1:rndpt2]+p1[rndpt2:0])
                        else:
                          child.append(p1[0:rndpt1]+p2[rndpt1:rndpt2]+p1[rndpt2:0])
                    else:
                          child.append(p1[0:rndpt1]+p2[rndpt1:rndpt2]+p1[rndpt2:0])
                    return sum(2**index for index in range(len(child)) if child[::-1][index]=='1')/10

                else:
                    for k,v in zip_longest(p1,p2):
                        if random.random()<0.5:
                             if k==None:
                                 child.append('0')
                             else:
                                 child.append(k)
                        elif random.random()<0.8:
                             if v==None:
                                 child.append('0')
                             else:
                                 child.append(v)
                        else:
                             child.append(random.choice(['0','1']))
                    return sum(2**index for index in range(len(child)) if child[::-1][index]=='1')/10

           def Logic_crossmut(self,gen):
                p1 = random.choice(gen)
                p2 = random.choice(gen)
                p3 = random.choice(gen)
                child = round((p1+p2+p3)/3,2)
                return child


           def driver(self):
                 gen = self.create()
                 print(gen)
                 if self.condition=='maxima':
                       m = -1
                 else:
                       m = 1
                 epoch = 0
                 if self.type=='logic':
                     while epoch<100:
                           gen = sorted(gen,key = lambda group:self.function(group))[::m]
                           print('generation {},  x = {},  f(x) = {}'.format(epoch,gen[0],self.function(gen[0])))
                           new_gen = gen[0:self.population_size//2]
                           for _ in range(self.population_size-self.population_size//2):
                                new_gen.append(self.Logic_crossmut(gen))
                           gen = new_gen
                           epoch+=1
                 else:
                      while epoch<100:
                            gen = sorted(gen,key = lambda group:self.function(group))[::m]
                            print('generation {},  x = {},  f(x) = {}'.format(epoch,gen[0],self.function(gen[0])))
                            new_gen = gen[0:self.population_size//2]
                            for _ in range(self.population_size-self.population_size//2):
                                 new_gen.append(self.Heurisitic_crossmut(gen))
                            gen = new_gen
                            epoch+=1

ga('minima','logic',[0,2],15)
