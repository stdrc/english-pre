---
theme: default
layout: cover
---

# Interrupt

Presented by Yibo Huang & Yuchao Qian

---
layout: center
---

# What Is Interrupt?

<v-click>

# And Why?

</v-click>

---

# Example: Boiling A Kettle Of Water

<img src="" alt="手绘桌子上一个烧水壶" align="middle" style="width: 70%;" />

---

# What Do You Do When The Kettle Is Boiling?

<v-click>

<img src="" alt="手绘一个人坐在烧水壶旁边呆呆地等" align="right" style="width: 50%" />

- Stare at the kettle, waiting for the water to be boiled?

</v-click>

---

# What Do You Do When The Kettle Is Boiling?

<img src="" alt="手绘一边是水壶，另一个房间是人在看书" align="right" style="width: 50%" />

- Stare at the kettle, waiting for the water to be boiled?
- No! You want to study!

<v-click>

- Then how can you know it when it's done?

</v-click>

---

# What Do You Do When The Kettle Is Boiling?

<img src="" alt="手绘一边是水壶，水壶上一个哨子，另一个房间是人在看书" align="right" style="width: 50%" />

- Stare at the kettle, waiting for the water to be boiled?
- No! You want to study!
- Then how can you know it when it's done?
- Use a whistle!

---

# Computer Systems

<img src="" alt="各种外设的图片" align="right" style="width: 50%;" />

- CPU has to communicate with peripherals
  - Keyboards
  - Monitors
  - Disks
  - Ethernet cards
  - ...

---

# Polling - The Old And "Silly" Approach

<v-click>

<img src="" alt="手绘一个人坐在烧水壶旁边呆呆地等，人头上放个 CPU，水壶上放个外设" align="right" style="width: 50%;" />

</v-click>

- Busy waiting
- Easy to implement
- Cannot do other things during polling

---

# Interrupt - A Smarter Approach

<v-click>

<img src="" alt="手绘水壶外设+哨子中断控制器+书房CPU" align="right" style="width: 50%;" />

</v-click>

- CPU can do other things during I/O
- Peripherals interrupt CPU when completed

---
layout: center
---

# Is That Perfect?

<v-click>

# No!

</v-click>

<!--
So, is that perfect?
Is the interrupt mechanism described just now perfect for the communication between CPU and peripherals?

No! There are some problems with it. And, of course, there are also solutions for these problems.
-->

---

# Problem 1: Slow

<v-clicks>

- Much slower than polling
- Water boiling example:
  - Walk from study room to kitchen
- Context switch

</v-clicks>

<!--
The first problem is slow. The interrupt mechanism is much slower than polling.

Take the water boiling example, when the water is boiled, you have to go back to the kitchen from your study room, to "handle the interrupt". That needs more time than just sitting there and waiting for it.

This is called "context switch" in computer systems. The CPU has to switch from the context of the current application task to another context which is used to handle the interrupt.

That's why interrupt is slow.
-->

---

# Solution: Interrupt + Polling

<v-clicks>

- Network card example:
  - Interrupt for the first packet
  - Polling for the remaining packets

</v-clicks>

<!--
And of course we have some solutions, one of which is interrupt + polling.

Let's use network card as an example. In modern network card drivers, if many packets arrive at once, or very closely, the CPU will only be interrupted for only one time, by the first packet, and then the drivers will use polling to get the remaining packets, to ensure the performance.
-->

---

# Problem 2: Occupy the CPU

<div v-click="2">

<img src="" alt="手绘人在倒水" align="right" style="width: 50%;" />

</div>

<div v-click="1">

- Water boiling example:
  - Can't be interrupted when pouring water

</div>
<div v-click="3">

- Other interrupts are MASKED during the processing of a previous one

</div>
<div v-click="4">

- Affect the performance of other urgent tasks

</div>

<!--
Another problem is that, an interrupt will occupy the CPU. That means, when handling an interrupt, the CPU can't be interrupted by other interrupts.

Recall the water boiling example, when you are pouring water from the kettle to a thermos bottle, you cannot be interrupted.

In computer systems, we say that other interrupts are masked during the processing of a previous one. And that will affect the performance of other urgent tasks.
-->

---

# Solution: Top Half + Bottom Half

<v-clicks>

1. Do the most necessary things with interrupt masked - Top Half
2. Unmask other interrupts
3. Finish the remaining work - Bottom Half

</v-clicks>

<!--
Again, when there is a problem, there is a solution.

In Linux operating system, this problem is solved by splitting the interrupt handling process into two stages, the Top Half and the Bottom Half.

When interrupt occurs, the Linux kernel will first do the most necessary things with other interrupts masked. That is the Top Half. Then it will unmask other interrupts. Finally it will finish the remaining work, and this is called Bottom Half. During the Bottom Half, the CPU can be nestedly interrupted again, so other interrupts can be handled as soon as possible.
-->

---
layout: center
---

# Thank You!

<!--
So that's all of our presentation. Thank you very much!
-->
