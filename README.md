# Scilab

clear ;
//parâmetros do processo:

h=[0];
v=[1,0,1,1,1,3,4,5,6,3,4,5,6,6,7,5,3,7,8,5,5,5,4,5,2,3,2,1,1,1,1,1];
des=[2,2,2,2,2,2,2,2,2,2,2,5,5,5,5,5,5,5,5,5,5,5,5,3,3,3,3,3,3,3];

e=[0];

tfinal=30; t=1;
tt=0;

H=[0];
E=[];

// cálculos dos parâmetros vinculados ao desvio do setpoint(erro)
       
       while t<tfinal
 
// cálculos dos parâmetros vinculados ao desvio do setpoint(erro)
 

h(t)=h(t)-v(t);
e1= (des(t)-h(t));
dv=diff(v);

if e1 > 0 
 
    if (e1 > 0 & e1 <= 5 ) 
        A=0;
    end 
    if (e1 > 1 & e1 <= 4) 
        A=2.5;
    end
        if (e1 >1 & e1 <=7 )  
        A=5;
    end
    if e1 >7    
        A=10;
    end    
    
    if (v(t) > 2)
        {
         e1 = 7;
        }
    end
end

if e1 <= 3

   A=2  ;
    
end

if e1 >= 5
    
    A = 6;
    
end

if e1 < 2
    
    A = 1;
    end

  
    h=[h,[h(t)+A]];
e2= (des(t)-h(t+1));

E=[E;abs(e2)]; 

H=[H,h(t+1)] ;

 e=[e,e1];
 t=t+1;
 tt=[tt,t];       
end
sum(E)
plot(tt,H,tt,des)
