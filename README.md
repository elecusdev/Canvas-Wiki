# Discord.js Canvas Complete Guide - V1 

## Örnekler

<div align="center">

<img src="https://cdn.discordapp.com/attachments/1498756764370473112/1513260279415177349/image.png" width="800">

<br><br>

<img src="https://media.discordapp.net/attachments/1498756764370473112/1513260279687938259/image.png?ex=6a2714f5&is=6a25c375&hm=04d498854cdc5f369c1e3198ade3b0eff68622f916859ebc6f27f026cd7f8277&=&format=webp&quality=lossless" width="800">

<br><br>

<img src="https://media.discordapp.net/attachments/1498756764370473112/1513260279994253512/image.png?ex=6a2714f5&is=6a25c375&hm=1fd5904082321b5a8204d520a077884944009bc59da01b0d7a22a3dc2d1aafeb&=&format=webp&quality=lossless" width="800">

<br><br>

<img src="https://media.discordapp.net/attachments/1498756764370473112/1513260280765747371/image.png?ex=6a2714f5&is=6a25c375&hm=54425f956ad40ea0dbea4187ef1802ab1b94ff08a1846aeedd1df75c334484e5&=&format=webp&quality=lossless" width="800">

<br><br>

<img src="https://media.discordapp.net/attachments/1498756764370473112/1513260281139040287/image.png?ex=6a2714f6&is=6a25c376&hm=8291bf231a5272a834603efd41382d66400a7905471f87e58b188ba2306c42a0&=&format=webp&quality=lossless" width="800">

<br><br>

<img src="https://media.discordapp.net/attachments/1498756764370473112/1513260281575510217/profile.png?ex=6a2714f6&is=6a25c376&hm=142894393572870047a3ed7e119ae4fcf64654d22c7c438b06d90b00a49596c5&=&format=webp&quality=lossless" width="800">

</div> 



----
> Created by Elecus

---

# Introduction

Canvas, Discord.js projelerinde dinamik görseller oluşturmak için kullanılan en güçlü çözümlerden biridir. Profil kartları, seviye sistemleri, hoş geldin kartları, liderlik tabloları ve özel görsel içerikler oluşturabilirsiniz.

Bu rehber başlangıç seviyesinden ileri seviyeye kadar Canvas kullanımını öğretmek amacıyla hazırlanmıştır.

---

# What is Canvas?

Canvas, Node.js içerisinde çalışan bir grafik işleme kütüphanesidir.

Canvas sayesinde:

- PNG oluşturabilirsiniz
- JPEG oluşturabilirsiniz
- Dinamik profil kartları yapabilirsiniz
- Avatar düzenleyebilirsiniz
- Yazılar ekleyebilirsiniz
- Özel şekiller çizebilirsiniz
- Filtreler uygulayabilirsiniz

---

# Installation

## Canvas

```bash
npm install canvas
```

## Discord.js

```bash
npm install discord.js
```

---

# First Canvas

```js
const { createCanvas } = require("canvas");

const canvas = createCanvas(800, 400);
const ctx = canvas.getContext("2d");
```

---

# Background Color

```js
ctx.fillStyle = "#2B2D31";
ctx.fillRect(0, 0, canvas.width, canvas.height);
```

---

# Saving Image

```js
const fs = require("fs");

fs.writeFileSync(
    "image.png",
    canvas.toBuffer("image/png")
);
```

---

# Sending Image In Discord

```js
const {
    AttachmentBuilder
} = require("discord.js");

const attachment =
new AttachmentBuilder(
    canvas.toBuffer(),
    {
        name: "image.png"
    }
);

await interaction.reply({
    files: [attachment]
});
```

---

# Drawing Rectangles

```js
ctx.fillStyle = "#5865F2";

ctx.fillRect(
    50,
    50,
    300,
    100
);
```

---

# Stroke Rectangles

