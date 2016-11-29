ARCH_FLAGS=-mcpu=cortex-m0
CC = arm-none-eabi-gcc
AR = arm-none-eabi-gcc-ar

TARGET_CFLAGS = $(ARCH_FLAGS) $(TARGET_INCLUDES) -mthumb -flto -Wall -static -ffunction-sections -Ofast -c -DSTM32F0xx
TARGET_LFLAGS = $(ARCH_FLAGS) --specs=nosys.specs -mthumb -flto -static -Ofast -Wl,-Map=./out_target/target.map,--gc-section,-T ./link.ld

TARGET_INCLUDES := \
	-I./. \
	-I./cmsis_core \
	-I./cmsis_boot \
	-I./stm32_lib/inc

TARGET_LINK_FILES := \
	./out_target/amiv_ad9984a.o \
	./out_target/amiv_cmd.o \
	./out_target/amiv_fpga.o \
	./out_target/amiv_main.o \
	./out_target/amiv_button.o \
	./out_target/amiv_flash.o \
	./out_target/amiv_irq.o \
	./out_target/amiv_util.o \
	./out_target/amiv_adv7511.o \
	./out_target/amiv_config.o \
	./out_target/amiv_i2c.o \
	./out_target/amiv_uart.o \
	./out_target/system_stm32f0xx_temp.o \
	./out_target/startup_stm32f0xx.o \
	./out_target/stm32f0xx_exti.o \
	./out_target/stm32f0xx_flash.o \
	./out_target/stm32f0xx_gpio.o \
	./out_target/stm32f0xx_i2c.o \
	./out_target/stm32f0xx_misc.o \
	./out_target/stm32f0xx_rcc.o \
	./out_target/stm32f0xx_syscfg.o \
	./out_target/stm32f0xx_usart.o

TARGET = target

all: $(TARGET)

$(TARGET):
	@mkdir ./out_target 2>/dev/null; true
	@echo Compiling target...
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_ad9984a.o ./amiv_ad9984a.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_cmd.o ./amiv_cmd.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_fpga.o ./amiv_fpga.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_main.o ./amiv_main.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_button.o ./amiv_button.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_flash.o ./amiv_flash.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_irq.o ./amiv_irq.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_util.o ./amiv_util.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_adv7511.o ./amiv_adv7511.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_config.o ./amiv_config.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_i2c.o ./amiv_i2c.c
	$(CC) $(TARGET_CFLAGS) -o out_target/amiv_uart.o ./amiv_uart.c
	$(CC) $(TARGET_CFLAGS) -o out_target/system_stm32f0xx_temp.o ./cmsis_boot/system_stm32f0xx_temp.c
	$(CC) $(TARGET_CFLAGS) -o out_target/startup_stm32f0xx.o ./cmsis_boot/startup/startup_stm32f0xx.s
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_exti.o ./stm32_lib/src/stm32f0xx_exti.c
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_flash.o ./stm32_lib/src/stm32f0xx_flash.c
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_gpio.o ./stm32_lib/src/stm32f0xx_gpio.c
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_i2c.o ./stm32_lib/src/stm32f0xx_i2c.c
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_misc.o ./stm32_lib/src/stm32f0xx_misc.c
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_rcc.o ./stm32_lib/src/stm32f0xx_rcc.c
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_syscfg.o ./stm32_lib/src/stm32f0xx_syscfg.c
	$(CC) $(TARGET_CFLAGS) -o out_target/stm32f0xx_usart.o ./stm32_lib/src/stm32f0xx_usart.c

	@echo Linking...
	$(CC) $(TARGET_LFLAGS) -o out_target/target.elf $(TARGET_LINK_FILES)

	@echo Create binary...
	arm-none-eabi-objcopy -O binary out_target/target.elf out_target/target.bin

clean:
	rm -rf ./out_target
