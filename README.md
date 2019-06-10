## F103 TIM3 实现1us延时

- Timer Clocks : 60MHZ
- PSC : 0
- ARR : 59

---
main.c添加

```c
void wait_us(uint32_t us)
{
	usDelay=us;
    HAL_TIM_Base_Start_IT(&htim3);//开启定时器中断
    while(usDelay);
    HAL_TIM_Base_Stop_IT(&htim3);
}

void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)//中断回调函数
{
	if(htim == (&htim3))
	{
		usDelay--;
	}
}
```