```js
ctx.strokeStyle = "#ffffff";

ctx.lineWidth = 5;

ctx.strokeRect(
    50,
    50,
    300,
    100
);
```

---

# Drawing Circles

```js
ctx.beginPath();

ctx.arc(
    200,
    200,
    100,
    0,
    Math.PI * 2
);

ctx.fill();
```

---

# Circle Outline

```js
ctx.beginPath();

ctx.arc(
    200,
    200,
    100,
    0,
    Math.PI * 2
);

ctx.stroke();
```

---

# Drawing Lines

```js
ctx.beginPath();

ctx.moveTo(0, 0);

ctx.lineTo(
    500,
    500
);

ctx.stroke();
```

---

# Text Basics

```js
ctx.font =
"40px Arial";

ctx.fillStyle =
"#ffffff";

ctx.fillText(
    "Hello World",
    100,
    100
);
```

---

# Text Align

```js
ctx.textAlign =
"center";

ctx.fillText(
    "Centered",
    400,
    200
);
```

---

# Text Baseline

```js
ctx.textBaseline =
"middle";
```

---

# Custom Fonts

```js
const {
 registerFont
} = require("canvas");

registerFont(
 "./fonts/Poppins.ttf",
 {
   family: "Poppins"
 }
);
```

---

# Using Font

```js
ctx.font =
"50px Poppins";
```

---

# Loading Images

```js
const {
 loadImage
} = require("canvas");
```

---

# Load Background

```js
const background =
await loadImage(
 "./images/bg.png"
);
```

---

# Draw Background

```js
ctx.drawImage(
 background,
 0,
 0,
 canvas.width,
 canvas.height
);
```

---

# Discord Avatar

```js
const avatar =
await loadImage(
 member.user
 .displayAvatarURL({
   extension: "png"
 })
);
```

---

# Draw Avatar

```js
ctx.drawImage(
 avatar,
 50,
 50,
 150,
 150
);
```

---

# Circular Avatar

```js
ctx.save();

ctx.beginPath();

ctx.arc(
125,
125,
75,
0,
Math.PI * 2
);

ctx.closePath();

ctx.clip();

ctx.drawImage(
 avatar,
 50,
 50,
 150,
 150
);

ctx.restore();
```

---

# Shadow Effect

```js
ctx.shadowColor =
"black";

ctx.shadowBlur =
20;
```

---

# Gradient Background

```js
const gradient =
ctx.createLinearGradient(
0,
0,
800,
0
);

gradient.addColorStop(
0,
"#5865F2"
);

gradient.addColorStop(
1,
"#7289DA"
);

ctx.fillStyle =
gradient;

ctx.fillRect(
0,
0,
800,
400
);
```

---

# Progress Bar

```js
ctx.fillStyle =
"#23272A";

ctx.fillRect(
100,
300,
500,
30
);

ctx.fillStyle =
"#5865F2";

ctx.fillRect(
100,
300,
250,
30
);
```

---

# Rounded Rectangle

```js
ctx.beginPath();

ctx.roundRect(
50,
50,
300,
150,
20
);

ctx.fill();
```

---

# User Profile Card

```js
ctx.fillStyle =
"#1E1F22";

ctx.fillRect(
0,
0,
800,
300
);

ctx.fillText(
member.user.username,
250,
120
);

ctx.fillText(
`ID: ${member.id}`,
250,
180
);
```

---

# Rank Card Structure

```text
+----------------------+
| Avatar               |
| Username             |
| Level                |
| XP Bar               |
+----------------------+
```

---

# Rank Card Example

```js
ctx.fillText(
`Level ${level}`,
250,
120
);

ctx.fillText(
`${xp}/${needXp}`,
250,
170
);
```

---

# Welcome Card

```js
ctx.fillText(
"Welcome",
400,
120
);

ctx.fillText(
member.user.tag,
400,
180
);
```

---

# Leave Card

```js
ctx.fillText(
"Goodbye",
400,
150
);
```

---

# Server Statistics

