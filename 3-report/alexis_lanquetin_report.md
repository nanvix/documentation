# Alexis Lanquetin - Internship Diary

## _Description_

I am a french UGA student doing an internship from April 26th, 2021, to July 30th, 2021. During this internship, I will work on the development of Nanvix on the ARM64 architecture. I'll use this file to write down and keep a track of what I am doing.
> Github: https://github.com/Neyrian
> 
> Mail:   alexis.lanquetin@gmail.com

_Last Update: Tuesday 04th, May 2021_

## **Week 1** - _04/26/21 - 04/30/21_

### Objectives
```
[x] Understand Nanvix code
[x] Setup Nanvix environnement
[x] Build and Run the hal for ARM64 arch
[x] Enable PMU for ARM64
```

During the first day, I had some issues with my Debian computer. When I tried to setup Nanvix, I undergo error with my Debian image and thus, I broke my computer. Hence, I installed Unbuntu 20.04. Then, I successfully built and ran the HAL on my new computer and everything worked. 
I talked with José Luiz de Souza about his work on Nanvix. He is also working on the ARM64 arch and so, he sent me some documentation he was using. He also showed me how to use gdb to debug nanvix which allowed me to try my hand with gdb and to further look for how the code is structured and work.
When I was familiar with Nanvix, Pedro Henrique Penna asked me to enable PMU for ARM64. So I read a lot of documentation to understand how PMU work and how I can enable it for Nanvix. 
I figured out how to implement PMU and I committed my work.

## **Week 2** - _05/03/21 - 05/07/21_

### Objectives

```
[x] Writing this Report
[X] Read documentation about the Memory stuff (MMU, TLB..)
```
The goal during this week was to read as much documentation as possible about how memory work on ARM64 Architecture. I was already a bit familiar with pagination and MMU, so I went through this task with ease. However, I had to figure out how does Translation Lookaside Buffer work.
Thursday afternoon, I had a meeting with Pedro, Jean-François and Marcio where I explained my research. It appears that in ARM, there are up to three translation level but Nanvix support only two. Plus, I have to go deeper in the understanding of how exactly all these things (The Page Directory, Page Table, Registers...) are defined and implemented in order to develop this feature.

Firstly, all the other OS implementation of the MMU for ARM I've found use mask to implement PTE, PDE, and PMD. Therefore, I've tried to do it this way, but I've figured out that it would be easier and clearer to keep the same structure used in Nanvix.
This was not an easy part because I had to understand how does MMU and TLB work on Nanvix in order to adapt my researches and implement it. I made some understanding mistake but I think that I have a good picture now and the next week I'll start the implementation.

You can fin some main sources I've used to understand how memory work:

- https://armv8-ref.codingbelief.com/en/preface.html
- https://git.es.eti.uni-siegen.de/mschmidt/linux-stable-mcs/-/tree/master/arch/arm64/include
- https://developer.arm.com/documentation/101811/0101/Translation-Lookaside-Buffer-maintenance
- https://cs140e.sergio.bz/docs/ARMv8-A-Programmer-Guide.pdf (page 162)
- https://wenboshen.org/posts/2018-09-09-page-table.html
- https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwjqnLm-nMTwAhWGmRQKHQi7BKMQFjACegQIBBAD&url=https%3A%2F%2Fdocumentation-service.arm.com%2Fstatic%2F5efa1d23dbdee951c1ccdec5%3Ftoken%3D&usg=AOvVaw38hHvTbFXER-_BItcS9O3Z

## **Week 3** - _05/10/21 - 05/12/21_

### Objectives

```
[x] Define the structures PTE, PDE
[x] Define the missing translation level PMD (level 2)
[ ] Enable the MMU
[ ] Enable TLB
```
During this week, I defined the structures required for pagination (PTE, PDE and the missing one, PMD). I also defined some parameters, such as mask, shifts or size.
Everything compiles and tests passe!
The objectives for the next week are to enable MMU and defines TLB.

You can fin some main sources I've used to define these structures:

- https://armv8-ref.codingbelief.com/en/chapter_d4/d43_3_memory_attribute_fields_in_the_vmsav8-64_translation_table_formats_descriptors.html?q=
- https://armv8-ref.codingbelief.com/en/chapter_d4/d43_1_vmsav8-64_translation_table_descriptor_formats.html
- https://git.es.eti.uni-siegen.de/mschmidt/linux-stable-mcs/-/blob/master/arch/arm64/include/asm/pgtable-hwdef.h

## **Week 4** - _05/17/21 - 05/21/21_

### Objectives

```
[ ] Enable the MMU
[ ] Enable TLB
[X] Flushing TLB
[X] Define TLBe
```

After a discussion with Pedro, I've figured out that the TLB is managed by the hardware and not the software, which explains why I had trouble to find how to implement it (i.e. to define TLB struct, TLB entry struct, TLB initialization). This is why I spent few days to fail to find anything and lost some times. But anyway, at the end of this week, I now have a look on how enable the mmu and the tlb. 
For now, I undergo issues to write in the System Control Register (EL1) (SCTLR_EL1), which provides top level control of the system, including its memory system, at EL1 and EL0. I am currently working with José on it, because he has used this register.

You can fin some main sources I've used to enable MMU and TLB:

- https://developer.arm.com/documentation/ddi0500/j/Level-1-Memory-System/Direct-access-to-internal-memory/TLB-RAM-accesses?lang=en#CHDFGIAB
- https://developer.arm.com/documentation/den0024/a/The-Memory-Management-Unit/Translating-a-Virtual-Address-to-a-Physical-Address/Configuring-and-enabling-the-MMU
- https://code.govanify.com/govanify/coreboot-navi/src/branch/master/payloads/libpayload/arch/arm64/mmu.c
- http://web.cs.wpi.edu/~cs4515/d15/Protected/LecturesNotes_D15/CS4515-TeamB-Report.pdf
- https://github.com/bztsrc/raspi3-tutorial/blob/master/10_virtualmemory/mmu.c
