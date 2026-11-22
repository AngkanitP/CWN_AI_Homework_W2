# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-QUEUE-02 รับเรื่องซ้อน (พร้อมกันและต่อกัน)
- Location: tests/part1.spec.ts:1076:1

# Error details

```
Error: expect(locator).toHaveText(expected) failed

Locator: getByTestId('action-error')
Expected: "มีเจ้าหน้าที่รับเรื่องนี้แล้ว"
Timeout: 7000ms
Error: element(s) not found

Call log:
  - Expect "toHaveText" getByTestId('action-error') with timeout 7000ms
  - waiting for getByTestId('action-error')

```

```yaml
- link "ข้ามไปเนื้อหาหลัก":
  - /url: "#main"
- banner:
  - link "e-Service กลาง เทศบาลนครตัวอย่าง":
    - /url: /
  - navigation "เมนูหลัก":
    - list:
      - listitem:
        - link "คิวงาน":
          - /url: /officer/queue
  - text: เจ้าหน้าที่ทะเบียน 1 เจ้าหน้าที่
  - link "แจ้งเตือน 3":
    - /url: /notifications
  - button "ออกจากระบบ"
- main:
  - status: รับเรื่อง EG-2569-000028 แล้ว
  - heading "คิวงาน" [level=1]
  - paragraph: คิวงานฝ่ายทะเบียน · เรียงตามกำหนดเสร็จเร็วสุดก่อน (เท่ากันเรียงเลขคำขอ)
  - paragraph:
    - text: "งานในมือของฉัน:"
    - strong: "4"
    - text: / 10 เรื่อง
  - text: แสดงรายการ
  - combobox "แสดงรายการ":
    - option "ทั้งหมด" [selected]
    - option "ยังไม่มีผู้รับ"
    - option "ของฉัน"
  - button "กรอง"
  - region "ตารางคิวงาน":
    - table:
      - rowgroup:
        - row "เลขคำขอ บริการ ผู้ยื่น เลขบัตร สถานะ กำหนดเสร็จ ระดับเตือน ผู้ถือเรื่อง ดำเนินการ":
          - columnheader "เลขคำขอ"
          - columnheader "บริการ"
          - columnheader "ผู้ยื่น"
          - columnheader "เลขบัตร"
          - columnheader "สถานะ"
          - columnheader "กำหนดเสร็จ"
          - columnheader "ระดับเตือน"
          - columnheader "ผู้ถือเรื่อง"
          - columnheader "ดำเนินการ"
      - rowgroup:
        - row "EG-2569-000020 SV-01 ขอหนังสือรับรอง สมชาย ใจดี X-XXXX-XXXXX-45-6 กำลังตรวจสอบ 30 พ.ย. 2569 16:30 เกินกำหนด off.reg1":
          - cell "EG-2569-000020":
            - link "EG-2569-000020":
              - /url: /officer/cases/EG-2569-000020
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "สมชาย ใจดี"
          - cell "X-XXXX-XXXXX-45-6"
          - cell "กำลังตรวจสอบ"
          - cell "30 พ.ย. 2569 16:30":
            - time: 30 พ.ย. 2569 16:30
          - cell "เกินกำหนด"
          - cell "off.reg1"
          - cell
        - row "EG-2569-000022 SV-01 ขอหนังสือรับรอง สมหญิง รักไทย X-XXXX-XXXXX-65-9 กำลังตรวจสอบ 1 ธ.ค. 2569 16:30 ใกล้ครบกำหนด off.reg1":
          - cell "EG-2569-000022":
            - link "EG-2569-000022":
              - /url: /officer/cases/EG-2569-000022
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "สมหญิง รักไทย"
          - cell "X-XXXX-XXXXX-65-9"
          - cell "กำลังตรวจสอบ"
          - cell "1 ธ.ค. 2569 16:30":
            - time: 1 ธ.ค. 2569 16:30
          - cell "ใกล้ครบกำหนด"
          - cell "off.reg1"
          - cell
        - row "EG-2569-000024 SV-01 ขอหนังสือรับรอง ปิติ มีสุข X-XXXX-XXXXX-01-5 ส่งคำขอแล้ว 2 ธ.ค. 2569 16:30 ใกล้ครบกำหนด รับเรื่อง EG-2569-000024":
          - cell "EG-2569-000024":
            - link "EG-2569-000024":
              - /url: /officer/cases/EG-2569-000024
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "ปิติ มีสุข"
          - cell "X-XXXX-XXXXX-01-5"
          - cell "ส่งคำขอแล้ว"
          - cell "2 ธ.ค. 2569 16:30":
            - time: 2 ธ.ค. 2569 16:30
          - cell "ใกล้ครบกำหนด"
          - cell
          - cell "รับเรื่อง EG-2569-000024":
            - button "รับเรื่อง EG-2569-000024": รับเรื่อง
        - row "EG-2569-000023 SV-01 ขอหนังสือรับรอง สมหญิง รักไทย X-XXXX-XXXXX-65-9 กำลังตรวจสอบ 3 ธ.ค. 2569 16:30 ปกติ off.reg1":
          - cell "EG-2569-000023":
            - link "EG-2569-000023":
              - /url: /officer/cases/EG-2569-000023
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "สมหญิง รักไทย"
          - cell "X-XXXX-XXXXX-65-9"
          - cell "กำลังตรวจสอบ"
          - cell "3 ธ.ค. 2569 16:30":
            - time: 3 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg1"
          - cell
        - row "EG-2569-000025 SV-01 ขอหนังสือรับรอง สมหญิง รักไทย X-XXXX-XXXXX-65-9 กำลังตรวจสอบ 3 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000025":
            - link "EG-2569-000025":
              - /url: /officer/cases/EG-2569-000025
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "สมหญิง รักไทย"
          - cell "X-XXXX-XXXXX-65-9"
          - cell "กำลังตรวจสอบ"
          - cell "3 ธ.ค. 2569 16:30":
            - time: 3 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000026 SV-01 ขอหนังสือรับรอง สมชาย ใจดี X-XXXX-XXXXX-45-6 กำลังตรวจสอบ 3 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000026":
            - link "EG-2569-000026":
              - /url: /officer/cases/EG-2569-000026
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "สมชาย ใจดี"
          - cell "X-XXXX-XXXXX-45-6"
          - cell "กำลังตรวจสอบ"
          - cell "3 ธ.ค. 2569 16:30":
            - time: 3 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000013 SV-02 ขออนุญาตประกอบกิจการ สมชาย ใจดี X-XXXX-XXXXX-45-6 กำลังตรวจสอบ 4 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000013":
            - link "EG-2569-000013":
              - /url: /officer/cases/EG-2569-000013
          - cell "SV-02 ขออนุญาตประกอบกิจการ"
          - cell "สมชาย ใจดี"
          - cell "X-XXXX-XXXXX-45-6"
          - cell "กำลังตรวจสอบ"
          - cell "4 ธ.ค. 2569 16:30":
            - time: 4 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000015 SV-02 ขออนุญาตประกอบกิจการ สมหญิง รักไทย X-XXXX-XXXXX-65-9 กำลังตรวจสอบ 4 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000015":
            - link "EG-2569-000015":
              - /url: /officer/cases/EG-2569-000015
          - cell "SV-02 ขออนุญาตประกอบกิจการ"
          - cell "สมหญิง รักไทย"
          - cell "X-XXXX-XXXXX-65-9"
          - cell "กำลังตรวจสอบ"
          - cell "4 ธ.ค. 2569 16:30":
            - time: 4 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000027 SV-01 ขอหนังสือรับรอง ปิติ มีสุข X-XXXX-XXXXX-01-5 กำลังตรวจสอบ 4 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000027":
            - link "EG-2569-000027":
              - /url: /officer/cases/EG-2569-000027
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "ปิติ มีสุข"
          - cell "X-XXXX-XXXXX-01-5"
          - cell "กำลังตรวจสอบ"
          - cell "4 ธ.ค. 2569 16:30":
            - time: 4 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000028 SV-01 ขอหนังสือรับรอง สมหญิง รักไทย X-XXXX-XXXXX-65-9 กำลังตรวจสอบ 4 ธ.ค. 2569 16:30 ปกติ off.reg1":
          - cell "EG-2569-000028":
            - link "EG-2569-000028":
              - /url: /officer/cases/EG-2569-000028
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "สมหญิง รักไทย"
          - cell "X-XXXX-XXXXX-65-9"
          - cell "กำลังตรวจสอบ"
          - cell "4 ธ.ค. 2569 16:30":
            - time: 4 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg1"
          - cell
        - row "EG-2569-000029 SV-01 ขอหนังสือรับรอง ปิติ มีสุข X-XXXX-XXXXX-01-5 ส่งคำขอแล้ว 4 ธ.ค. 2569 16:30 ปกติ รับเรื่อง EG-2569-000029":
          - cell "EG-2569-000029":
            - link "EG-2569-000029":
              - /url: /officer/cases/EG-2569-000029
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "ปิติ มีสุข"
          - cell "X-XXXX-XXXXX-01-5"
          - cell "ส่งคำขอแล้ว"
          - cell "4 ธ.ค. 2569 16:30":
            - time: 4 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell
          - cell "รับเรื่อง EG-2569-000029":
            - button "รับเรื่อง EG-2569-000029": รับเรื่อง
        - row "EG-2569-000030 SV-01 ขอหนังสือรับรอง สมชาย ใจดี X-XXXX-XXXXX-45-6 ส่งคำขอแล้ว 4 ธ.ค. 2569 16:30 ปกติ รับเรื่อง EG-2569-000030":
          - cell "EG-2569-000030":
            - link "EG-2569-000030":
              - /url: /officer/cases/EG-2569-000030
          - cell "SV-01 ขอหนังสือรับรอง"
          - cell "สมชาย ใจดี"
          - cell "X-XXXX-XXXXX-45-6"
          - cell "ส่งคำขอแล้ว"
          - cell "4 ธ.ค. 2569 16:30":
            - time: 4 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell
          - cell "รับเรื่อง EG-2569-000030":
            - button "รับเรื่อง EG-2569-000030": รับเรื่อง
        - row "EG-2569-000016 SV-02 ขออนุญาตประกอบกิจการ ปิติ มีสุข X-XXXX-XXXXX-01-5 กำลังตรวจสอบ 8 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000016":
            - link "EG-2569-000016":
              - /url: /officer/cases/EG-2569-000016
          - cell "SV-02 ขออนุญาตประกอบกิจการ"
          - cell "ปิติ มีสุข"
          - cell "X-XXXX-XXXXX-01-5"
          - cell "กำลังตรวจสอบ"
          - cell "8 ธ.ค. 2569 16:30":
            - time: 8 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000018 SV-02 ขออนุญาตประกอบกิจการ สมชาย ใจดี X-XXXX-XXXXX-45-6 กำลังตรวจสอบ 9 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000018":
            - link "EG-2569-000018":
              - /url: /officer/cases/EG-2569-000018
          - cell "SV-02 ขออนุญาตประกอบกิจการ"
          - cell "สมชาย ใจดี"
          - cell "X-XXXX-XXXXX-45-6"
          - cell "กำลังตรวจสอบ"
          - cell "9 ธ.ค. 2569 16:30":
            - time: 9 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000019 SV-02 ขออนุญาตประกอบกิจการ สมหญิง รักไทย X-XXXX-XXXXX-65-9 อนุมัติ 9 ธ.ค. 2569 16:30 ปกติ":
          - cell "EG-2569-000019":
            - link "EG-2569-000019":
              - /url: /officer/cases/EG-2569-000019
          - cell "SV-02 ขออนุญาตประกอบกิจการ"
          - cell "สมหญิง รักไทย"
          - cell "X-XXXX-XXXXX-65-9"
          - cell "อนุมัติ"
          - cell "9 ธ.ค. 2569 16:30":
            - time: 9 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell
          - cell
        - row "EG-2569-000012 SV-03 ขออนุญาตก่อสร้าง/ต่อเติมอาคาร ขั้นตอน 1/3 · ฝ่ายทะเบียน ปิติ มีสุข X-XXXX-XXXXX-01-5 กำลังตรวจสอบ 11 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000012":
            - link "EG-2569-000012":
              - /url: /officer/cases/EG-2569-000012
          - cell "SV-03 ขออนุญาตก่อสร้าง/ต่อเติมอาคาร ขั้นตอน 1/3 · ฝ่ายทะเบียน"
          - cell "ปิติ มีสุข"
          - cell "X-XXXX-XXXXX-01-5"
          - cell "กำลังตรวจสอบ"
          - cell "11 ธ.ค. 2569 16:30":
            - time: 11 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
        - row "EG-2569-000021 SV-02 ขออนุญาตประกอบกิจการ สมหญิง รักไทย X-XXXX-XXXXX-65-9 กำลังตรวจสอบ 11 ธ.ค. 2569 16:30 ปกติ off.reg2":
          - cell "EG-2569-000021":
            - link "EG-2569-000021":
              - /url: /officer/cases/EG-2569-000021
          - cell "SV-02 ขออนุญาตประกอบกิจการ"
          - cell "สมหญิง รักไทย"
          - cell "X-XXXX-XXXXX-65-9"
          - cell "กำลังตรวจสอบ"
          - cell "11 ธ.ค. 2569 16:30":
            - time: 11 ธ.ค. 2569 16:30
          - cell "ปกติ"
          - cell "off.reg2"
          - cell
- contentinfo:
  - paragraph: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  1003 |   const old = await getCase(api, caseNo(31));
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
  1098 |     const c = await getCase(A.api, NO);
  1099 |     expect(['off.reg1', 'off.reg2']).toContain(c.owner);
  1100 |     expect(c.status).toBe('IN_REVIEW');
  1101 |     const [win, lose] = c.owner === 'off.reg1' ? [A, B] : [B, A];
  1102 |     const winner = c.owner as StaffUser;
> 1103 |     await expect(tid(lose.page, 'action-error')).toHaveText(MSG.ALREADY_CLAIMED);
       |                                                  ^ Error: expect(locator).toHaveText(expected) failed
  1104 |     await win.page.goto('/officer/queue');
  1105 |     await expect(queueRow(win.page, NO)).toHaveAttribute('data-owner', winner);
  1106 |     await expect(queueRow(win.page, NO).getByTestId('row-owner')).toHaveText(new RegExp(`${winner}|${STAFF[winner].name}`));
  1107 |     expect(await claimAuditCount(NO)).toBe(1);
  1108 |   });
  1109 | 
  1110 |   await test.step('ส่วน 2 พร้อมกัน 10 ครั้ง (API · RESET)', async () => {
  1111 |     await reset();
  1112 |     const NO = caseNo(29);
  1113 |     const reg1 = await loginStaff('off.reg1');
  1114 |     const reg2 = await loginStaff('off.reg2');
  1115 |     const calls = [reg1, reg2, reg1, reg2, reg1, reg2, reg1, reg2, reg1, reg2].map((api) => claimRaw(api, NO));
  1116 |     const res = await Promise.all(calls);
  1117 |     const bodies = await Promise.all(res.map((r) => bodyOf(r)));
  1118 |     const ok = res.filter((r) => r.status() === 200);
  1119 |     expect(ok, JSON.stringify(res.map((r, i) => [r.status(), bodies[i].code]))).toHaveLength(1);
  1120 |     bodies.forEach((b, i) => {
  1121 |       if (res[i].status() !== 200) {
  1122 |         expect(res[i].status()).toBe(409);
  1123 |         expect(b.code).toBe('ALREADY_CLAIMED');
  1124 |       }
  1125 |     });
  1126 |     const winnerBody = bodies[res.findIndex((r) => r.status() === 200)];
  1127 |     const c = await getCase(reg1, NO);
  1128 |     expect(c.owner).toBe(winnerBody.owner);
  1129 |     expect(c.status).toBe('IN_REVIEW');
  1130 |     expect(await claimAuditCount(NO)).toBe(1);
  1131 |   });
  1132 | 
  1133 |   await test.step('ส่วน 3 ต่อกัน (API · RESET) — จับ B08', async () => {
  1134 |     await reset();
  1135 |     const NO = caseNo(29);
  1136 |     const reg1 = await loginStaff('off.reg1');
  1137 |     const reg2 = await loginStaff('off.reg2');
  1138 |     const first = await claim(reg1, NO);
  1139 |     expect(first.owner).toBe('off.reg1');
  1140 |     const second = await expectApi(claimRaw(reg2, NO), 409, 'ALREADY_CLAIMED');
  1141 |     expect(second.message).toBe(MSG.ALREADY_CLAIMED);
  1142 |     expect((await getCase(reg2, NO)).owner).toBe('off.reg1');
  1143 |     expect(await queueItems(reg2, 'mine')).toHaveLength(9);
  1144 |     const s2 = await staffSession(browser, 'off.reg2');
  1145 |     await expectWorkload(s2.page, 9);
  1146 |     await expectApi(claimRaw(reg1, NO), 409, 'ALREADY_CLAIMED');
  1147 |     expect((await getCase(reg1, NO)).owner).toBe('off.reg1');
  1148 |     expect(await claimAuditCount(NO)).toBe(1);
  1149 |   });
  1150 | });
  1151 | 
  1152 | test('TC-QUEUE-03 งานในมือสูงสุด 10', async ({ browser }) => {
  1153 |   test.setTimeout(240_000);
  1154 |   await reset();
  1155 |   let s = await staffSession(browser, 'off.reg2');
  1156 |   let p = s.page;
  1157 |   const claimUi = async (n: number) => {
  1158 |     await p.goto('/officer/queue');
  1159 |     await withMutation(p, () => queueRow(p, caseNo(n)).getByTestId('claim-btn').click());
  1160 |   };
  1161 | 
  1162 |   // 1
  1163 |   await expectWorkload(p, 9);
  1164 |   // 2 ครั้งที่ 10
  1165 |   await claimUi(28);
  1166 |   await expect(tid(p, 'action-error')).toBeHidden();
  1167 |   await expectWorkload(p, 10);
  1168 |   expect((await getCase(s.api, caseNo(28))).owner).toBe('off.reg2');
  1169 |   // 3 ครั้งที่ 11 → เพดาน
  1170 |   await claimUi(29);
  1171 |   await expect(tid(p, 'action-error')).toHaveText(MSG.WORKLOAD_LIMIT);
  1172 |   const lim = await expectApi(claimRaw(s.api, caseNo(29)), 409, 'WORKLOAD_LIMIT');
  1173 |   expect(lim.message).toBe(MSG.WORKLOAD_LIMIT);
  1174 |   const c29 = await getCase(s.api, caseNo(29));
  1175 |   expect(c29.status).toBe('SUBMITTED');
  1176 |   expect(c29.owner || null).toBeNull();
  1177 |   await expectWorkload(p, 10);
  1178 |   // 4 อนุมัติ …000025 (SV-01 ของตัวเอง) → APPROVED ไม่นับ
  1179 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1180 |   await tid(p, 'approve-btn').click();
  1181 |   await expectStatus(p, 'APPROVED');
  1182 |   await expectWorkload(p, 9);
  1183 |   // 5
  1184 |   await claimUi(29);
  1185 |   await expectWorkload(p, 10);
  1186 |   expect((await getCase(s.api, caseNo(29))).owner).toBe('off.reg2');
  1187 |   // 6 off.reg1 (งานในมือ 3) ไม่ติดเพดาน
  1188 |   const reg1 = await loginStaff('off.reg1');
  1189 |   expect((await claim(reg1, caseNo(30))).owner).toBe('off.reg1');
  1190 | 
  1191 |   // 7 RESET · ตีกลับ …000025 → NEED_FIX ไม่นับ
  1192 |   await reset();
  1193 |   s = await staffSession(browser, 'off.reg2');
  1194 |   p = s.page;
  1195 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1196 |   await tid(p, 'return-btn').click();
  1197 |   await tid(p, 'return-reason').fill('xxxxxxxxxx');
  1198 |   await tid(p, 'return-submit').click();
  1199 |   await expectStatus(p, 'NEED_FIX');
  1200 |   await expectWorkload(p, 8);
  1201 |   // 8
  1202 |   await claimUi(28);
  1203 |   await claimUi(29);
```