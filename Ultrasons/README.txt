#include "mbed.h"
#include "Ultrasons.h"
//#include "TextLCD.h"
 
DigitalOut myled(LED1);
HCSR04  usensor(PA_1,PA_0);
//TextLCD lcd(p14, p16, p17, p18, p19, p20,TextLCD::LCD16x2); // rs, e, d4-d7
unsigned int dist;
unsigned int tabdist [10];
int main()
{
    for (int i=0; i<10;i++)
    {
        tabdist[i]=0;   
    }
    int i=0;
    
    while(1) {
        //printf( "initialisation 0\n");
        usensor.start();
        //printf( "initialisation 1\n");
        wait_ms(30); 
        dist=usensor.get_dist_cm();
        int sum=0;
        if (dist < 2000)
            {
            tabdist[i] = dist;
            for (int nb=0; nb<10;nb++)
            {
                sum += tabdist[nb];
            }
            
            printf( "distance : %u \n", sum/10);
        
        
            if (i==9)
                i=0;
            else
                i++;
            }
    }
}
