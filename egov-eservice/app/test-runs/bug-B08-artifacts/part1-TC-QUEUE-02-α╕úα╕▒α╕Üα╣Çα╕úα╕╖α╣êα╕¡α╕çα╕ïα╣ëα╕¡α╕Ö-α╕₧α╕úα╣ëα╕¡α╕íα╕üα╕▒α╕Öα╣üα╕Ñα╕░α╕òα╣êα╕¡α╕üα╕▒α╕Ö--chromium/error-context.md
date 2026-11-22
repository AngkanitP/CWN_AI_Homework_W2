# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-QUEUE-02 รับเรื่องซ้อน (พร้อมกันและต่อกัน)
- Location: tests/part1.spec.ts:1076:1

# Error details

```
Error: กดรับเรื่องพร้อมกัน 2 คน: สำเร็จ 1 และได้ ALREADY_CLAIMED 1

expect(received).toEqual(expected) // deep equality

- Expected  - 1
+ Received  + 1

  Array [
-   "error: มีเจ้าหน้าที่รับเรื่องนี้แล้ว",
+   "success",
    "success",
  ]
```

# Page snapshot

```yaml
- generic [active] [ref=f1e1]:
  - link "ข้ามไปเนื้อหาหลัก" [ref=f1e2] [cursor=pointer]:
    - /url: "#main"
  - banner [ref=f1e3]:
    - generic [ref=f1e4]:
      - link "e-Service กลาง เทศบาลนครตัวอย่าง" [ref=f1e5] [cursor=pointer]:
        - /url: /
      - navigation "เมนูหลัก" [ref=f1e6]:
        - list [ref=f1e7]:
          - listitem [ref=f1e8]:
            - link "คิวงาน" [ref=f1e9] [cursor=pointer]:
              - /url: /officer/queue
      - generic [ref=f1e10]:
        - generic [ref=f1e11]:
          - text: เจ้าหน้าที่ทะเบียน 2
          - generic [ref=f1e12]: เจ้าหน้าที่
        - link "แจ้งเตือน 1" [ref=f1e13] [cursor=pointer]:
          - /url: /notifications
          - text: แจ้งเตือน
          - generic [ref=f1e14]: "1"
        - button "ออกจากระบบ" [ref=f1e16] [cursor=pointer]
  - main [ref=f1e17]:
    - status [ref=f1e19]: รับเรื่อง EG-2569-000028 แล้ว
    - heading "คิวงาน" [level=1] [ref=f1e20]
    - paragraph [ref=f1e21]: คิวงานฝ่ายทะเบียน · เรียงตามกำหนดเสร็จเร็วสุดก่อน (เท่ากันเรียงเลขคำขอ)
    - paragraph [ref=f1e22]:
      - text: "งานในมือของฉัน:"
      - strong [ref=f1e23]: "9"
      - text: / 10 เรื่อง
    - generic [ref=f1e24]:
      - generic [ref=f1e25]:
        - generic [ref=f1e26]: แสดงรายการ
        - combobox "แสดงรายการ" [ref=f1e27]:
          - option "ทั้งหมด" [selected]
          - option "ยังไม่มีผู้รับ"
          - option "ของฉัน"
      - button "กรอง" [ref=f1e29] [cursor=pointer]
    - region "ตารางคิวงาน" [ref=f1e30]:
      - table [ref=f1e31]:
        - rowgroup [ref=f1e32]:
          - row [ref=f1e33]:
            - columnheader "เลขคำขอ" [ref=f1e34]
            - columnheader "บริการ" [ref=f1e35]
            - columnheader "ผู้ยื่น" [ref=f1e36]
            - columnheader "เลขบัตร" [ref=f1e37]
            - columnheader "สถานะ" [ref=f1e38]
            - columnheader "กำหนดเสร็จ" [ref=f1e39]
            - columnheader "ระดับเตือน" [ref=f1e40]
            - columnheader "ผู้ถือเรื่อง" [ref=f1e41]
            - columnheader "ดำเนินการ" [ref=f1e42]
        - rowgroup [ref=f1e43]:
          - row [ref=f1e44]:
            - cell [ref=f1e45]:
              - link "EG-2569-000020" [ref=f1e46] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000020
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e47]
            - cell "สมชาย ใจดี" [ref=f1e48]
            - cell "X-XXXX-XXXXX-45-6" [ref=f1e49]
            - cell "กำลังตรวจสอบ" [ref=f1e50]
            - cell [ref=f1e52]:
              - time [ref=f1e53]: 30 พ.ย. 2569 16:30
            - cell "เกินกำหนด" [ref=f1e54]
            - cell "off.reg1" [ref=f1e56]
            - cell [ref=f1e57]
          - row [ref=f1e58]:
            - cell [ref=f1e59]:
              - link "EG-2569-000022" [ref=f1e60] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000022
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e61]
            - cell "สมหญิง รักไทย" [ref=f1e62]
            - cell "X-XXXX-XXXXX-65-9" [ref=f1e63]
            - cell "กำลังตรวจสอบ" [ref=f1e64]
            - cell [ref=f1e66]:
              - time [ref=f1e67]: 1 ธ.ค. 2569 16:30
            - cell "ใกล้ครบกำหนด" [ref=f1e68]
            - cell "off.reg1" [ref=f1e70]
            - cell [ref=f1e71]
          - row [ref=f1e72]:
            - cell [ref=f1e73]:
              - link "EG-2569-000024" [ref=f1e74] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000024
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e75]
            - cell "ปิติ มีสุข" [ref=f1e76]
            - cell "X-XXXX-XXXXX-01-5" [ref=f1e77]
            - cell "ส่งคำขอแล้ว" [ref=f1e78]
            - cell [ref=f1e80]:
              - time [ref=f1e81]: 2 ธ.ค. 2569 16:30
            - cell "ใกล้ครบกำหนด" [ref=f1e82]
            - cell [ref=f1e84]
            - cell [ref=f1e85]:
              - button "รับเรื่อง EG-2569-000024" [ref=f1e87] [cursor=pointer]: รับเรื่อง
          - row [ref=f1e88]:
            - cell [ref=f1e89]:
              - link "EG-2569-000023" [ref=f1e90] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000023
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e91]
            - cell "สมหญิง รักไทย" [ref=f1e92]
            - cell "X-XXXX-XXXXX-65-9" [ref=f1e93]
            - cell "กำลังตรวจสอบ" [ref=f1e94]
            - cell [ref=f1e96]:
              - time [ref=f1e97]: 3 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e98]
            - cell "off.reg1" [ref=f1e100]
            - cell [ref=f1e101]
          - row [ref=f1e102]:
            - cell [ref=f1e103]:
              - link "EG-2569-000025" [ref=f1e104] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000025
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e105]
            - cell "สมหญิง รักไทย" [ref=f1e106]
            - cell "X-XXXX-XXXXX-65-9" [ref=f1e107]
            - cell "กำลังตรวจสอบ" [ref=f1e108]
            - cell [ref=f1e110]:
              - time [ref=f1e111]: 3 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e112]
            - cell "off.reg2" [ref=f1e114]
            - cell [ref=f1e115]
          - row [ref=f1e116]:
            - cell [ref=f1e117]:
              - link "EG-2569-000026" [ref=f1e118] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000026
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e119]
            - cell "สมชาย ใจดี" [ref=f1e120]
            - cell "X-XXXX-XXXXX-45-6" [ref=f1e121]
            - cell "กำลังตรวจสอบ" [ref=f1e122]
            - cell [ref=f1e124]:
              - time [ref=f1e125]: 3 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e126]
            - cell "off.reg2" [ref=f1e128]
            - cell [ref=f1e129]
          - row [ref=f1e130]:
            - cell [ref=f1e131]:
              - link "EG-2569-000013" [ref=f1e132] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000013
            - cell "SV-02 ขออนุญาตประกอบกิจการ" [ref=f1e133]
            - cell "สมชาย ใจดี" [ref=f1e134]
            - cell "X-XXXX-XXXXX-45-6" [ref=f1e135]
            - cell "กำลังตรวจสอบ" [ref=f1e136]
            - cell [ref=f1e138]:
              - time [ref=f1e139]: 4 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e140]
            - cell "off.reg2" [ref=f1e142]
            - cell [ref=f1e143]
          - row [ref=f1e144]:
            - cell [ref=f1e145]:
              - link "EG-2569-000015" [ref=f1e146] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000015
            - cell "SV-02 ขออนุญาตประกอบกิจการ" [ref=f1e147]
            - cell "สมหญิง รักไทย" [ref=f1e148]
            - cell "X-XXXX-XXXXX-65-9" [ref=f1e149]
            - cell "กำลังตรวจสอบ" [ref=f1e150]
            - cell [ref=f1e152]:
              - time [ref=f1e153]: 4 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e154]
            - cell "off.reg2" [ref=f1e156]
            - cell [ref=f1e157]
          - row [ref=f1e158]:
            - cell [ref=f1e159]:
              - link "EG-2569-000027" [ref=f1e160] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000027
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e161]
            - cell "ปิติ มีสุข" [ref=f1e162]
            - cell "X-XXXX-XXXXX-01-5" [ref=f1e163]
            - cell "กำลังตรวจสอบ" [ref=f1e164]
            - cell [ref=f1e166]:
              - time [ref=f1e167]: 4 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e168]
            - cell "off.reg2" [ref=f1e170]
            - cell [ref=f1e171]
          - row [ref=f1e172]:
            - cell [ref=f1e173]:
              - link "EG-2569-000028" [ref=f1e174] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000028
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e175]
            - cell "สมหญิง รักไทย" [ref=f1e176]
            - cell "X-XXXX-XXXXX-65-9" [ref=f1e177]
            - cell "กำลังตรวจสอบ" [ref=f1e178]
            - cell [ref=f1e180]:
              - time [ref=f1e181]: 4 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e182]
            - cell "off.reg1" [ref=f1e184]
            - cell [ref=f1e185]
          - row [ref=f1e186]:
            - cell [ref=f1e187]:
              - link "EG-2569-000029" [ref=f1e188] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000029
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e189]
            - cell "ปิติ มีสุข" [ref=f1e190]
            - cell "X-XXXX-XXXXX-01-5" [ref=f1e191]
            - cell "ส่งคำขอแล้ว" [ref=f1e192]
            - cell [ref=f1e194]:
              - time [ref=f1e195]: 4 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e196]
            - cell [ref=f1e198]
            - cell [ref=f1e199]:
              - button "รับเรื่อง EG-2569-000029" [ref=f1e201] [cursor=pointer]: รับเรื่อง
          - row [ref=f1e202]:
            - cell [ref=f1e203]:
              - link "EG-2569-000030" [ref=f1e204] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000030
            - cell "SV-01 ขอหนังสือรับรอง" [ref=f1e205]
            - cell "สมชาย ใจดี" [ref=f1e206]
            - cell "X-XXXX-XXXXX-45-6" [ref=f1e207]
            - cell "ส่งคำขอแล้ว" [ref=f1e208]
            - cell [ref=f1e210]:
              - time [ref=f1e211]: 4 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e212]
            - cell [ref=f1e214]
            - cell [ref=f1e215]:
              - button "รับเรื่อง EG-2569-000030" [ref=f1e217] [cursor=pointer]: รับเรื่อง
          - row [ref=f1e218]:
            - cell [ref=f1e219]:
              - link "EG-2569-000016" [ref=f1e220] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000016
            - cell "SV-02 ขออนุญาตประกอบกิจการ" [ref=f1e221]
            - cell "ปิติ มีสุข" [ref=f1e222]
            - cell "X-XXXX-XXXXX-01-5" [ref=f1e223]
            - cell "กำลังตรวจสอบ" [ref=f1e224]
            - cell [ref=f1e226]:
              - time [ref=f1e227]: 8 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e228]
            - cell "off.reg2" [ref=f1e230]
            - cell [ref=f1e231]
          - row [ref=f1e232]:
            - cell [ref=f1e233]:
              - link "EG-2569-000018" [ref=f1e234] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000018
            - cell "SV-02 ขออนุญาตประกอบกิจการ" [ref=f1e235]
            - cell "สมชาย ใจดี" [ref=f1e236]
            - cell "X-XXXX-XXXXX-45-6" [ref=f1e237]
            - cell "กำลังตรวจสอบ" [ref=f1e238]
            - cell [ref=f1e240]:
              - time [ref=f1e241]: 9 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e242]
            - cell "off.reg2" [ref=f1e244]
            - cell [ref=f1e245]
          - row [ref=f1e246]:
            - cell [ref=f1e247]:
              - link "EG-2569-000019" [ref=f1e248] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000019
            - cell "SV-02 ขออนุญาตประกอบกิจการ" [ref=f1e249]
            - cell "สมหญิง รักไทย" [ref=f1e250]
            - cell "X-XXXX-XXXXX-65-9" [ref=f1e251]
            - cell "อนุมัติ" [ref=f1e252]
            - cell [ref=f1e254]:
              - time [ref=f1e255]: 9 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e256]
            - cell [ref=f1e258]
            - cell [ref=f1e259]
          - row [ref=f1e260]:
            - cell [ref=f1e261]:
              - link "EG-2569-000012" [ref=f1e262] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000012
            - cell "SV-03 ขออนุญาตก่อสร้าง/ต่อเติมอาคาร ขั้นตอน 1/3 · ฝ่ายทะเบียน" [ref=f1e263]: SV-03 ขออนุญาตก่อสร้าง/ต่อเติมอาคารขั้นตอน 1/3 · ฝ่ายทะเบียน
            - cell "ปิติ มีสุข" [ref=f1e264]
            - cell "X-XXXX-XXXXX-01-5" [ref=f1e265]
            - cell "กำลังตรวจสอบ" [ref=f1e266]
            - cell [ref=f1e268]:
              - time [ref=f1e269]: 11 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e270]
            - cell "off.reg2" [ref=f1e272]
            - cell [ref=f1e273]
          - row [ref=f1e274]:
            - cell [ref=f1e275]:
              - link "EG-2569-000021" [ref=f1e276] [cursor=pointer]:
                - /url: /officer/cases/EG-2569-000021
            - cell "SV-02 ขออนุญาตประกอบกิจการ" [ref=f1e277]
            - cell "สมหญิง รักไทย" [ref=f1e278]
            - cell "X-XXXX-XXXXX-65-9" [ref=f1e279]
            - cell "กำลังตรวจสอบ" [ref=f1e280]
            - cell [ref=f1e282]:
              - time [ref=f1e283]: 11 ธ.ค. 2569 16:30
            - cell "ปกติ" [ref=f1e284]
            - cell "off.reg2" [ref=f1e286]
            - cell [ref=f1e287]
  - contentinfo [ref=f1e288]:
    - paragraph [ref=f1e289]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  1004 |   expect(old.caseNo).toBe(caseNo(31));
  1005 |   expect(old.paidAt).toBe('2026-12-31T23:59:00+07:00');
  1006 | });
  1007 | 
  1008 | // ═══════════════════════════════════ QUEUE ═══════════════════════════════════
  1009 | 
  1010 | const REGISTRY_ORDER = [20, 22, 24, 23, 25, 26, 13, 15, 27, 28, 29, 30, 16, 18, 19, 12, 21].map((n) => caseNo(n));
  1011 | 
  1012 | test('TC-QUEUE-01 ลำดับคิวและขอบเขตแผนก', async ({ browser }) => {
  1013 |   await reset();
  1014 | 
  1015 |   await test.step('off.reg1 filter all', async () => {
  1016 |     const { page: p, api } = await staffSession(browser, 'off.reg1');
  1017 |     await p.goto('/officer/queue');
  1018 |     await expect(tid(p, 'queue-filter')).toHaveValue('all');
  1019 |     await expect(tid(p, 'queue-row')).toHaveCount(17);
  1020 |     expect(await queueOrder(p)).toEqual(REGISTRY_ORDER);
  1021 |     const levels = await texts(tid(p, 'row-sla-level'));
  1022 |     expect(levels.slice(0, 3)).toEqual(['เกินกำหนด', 'ใกล้ครบกำหนด', 'ใกล้ครบกำหนด']);
  1023 |     const masked = await texts(tid(p, 'row-id-masked'));
  1024 |     expect(masked).toHaveLength(17);
  1025 |     for (const m of masked) expect(m).toMatch(/^X-XXXX-XXXXX-\d{2}-\d$/);
  1026 |     await expect(tid(p, 'claim-btn')).toHaveCount(4);
  1027 |     expect(await claimableRows(p)).toEqual([24, 28, 29, 30].map((n) => caseNo(n)));
  1028 |     await expect(tid(p, 'workload-count')).toHaveText('3');
  1029 |     for (const n of [17, 11, 14, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]) await expect(queueRow(p, caseNo(n))).toHaveCount(0);
  1030 | 
  1031 |     await uiQueueFilter(p, 'unclaimed');
  1032 |     await expect(tid(p, 'queue-row')).toHaveCount(4);
  1033 |     expect(await queueOrder(p)).toEqual([24, 28, 29, 30].map((n) => caseNo(n)));
  1034 |     await uiQueueFilter(p, 'mine');
  1035 |     await expect(tid(p, 'queue-row')).toHaveCount(3);
  1036 |     expect(await queueOrder(p)).toEqual([20, 22, 23].map((n) => caseNo(n)));
  1037 |     await expect(tid(p, 'workload-count')).toHaveText('3');
  1038 | 
  1039 |     expect((await queueItems(api, 'all')).map((i) => i.caseNo)).toEqual(REGISTRY_ORDER);
  1040 |     expect((await queueItems(api, 'unclaimed')).map((i) => i.caseNo)).toEqual([24, 28, 29, 30].map((n) => caseNo(n)));
  1041 |     expect((await queueItems(api, 'mine')).map((i) => i.caseNo)).toEqual([20, 22, 23].map((n) => caseNo(n)));
  1042 |   });
  1043 | 
  1044 |   await test.step('off.reg2 filter mine', async () => {
  1045 |     const { page: p, api } = await staffSession(browser, 'off.reg2');
  1046 |     await p.goto('/officer/queue');
  1047 |     await uiQueueFilter(p, 'mine');
  1048 |     const mine = [25, 26, 13, 15, 27, 16, 18, 12, 21].map((n) => caseNo(n));
  1049 |     await expect(tid(p, 'queue-row')).toHaveCount(9);
  1050 |     expect(await queueOrder(p)).toEqual(mine);
  1051 |     await expect(tid(p, 'workload-count')).toHaveText('9');
  1052 |     expect((await queueItems(api, 'mine')).map((i) => i.caseNo)).toEqual(mine);
  1053 |   });
  1054 | 
  1055 |   await test.step('off.works1 เห็นเฉพาะโยธา', async () => {
  1056 |     const { page: p, api } = await staffSession(browser, 'off.works1');
  1057 |     await p.goto('/officer/queue');
  1058 |     await expect(tid(p, 'queue-row')).toHaveCount(1);
  1059 |     expect(await queueOrder(p)).toEqual([caseNo(10)]);
  1060 |     expect((await queueItems(api, 'all')).map((i) => i.caseNo)).toEqual([caseNo(10)]);
  1061 |   });
  1062 | 
  1063 |   await test.step('head1 เห็นทุกแผนก อ่านอย่างเดียว', async () => {
  1064 |     const { page: p, api } = await staffSession(browser, 'head1');
  1065 |     await p.goto('/officer/queue');
  1066 |     await expect(tid(p, 'queue-row')).toHaveCount(18);
  1067 |     const order = await queueOrder(p);
  1068 |     const i = order.indexOf(caseNo(10));
  1069 |     expect(order.slice(i, i + 4)).toEqual([10, 23, 25, 26].map((n) => caseNo(n)));
  1070 |     expect(order).toEqual([20, 22, 24, 10, 23, 25, 26, 13, 15, 27, 28, 29, 30, 16, 18, 19, 12, 21].map((n) => caseNo(n)));
  1071 |     await expect(tid(p, 'claim-btn')).toHaveCount(0);
  1072 |     expect(await queueItems(api, 'all')).toHaveLength(18);
  1073 |   });
  1074 | });
  1075 | 
  1076 | test('TC-QUEUE-02 รับเรื่องซ้อน (พร้อมกันและต่อกัน)', async ({ browser }) => {
  1077 |   test.setTimeout(240_000);
  1078 | 
  1079 |   /** จำนวนแถว CLAIM ใน Audit ของคำขอ (ตรวจผ่าน audit1) */
  1080 |   async function claimAuditCount(no: string): Promise<number> {
  1081 |     const auditor = await loginStaff('audit1');
  1082 |     return (await auditItems(auditor, { event: 'CLAIM' })).filter((a) => a.caseNo === no).length;
  1083 |   }
  1084 | 
  1085 |   await test.step('ส่วน 1 พร้อมกัน (UI 2 context)', async () => {
  1086 |     await reset();
  1087 |     const NO = caseNo(28);
  1088 |     const A = await staffSession(browser, 'off.reg1');
  1089 |     const B = await staffSession(browser, 'off.reg2');
  1090 |     await Promise.all([A.page.goto('/officer/queue'), B.page.goto('/officer/queue')]);
  1091 |     const btnA = queueRow(A.page, NO).getByTestId('claim-btn');
  1092 |     const btnB = queueRow(B.page, NO).getByTestId('claim-btn');
  1093 |     await expect(btnA).toBeVisible();
  1094 |     await expect(btnB).toBeVisible();
  1095 | 
  1096 |     await Promise.all([withMutation(A.page, () => btnA.click()), withMutation(B.page, () => btnB.click())]);
  1097 | 
  1098 |     // ผลบนจอของทั้งสองคนต้องเป็น สำเร็จ 1 + ALREADY_CLAIMED 1 (ตรวจเป็นค่า → B08 ล้มที่ค่า ไม่ใช่หา action-error ไม่เจอ)
  1099 |     const outcome = async (p: Page): Promise<string> => {
  1100 |       await expect(tid(p, 'action-error').or(tid(p, 'action-success'))).toBeVisible();
  1101 |       return (await tid(p, 'action-error').count()) ? `error: ${(await tid(p, 'action-error').innerText()).trim()}` : 'success';
  1102 |     };
  1103 |     const outcomes = [await outcome(A.page), await outcome(B.page)].sort();
> 1104 |     expect(outcomes, 'กดรับเรื่องพร้อมกัน 2 คน: สำเร็จ 1 และได้ ALREADY_CLAIMED 1').toEqual([`error: ${MSG.ALREADY_CLAIMED}`, 'success']);
       |                                                                                     ^ Error: กดรับเรื่องพร้อมกัน 2 คน: สำเร็จ 1 และได้ ALREADY_CLAIMED 1
  1105 | 
  1106 |     const c = await getCase(A.api, NO);
  1107 |     expect(['off.reg1', 'off.reg2']).toContain(c.owner);
  1108 |     expect(c.status).toBe('IN_REVIEW');
  1109 |     const [win, lose] = c.owner === 'off.reg1' ? [A, B] : [B, A];
  1110 |     const winner = c.owner as StaffUser;
  1111 |     await expect(tid(lose.page, 'action-error')).toHaveText(MSG.ALREADY_CLAIMED);
  1112 |     await win.page.goto('/officer/queue');
  1113 |     await expect(queueRow(win.page, NO)).toHaveAttribute('data-owner', winner);
  1114 |     await expect(queueRow(win.page, NO).getByTestId('row-owner')).toHaveText(new RegExp(`${winner}|${STAFF[winner].name}`));
  1115 |     expect(await claimAuditCount(NO)).toBe(1);
  1116 |   });
  1117 | 
  1118 |   await test.step('ส่วน 2 พร้อมกัน 10 ครั้ง (API · RESET)', async () => {
  1119 |     await reset();
  1120 |     const NO = caseNo(29);
  1121 |     const reg1 = await loginStaff('off.reg1');
  1122 |     const reg2 = await loginStaff('off.reg2');
  1123 |     const calls = [reg1, reg2, reg1, reg2, reg1, reg2, reg1, reg2, reg1, reg2].map((api) => claimRaw(api, NO));
  1124 |     const res = await Promise.all(calls);
  1125 |     const bodies = await Promise.all(res.map((r) => bodyOf(r)));
  1126 |     const ok = res.filter((r) => r.status() === 200);
  1127 |     expect(ok, JSON.stringify(res.map((r, i) => [r.status(), bodies[i].code]))).toHaveLength(1);
  1128 |     bodies.forEach((b, i) => {
  1129 |       if (res[i].status() !== 200) {
  1130 |         expect(res[i].status()).toBe(409);
  1131 |         expect(b.code).toBe('ALREADY_CLAIMED');
  1132 |       }
  1133 |     });
  1134 |     const winnerBody = bodies[res.findIndex((r) => r.status() === 200)];
  1135 |     const c = await getCase(reg1, NO);
  1136 |     expect(c.owner).toBe(winnerBody.owner);
  1137 |     expect(c.status).toBe('IN_REVIEW');
  1138 |     expect(await claimAuditCount(NO)).toBe(1);
  1139 |   });
  1140 | 
  1141 |   await test.step('ส่วน 3 ต่อกัน (API · RESET) — จับ B08', async () => {
  1142 |     await reset();
  1143 |     const NO = caseNo(29);
  1144 |     const reg1 = await loginStaff('off.reg1');
  1145 |     const reg2 = await loginStaff('off.reg2');
  1146 |     const first = await claim(reg1, NO);
  1147 |     expect(first.owner).toBe('off.reg1');
  1148 |     const second = await expectApi(claimRaw(reg2, NO), 409, 'ALREADY_CLAIMED');
  1149 |     expect(second.message).toBe(MSG.ALREADY_CLAIMED);
  1150 |     expect((await getCase(reg2, NO)).owner).toBe('off.reg1');
  1151 |     expect(await queueItems(reg2, 'mine')).toHaveLength(9);
  1152 |     const s2 = await staffSession(browser, 'off.reg2');
  1153 |     await expectWorkload(s2.page, 9);
  1154 |     await expectApi(claimRaw(reg1, NO), 409, 'ALREADY_CLAIMED');
  1155 |     expect((await getCase(reg1, NO)).owner).toBe('off.reg1');
  1156 |     expect(await claimAuditCount(NO)).toBe(1);
  1157 |   });
  1158 | });
  1159 | 
  1160 | test('TC-QUEUE-03 งานในมือสูงสุด 10', async ({ browser }) => {
  1161 |   test.setTimeout(240_000);
  1162 |   await reset();
  1163 |   let s = await staffSession(browser, 'off.reg2');
  1164 |   let p = s.page;
  1165 |   const claimUi = async (n: number) => {
  1166 |     await p.goto('/officer/queue');
  1167 |     await withMutation(p, () => queueRow(p, caseNo(n)).getByTestId('claim-btn').click());
  1168 |   };
  1169 | 
  1170 |   // 1
  1171 |   await expectWorkload(p, 9);
  1172 |   // 2 ครั้งที่ 10
  1173 |   await claimUi(28);
  1174 |   await expect(tid(p, 'action-error')).toBeHidden();
  1175 |   await expectWorkload(p, 10);
  1176 |   expect((await getCase(s.api, caseNo(28))).owner).toBe('off.reg2');
  1177 |   // 3 ครั้งที่ 11 → เพดาน
  1178 |   await claimUi(29);
  1179 |   await expect(tid(p, 'action-error')).toHaveText(MSG.WORKLOAD_LIMIT);
  1180 |   const lim = await expectApi(claimRaw(s.api, caseNo(29)), 409, 'WORKLOAD_LIMIT');
  1181 |   expect(lim.message).toBe(MSG.WORKLOAD_LIMIT);
  1182 |   const c29 = await getCase(s.api, caseNo(29));
  1183 |   expect(c29.status).toBe('SUBMITTED');
  1184 |   expect(c29.owner || null).toBeNull();
  1185 |   await expectWorkload(p, 10);
  1186 |   // 4 อนุมัติ …000025 (SV-01 ของตัวเอง) → APPROVED ไม่นับ
  1187 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1188 |   await tid(p, 'approve-btn').click();
  1189 |   await expectStatus(p, 'APPROVED');
  1190 |   await expectWorkload(p, 9);
  1191 |   // 5
  1192 |   await claimUi(29);
  1193 |   await expectWorkload(p, 10);
  1194 |   expect((await getCase(s.api, caseNo(29))).owner).toBe('off.reg2');
  1195 |   // 6 off.reg1 (งานในมือ 3) ไม่ติดเพดาน
  1196 |   const reg1 = await loginStaff('off.reg1');
  1197 |   expect((await claim(reg1, caseNo(30))).owner).toBe('off.reg1');
  1198 | 
  1199 |   // 7 RESET · ตีกลับ …000025 → NEED_FIX ไม่นับ
  1200 |   await reset();
  1201 |   s = await staffSession(browser, 'off.reg2');
  1202 |   p = s.page;
  1203 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1204 |   await tid(p, 'return-btn').click();
```