```js
ctx.fillText(
`${guild.memberCount}`,
400,
250
);
```

---

# Drawing Icons

```js
const icon =
await loadImage(
"./icon.png"
);

ctx.drawImage(
icon,
700,
20,
50,
50
);
```

---

# Transparency

```js
ctx.globalAlpha =
0.5;
```

---

# Rotate Object

```js
ctx.save();

ctx.translate(
400,
200
);

ctx.rotate(
45 *
Math.PI /
180
);

ctx.restore();
```

---

# Blur Shadow

```js
ctx.shadowBlur =
50;
```

---

# Advanced Profile Layout

```text
+--------------------------------+
| Avatar     Username            |
|            About              |
|            Badges             |
|                                |
| XP Progress Bar               |
+--------------------------------+
```

---

# Dynamic Username

```js
ctx.fillText(
member.user.username,
220,
90
);
```

---

# Dynamic Discriminator

```js
ctx.fillText(
member.user.tag,
220,
130
);
```

---

# Dynamic Join Date

```js
ctx.fillText(
member.joinedAt
.toDateString(),
220,
170
);
```

---

# XP Percentage

```js
const percent =
xp /
needXp *
100;
```

---

# XP Width

```js
const width =
500 *
(percent / 100);
```

---

# Draw XP

```js
ctx.fillRect(
100,
250,
width,
20
);
```

---

# Badge System

```js
const badges = [
 "Owner",
 "Developer",
 "Premium"
];
```

---

# Draw Badge

```js
badges.forEach(
(badge, i) => {
ctx.fillText(
 badge,
 220,
 220 + i * 30
);
});
```

---

# Error Handling

```js
try {

} catch(err) {
 console.log(err);
}
```

---

# Canvas Optimization

## Use Cached Images

```js
Map
Collection
QuickLRU
```

---

## Avoid Recreating Fonts

```js
registerFont(
 "./font.ttf",
 {
  family:"Poppins"
 }
);
```

Only once.

---

## Cache Backgrounds

```js
const bg =
await loadImage(
"./bg.png"
);
```

Load once.

---

# Common Mistakes

## Wrong Extension

```js
displayAvatarURL({
 extension:"png"
});
```

---

## Missing Await

```js
await loadImage(...)
```

---

## Wrong Path

```js
./assets/bg.png
```

---

# Folder Structure

```text
src/
├── commands
├── events
├── canvas
│   ├── rank.js
│   ├── welcome.js
│   ├── profile.js
│   └── leaderboard.js
├── assets
│   ├── fonts
│   ├── backgrounds
│   └── icons
└── index.js
```

---

# Recommended Canvas Projects

### Welcome System

- Avatar
- Username
- Server Name

---

### Rank System

- XP
- Level
- Progress Bar

---

### Profile System

- Bio
- Badges
- Statistics

---

### Leaderboard

- Top XP
- Top Messages
- Top Voice

---

### Ticket Transcript Cover

- Ticket Name
- User
- Date

---

### Music Card

- Song Name
- Duration
- Thumbnail

---

### Giveaway Banner

- Prize
- Host
- Winners

---

# Best Practices

- Cache images
- Cache fonts
- Optimize dimensions
- Use PNG for quality
- Compress large assets
- Avoid loading assets every command execution

---

# Useful Resources

- Discord.js Documentation
- Canvas Documentation
- MDN Canvas API

---

# Conclusion

Canvas ile Discord botlarınıza profesyonel seviyede görsel sistemler ekleyebilirsiniz.

Öğrendiğiniz başlıklar:

- Canvas kurulumu
- Şekiller
- Metinler
- Avatarlar
- Profil kartları
- Rank kartları
- Welcome kartları
- Gradientler
- Gölgeler
- Optimizasyon

Bu bilgilerle kendi gelişmiş Discord.js Canvas sistemlerinizi oluşturmaya başlayabilirsiniz.

---

Made with ❤️ by Elecus
