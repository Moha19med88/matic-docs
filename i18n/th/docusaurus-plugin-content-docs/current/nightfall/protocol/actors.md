---
id: actors
title: แอคเตอร์
sidebar_label: Actors
description: "ประเภทของแอคเตอร์บน Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - transactor
  - proposer
  - challenger
  - liquidity
  - provider
image: https://matic.network/banners/matic-network-16x9.png
---

มันมีแอคเตอร์อยู่ 4 แบบในเครือข่าย

- [ผู้ทำธุรกรรม](#transactor)
- [ผู้เสนอ](#proposer)
- [Challengers](#challenger)

## ผู้ทำธุรกรรม {#transactor}
ผู้ทำธุรกรรมลูกค้าประจำของการบริการพวกเขาต้องการทำธุรกรรม เช่น ฝาก โอน และถอนเงินเป็นการส่วนตัวลูกค้าเหล่านี้มักจะใช้วอลเล็ตเว็บหรือเซิร์ฟเวอร์เฉพาะ (ไคลเอนต์) เพื่อดำเนินการพิสูจน์ ZK ที่จำเป็นในการสร้างธุรกรรม

## ผู้เสนอ {#proposer}
ผู้เสนอรวบรวมธุรกรรมจากลูกค้าและเสนอการปรับปรุงใหม่ให้กับสถานะของสัญญาชิลด์ด้วยสถานะ เราหมายถึงเฉพาะตัวแปรการจัดเก็บที่เกี่ยวข้องกับธุรกรรม ZKPตัวทำให้เป็นโมฆะและรากข้อผูกมัดข้อเสนออัปเดตประกอบด้วยธุรกรรมหลายรายการ รวมกันเป็นบล็อกเลเยอร์ 2เฉพาะแฮชสถานะสุดท้ายที่จะมีขึ้นหลังจากธุรกรรมทั้งหมดในบล็อกได้รับการประมวลผลถูกจัดเก็บในเชนธุรกรรมจะสิ้นสุดหลังจากระยะเวลา 1 สัปดาห์

ทุกคนสามารถเป็นผู้เสนอได้ แต่ต้องวางสเตคบางส่วนสเตคมีจุดมุ่งหมายเพื่อจูงใจให้เกิดพฤติกรรมที่ดีผู้เสนอทำเงินโดยการให้บล็อกที่ถูกต้อง เก็บค่าธรรมเนียมจากผู้ทำธุรกรรมพวกมันค่อนข้างคล้ายกับนักขุด (Miners) ในบล็อคเชนทั่วไป

## Challenger {#challenger}
Challenger ดูแลความถูกต้องของบล็อกที่เสนอภายในหนึ่งสัปดาห์หลังจากส่งบล็อกใครๆ ก็เป็น Challenger ได้Challenger ใช้สเตคที่โพสต์โดยผู้เสนอเมื่อสร้างบล็อกของพวกเขาเมื่อพวกเขาส่งความท้าทายได้สำเร็จ


## หมายเหตุ {#notes}
ในการใช้งานอ้างอิงของ Polygon ทั้งผู้เสนอและ Challenger จะลดการทำงานบางอย่างลงในโมดูลทั่วไปหนึ่งโมดูลที่เรียกว่า Optimistโมดูล Optimist นี้ให้บริการบางอย่างแก่ผู้เสนอและผู้ท้าชิงจำนวนหนึ่ง เช่น การสร้างและบล็อกที่ท้าทาย(ผู้เสนอและ Challenger จะต้องลงนามในธุรกรรมเหล่านี้) การซิงโครไนซ์กับเหตุการณ์บล็อคเชน ฯลฯ

นอกเหนือจากแอคเตอร์ที่อธิบายข้างต้นแล้ว ยังมีนัแอคเตอร์เพิ่มเติมที่เรียกว่าลูกค้าลูกค้าทำหน้าที่เป็นบริการที่เชื่อถือได้ซึ่งรวบรวมธุรกรรมของผู้ใช้ ดำเนินการพิสูจน์ ZK ในนามของพวกเขา ส่งธุรกรรมไปยังผู้เสนอ ฟังเหตุการณ์บล็อคเชน ฯลฯ โดยสรุป ลูกค้าทำหน้าที่เป็นผู้ส่งต่อที่เชื่อถือได้สำหรับกลุ่มผู้ใช้ที่ต้องการออฟโหลด การคำนวณที่มีหลักฐานหนักและไว้วางใจซึ่งกันและกัน

ทางเลือกอื่นสำหรับลูกค้าคือการใช้กระเป๋าเงินของเบราว์เซอร์ ซึ่งเป็นบริการแบบไร้เซิร์ฟเวอร์ที่ Polygon ให้บริการวอลเล็ตนี้จัดการกิจกรรมการทำธุรกรรมทั้งหมดสำหรับผู้ใช้คนเดียวในขณะที่รักษาความเป็นส่วนตัว