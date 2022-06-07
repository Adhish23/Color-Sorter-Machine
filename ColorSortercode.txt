#include <stm32f1xx.h>
#define  Servo1MinAngle  600             // 0
#define  Servo1MaxAngle  3000 // 180
#define  Servo2MinAngle  500             // 0
#define  Servo2MaxAngle  3000 // 180

void port_init();
void timer2_init();
void servo1_angle(uint32_t angle);
void servo2_angle(uint32_t angle);
void _delay_ms(int time);
void init_ADC();
uint16_t ADC_read(int channel_num);

int s_mode=0;
unsigned int data = 0,i =0,j = 0;
uint16_t value = 0;

int main(void)
{
port_init();
timer2_init();
init_ADC();

while(1)
{
switch(s_mode)
{
case 0:
servo1_angle(180);
_delay_ms(2000);
servo1_angle(97);
_delay_ms(1000);
s_mode++;
break;
case 1:
value=ADC_read(3);
if(value>3400 && value<3900)
{
s_mode=2;
}
else if(value>3950)
{
s_mode=3;
}
else if (value>3100 && value<3400)
{
s_mode=4;
}
else
{
s_mode=5;
}
break;
case 2:
servo2_angle(0);
_delay_ms(2000);
servo1_angle(85);
_delay_ms(1000);
servo1_angle(90);
_delay_ms(1000);
break;
case 3:
servo2_angle(60);
_delay_ms(2000);
servo1_angle(85);
_delay_ms(1000);
servo1_angle(90);
_delay_ms(1000);
break;
case 4:
servo2_angle(90);
_delay_ms(2000);
servo1_angle(85);
_delay_ms(1000);
servo1_angle(90);
_delay_ms(1000);
break;
}}}

void port_init()
{
RCC->CR|=(1<<0);                  //HSE selected as system clock
RCC->CFGR = (1<<15)|(1<<14);      // adc prescalar by 6 , 72/6 = 12

RCC->APB2ENR|=(1<<2)|(1<<9);
RCC->APB1ENR|=(1<<0)
GPIOA->CRL&=~(1<<12)&(1<<13)&(1<<14)&(1<<15);}

void timer2_init()
{
TIM2->CCER|= (1<<8);              //Capture/Compare 1 output enable
TIM2->CCER|= (1<<4);              //Capture/Compare 2 output enable
TIM2->CR1 |= (1<<0)|(1<<7);        //Counter enabled. TIMx_ARR register is buffered
TIM2->ARR = 8399;                  //Auto-reload value
TIM2->CR2 |= (1<<10)|(1<<11);
TIM2->CR2 |= (1<<12)|(1<<13);
TIM2->PSC = 10;                   //Prescaler value
TIM2->CCMR2|= (1<<7)|(1<<6)|(1<<5)|(1<<3)|(1<<2);  //
TIM2->CCMR1|= (1<<15)|(1<<14)|(1<<13)|(1<<11)|(1<<10);  //
TIM2->BDTR|= (1<<15);             //Main output enable
}

void servo1_angle(uint32_t angle)
{
GPIOA->CRL=(1<<8)|(1<<9)|(1<<11);  //Output mode, max speed 50 MHz.Alternate function output Push-pull

uint32_t step = ((Servo1MaxAngle - Servo1MinAngle)/180)*angle;

if(step == 0)
step = Servo1MinAngle;

if(step > Servo1MaxAngle)
step = Servo1MaxAngle;

TIM2->CCR3=step;
}

void servo2_angle(uint32_t angle)
{
GPIOA->CRL=(1<<4)|(1<<5)|(1<<7);  //Output mode, max speed 50 MHz.Alternate function output Push-pull

uint32_t step = ((Servo2MaxAngle - Servo2MinAngle)/180)*angle;

if(step == 0)
step = Servo2MinAngle;

if(step > Servo2MaxAngle)
step = Servo2MaxAngle;

TIM2->CCR2=step;
}


void init_ADC()
{
ADC1->CR2 = (1<<0)|(1<<2)|(1<<22)|(1<<17);//|(1<<1);//|(1<<20)|(1<<17) ; // ADC ON | start of conversion of regular channel
ADC1->SQR1 = 0x00100000;                  // Total number of channels
ADC1->SMPR2 = (1<<0)|(1<<1)|(1<<2);
}

uint16_t ADC_read(int channel_num)
{
ADC1->SQR3 = channel_num;
while((ADC1->CR2 & 0x00000004)!=0);
ADC1->CR2 |= (1<<0);
while((ADC1->SR&0x00000002)==0) ;  // wait for end of conversion bit to be 1
data = ADC1->DR;                  // data stored in adc1->dr is stored in data(unsigned int)
ADC1->SR = 0x00000000;             // clearing eoc and start for regular channel
ADC1->CR2 |= (1<<22);
return data;
}

void _delay_ms(int time)
{
for(int i=0;i<time;i++)
{
for(int j=0;j<1000;j++);
} 

