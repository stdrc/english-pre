---
theme: default
layout: cover
title: Interrupt
---

# The Interrupt Mechanism in Computer

Presented by Yibo Huang & Yuchao Qian

<!--
Good morning everybody.

My name is Huang Yibo and my teammate's name is Qian Yuchao.

Today our group is going to talk about the interrupt mechanism in computer systems.
-->

---
layout: center
---

# What Is Interrupt?

<v-click>

# And Why?

</v-click>

<!--
So, in computer systems, what is interrupt?

And, why we need it?

To answer these two questions, I'm going to give you a vivid example.
-->

---

# Example: Boiling A Kettle Of Water

<img src="/images/kettle.png" alt="手绘桌子上一个烧水壶" style="width: 60%; margin: auto;" />

<!--
There is a kettle of water on the desk. Please imagine that we are currently boiling a kettle of water.
-->

---

# What Do You Do When The Kettle Is Boiling?

<v-click>

<img src="/images/waiting-for-kettle.png" alt="手绘一个人坐在烧水壶旁边呆呆地等" align="right" style="width: 60%" />

- Stare at the kettle, waiting for the water to be boiled?

</v-click>

<!--
Now given that we are boiling a kettle of water, we should turn it off when the water boils.

There're several ways to do it.

First, we just stare at the kettle, waiting for the water to be boiled.

Is this solution feasible?
-->

---

# What Do You Do When The Kettle Is Boiling?

<img src="/images/kitchen-study-room.png" alt="手绘一边是水壶，另一个房间是人在看书" align="right" style="width: 60%" />

- Stare at the kettle, waiting for the water to be boiled?
- No! You want to study!

<v-click>

- Then how can you know it when it's done?

</v-click>

<!--
Absolutely, Not!

Because you want to study instead of wasting your time just staring at the kettle!
-->

---

# What Do You Do When The Kettle Is Boiling?

<img src="/images/kettle-with-whistle.png" alt="手绘一边是水壶，水壶上一个哨子，另一个房间是人在看书" align="right" style="width: 60%" />

- Stare at the kettle, waiting for the water to be boiled?
- No! You want to study!
- Then how can you know it when it's done?
- Use a whistle!

<!--
Then how can you know it when it's done ?

We can use a whistle.

When the kettle boils, it blows the whistle.

And then we hear the whistle so we know it's time to turn it off.
-->

---

# Computer Systems

<img src="/images/peripherals.jpg" alt="各种外设的图片" align="right" style="width: 50%;" />

- CPU has to communicate with peripherals
  - Keyboards
  - Monitors
  - Disks
  - Ethernet cards
  - ...

<!--
The computer systems is just the same!

In the last example, we ourselves are like cpu, and the kettle is like a peripheral.

Just like we should turn the kettle off when it is boiled.

The cpu also should handle some events that occur on the peripherals.

For example, when we press the keyboard, the cpu must know this and display the character we pressed on the screen.
-->

---

# Polling - The Old And "Silly" Approach

<v-click>

<img src="/images/cpu-waiting-for-peripheral.png" alt="手绘一个人坐在烧水壶旁边呆呆地等，人头上放个 CPU，水壶上放个外设" align="right" style="width: 60%;" />

</v-click>

- Busy waiting
- Easy to implement
- Cannot do other things during polling

<!--
In computer systems. There are also two ways to do it.

The first way is called "POLLING". It is an silly and naive approach. 

It's just like the first approach of the last example. The cpu just keeps watching at the Peripheral waiting for a event to occur at the peripheral.

Apparently, this approach is very easy to implement but the cpu cannot do other things during polling.
-->

---

# Interrupt - A Smarter Approach

<v-click>

<img src="/images/cpu-peripheral-interrupt.png" alt="手绘水壶外设+哨子中断控制器+书房CPU" align="right" style="width: 60%;" />

</v-click>

- CPU can do other things during I/O
- Peripherals interrupt CPU when completed

<!--
So In order to overcome these shortcomings, the interrupt is invented!

Just like the second approach of the last example. the interrupt is like a whistle. When an event occurs at a peripheral, the peripheral will send an interrupt to the cpu. When the cpu receives this interrupt, it knows that it's time to handle this event.

So that using this approach, the cpu could do other things during I/O. This can lead to a huge performance improvement.

Next, my partenr will discuss some issues of the interrupt mechanism.
-->

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

<img src="/images/pouring-water.png" alt="手绘人在倒水" align="right" style="width: 50%;" />

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
