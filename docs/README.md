Voici les ressources officielles pour démarrer :

## 1. Documentation matérielle (référence absolue)

**Datasheet complet ATmega328P** (Microchip, ~660 pages)
`https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-7810-Automotive-Microcontrollers-ATmega328P_Datasheet.pdf`
— C'est ta bible : mapping mémoire, registres de chaque périphérique (GPIO, Timer, UART, ADC), interruptions, tout y est.

**AVR Instruction Set Manual** (Microchip, officiel)
`https://ww1.microchip.com/downloads/en/DeviceDoc/AVR-InstructionSet-Manual-DS40002198.pdf`
— Chaque instruction avec son opcode binaire exact, sa syntaxe, son effet sur SREG, son nombre de cycles. C'est le document que tu vas ouvrir en permanence pendant le développement du décodeur.

Version consultable en ligne (utile pour chercher rapidement une instruction) :
`https://onlinedocs.microchip.com/oxy/GUID-0B644D8F-67E7-49E6-82C9-1B2B9ABE6A0D-en-US-23/index.html`

## 2. Toolchain pour générer tes programmes de test

**avr-gcc** — le compilateur officiel qui te permet de compiler du C/Arduino en binaire AVR réel
- Sous Linux : `apt install gcc-avr avr-libc binutils-avr`
- Sous macOS : `brew tap osx-cross/avr && brew install avr-gcc`

**avr-libc** — la libc pour AVR (registres nommés, macros d'interruption), utile pour écrire tes programmes de test sans tout faire en assembleur brut.

## 3. Référence croisée (à consulter, pas à copier)

**simavr** — un émulateur AVR open source déjà existant, bien structuré
`https://github.com/buserror/simavr`
— Utile si tu bloques sur une question d'architecture ou de timing, pour vérifier ta compréhension. Ne pas copier le code, mais ça sert de "second avis" quand le datasheet est ambigu.

## Comment les utiliser ensemble concrètement
1. Tu lis le datasheet pour comprendre l'architecture (mémoire, registres, périphériques)
2. Tu utilises l'Instruction Set Manual pour implémenter le décodeur d'opcodes instruction par instruction
3. Tu écris des petits programmes C, tu les compiles avec `avr-gcc -mmcu=atmega328p`
4. Tu extrais le binaire avec `avr-objcopy` en `.hex` ou tu gardes l'`.elf`, que tu charges dans ta Flash émulée pour tester

Tu veux qu'on commence par décortiquer le mapping mémoire du datasheet (Flash/SRAM/registres I/O), ou plutôt par la structure des opcodes (comment un octet binaire devient une instruction) ?