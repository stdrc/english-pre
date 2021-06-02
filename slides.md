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

# Back To The Example

<!-- 这一页感觉可以不要 -->

<v-clicks>

- Why not setup a timer on my phone
  - and check the water when time is up?
- This is also interrupt!

</v-clicks>

---
layout: center
---

# Is That Perfect?

<v-click>

# No!

</v-click>
