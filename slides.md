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

---

# Problem 1: Slower

<v-clicks>

- Much slower than polling
- Water boiling example:
  - Go back and forth between study room and kitchen
- Context switch

</v-clicks>

---

# Solution: Interrupt + Polling

<v-clicks>

- Network example:
  - Interrupt for the first packet
  - Polling for the remaining packets
- Realworld example:
  - Chatting on your phone

</v-clicks>

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

- Affect the performance of other tasks

</div>

---

# Solution: Top Half + Bottom Half

<v-clicks>

1. Do the most necessary things with interrupt masked - top half
2. Unmask interrupt
3. Finish the remaining work - bottom half

</v-clicks>

---
layout: center
---

# Thank You!
