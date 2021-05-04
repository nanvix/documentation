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
[ ] Read documentation about the Memory stuff (MMU, TLB..)
```

