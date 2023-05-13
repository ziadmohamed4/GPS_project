# GPS_project

void PortFInit() {
	SYSCTL_RCGCGPIO_R |=0x20;
	while((SYSCTL_PRGPIO_R & 0x20)==0){};
	//GPIO_PORTF_LOCK_R = GPIO_LOCK_KEY; no need
	//GPIO_PORTF_CR_R |= 0X0E; no need
	GPIO_PORTF_AMSEL_R &= ~0X0E;
	GPIO_PORTF_PCTL_R &= ~0X0000FFF0;
	GPIO_PORTF_AFSEL_R &= ~0X0E;
	GPIO_PORTF_DEN_R |= 0X0E;
	GPIO_PORTF_DIR_R |= 0X0E;
	GPIO_PORTF_DATA_R &=~0X0E;
}

void RGB_set(uint8_t mask) {
	mask &= 0xE;
	GPIO_PORTF_DATA_R |= mask;
}

void RGB_clear(uint8_t mask) {
	mask &= 0xE;
	GPIO_PORTF_DATA_R &= ~mask;
}
