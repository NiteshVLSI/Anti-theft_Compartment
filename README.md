# Anti-theft_Compartment

### Project Overview

The Anti-Theft Compartment project is a comprehensive security solution designed to safeguard valuable belongings from unauthorized access. This project combines hardware and software components, featuring a digital light sensor to detect intrusion and trigger an alarm. Beyond security, it presents an opportunity to explore the details of RISC-V ISA for ASIC implementation.

### Key Features

- **Light Sensor-Based Intrusion Detection:** The project relies on a digital light sensor to detect unauthorized access, promptly triggering an alarm when the compartment is opened.

- **Alarm Activation:** An alarm system is integrated to provide immediate notification upon unauthorized access.

- **Customizable Hardware and Software:** The project offers flexibility, allowing users to customize both hardware components and software logic to suit their specific requirements.

- **Well-Documented Code:** Clear and comprehensive documentation accompanies the code, making implementation straightforward and user-friendly.

- **Room for Enhancements:** The project is designed with room for further enhancements and integrations, enabling users to expand its capabilities as needed.

<h2>Block Diagram</h2>
<div>
	<img src="https://github.com/NiteshIIITB/Anti-theft_Compartment/assets/140998787/3d857054-9e97-4d45-b923-02434353f34d">

</div>


<h2>C Code</h2>

```

int main()  {

    
    int light_sensor;
    int buzzer;
    int buff;
    
    
        while(1) {
        // Read sensor data into x30
	asm (
            "and %0, x30, 1"
            : "=r"(light_sensor)
        );

       
        

        
        if (light_sensor) {
            // If light sensor output is 1 turn on buzzer
            buff =0xFFFFFFFD;
            asm(
            "and x30,x30, %0\n\t"     // Making 2nd bit from lsb0
            "or %1, x30,2"                 // output at 2nd bit that turn on buzzer
            :"=r"(buff)
            :"r"(buzzer)
        );
        } 
        else {
            // If light sensor output is 0 turn off the buzzer
            buff =0xFFFFFFFD;
            asm(
            "and x30,x30, %0\n\t"     
            "or %1, x30,0"            //Making 2nd bit from lsb(output) as 0
            :"=r"(buff)
            :"r"(buzzer)
        );
        }
    return 0;
}

}



```

<h2>Assembly Code</h2>

```


out:     file format elf32-littleriscv


Disassembly of section .text:

00010054 <main>:
   10054:	fe010113          	addi	sp,sp,-32
   10058:	00812e23          	sw	s0,28(sp)
   1005c:	02010413          	addi	s0,sp,32
   10060:	001f7793          	andi	a5,t5,1
   10064:	fef42623          	sw	a5,-20(s0)
   10068:	fec42783          	lw	a5,-20(s0)
   1006c:	02078063          	beqz	a5,1008c <main+0x38>
   10070:	ffd00793          	li	a5,-3
   10074:	fef42423          	sw	a5,-24(s0)
   10078:	fe442783          	lw	a5,-28(s0)
   1007c:	00ff7f33          	and	t5,t5,a5
   10080:	002f6793          	ori	a5,t5,2
   10084:	fef42423          	sw	a5,-24(s0)
   10088:	01c0006f          	j	100a4 <main+0x50>
   1008c:	ffd00793          	li	a5,-3
   10090:	fef42423          	sw	a5,-24(s0)
   10094:	fe442783          	lw	a5,-28(s0)
   10098:	00ff7f33          	and	t5,t5,a5
   1009c:	000f6793          	ori	a5,t5,0
   100a0:	fef42423          	sw	a5,-24(s0)
   100a4:	00000793          	li	a5,0
   100a8:	00078513          	mv	a0,a5
   100ac:	01c12403          	lw	s0,28(sp)
   100b0:	02010113          	addi	sp,sp,32
   100b4:	00008067          	ret

```

<h2>Instructions</h2>

```
Number of different instructions: 11
List of unique instructions:
lw
mv
li
ori
j
and
beqz
ret
andi
addi
sw


```

## Word of Thanks

I would like to sincerely thank Mr. Kunal Gosh, Founder of VSD (VLSI System Design), for his invaluable assistance and guidance, which played a pivotal role in ensuring the smooth completion of this project flow.


## References

- [OpenSTA GitHub Repository](https://github.com/The-OpenROAD-Project/OpenSTA.git)
- [kunalg123 GitHub Profile](https://github.com/kunalg123)
- [VSDIAT Official Website](https://www.vsdiat.com)
- [RISCV-GNU GitHub Repository by Saketh Gajawada](https://github.com/SakethGajawada/RISCV-GNU)

