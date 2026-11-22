# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-NOTI-02 ไม่แจ้งซ้ำ ข้ามระดับ และขั้นรออนุมัติ/รอออกเอกสาร
- Location: tests/part1.spec.ts:1486:1

# Error details

```
Error: expect(received).toEqual(expected) // deep equality

- Expected  - 1
+ Received  + 0

@@ -1,9 +1,8 @@
  Array [
    "EG-2569-000013:overdue",
    "EG-2569-000015:overdue",
-   "EG-2569-000016:near",
    "EG-2569-000024:overdue",
    "EG-2569-000025:overdue",
    "EG-2569-000026:overdue",
    "EG-2569-000027:overdue",
    "EG-2569-000028:overdue",
```

# Page snapshot

```yaml
- generic [active] [ref=e1]:
  - link "ข้ามไปเนื้อหาหลัก" [ref=e2] [cursor=pointer]:
    - /url: "#main"
  - banner [ref=e3]:
    - generic [ref=e4]:
      - link "e-Service กลาง เทศบาลนครตัวอย่าง" [ref=e5] [cursor=pointer]:
        - /url: /
      - navigation "เมนูหลัก" [ref=e6]:
        - list [ref=e7]:
          - listitem [ref=e8]:
            - link "คิวงาน" [ref=e9] [cursor=pointer]:
              - /url: /officer/queue
      - generic [ref=e10]:
        - generic [ref=e11]:
          - text: เจ้าหน้าที่โยธา 1
          - generic [ref=e12]: เจ้าหน้าที่
        - link "แจ้งเตือน 0" [ref=e13] [cursor=pointer]:
          - /url: /notifications
          - text: แจ้งเตือน
          - generic [ref=e14]: "0"
        - button "ออกจากระบบ" [ref=e16] [cursor=pointer]
  - main [ref=e17]:
    - heading "แจ้งเตือน" [level=1] [ref=e18]
    - paragraph [ref=e19]: แจ้งเมื่อคำขอที่เกี่ยวกับคุณเข้าระดับ "ใกล้ครบกำหนด" หรือ "เกินกำหนด" (ระดับละ 1 ครั้งต่อคำขอ)
    - paragraph [ref=e20]: ไม่มีแจ้งเตือน
  - contentinfo [ref=e21]:
    - paragraph [ref=e22]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  1421 |     const somying = await citizenSession(browser, ID.SOMYING);
  1422 |     await somying.page.goto(`/citizen/cases/${caseNo(1)}`);
  1423 |     await expectLevel(somying.page, 'closed');
  1424 | 
  1425 |     await setClock('2026-12-01T16:30:00+07:00');
  1426 |     await o.page.goto('/officer/queue');
  1427 |     await expect(queueRow(o.page, caseNo(22)).getByTestId('row-sla-level')).toHaveText('ใกล้ครบกำหนด');
  1428 |     await setClock('2026-12-01T16:31:00+07:00');
  1429 |     await o.page.goto('/officer/queue');
  1430 |     await expect(queueRow(o.page, caseNo(22)).getByTestId('row-sla-level')).toHaveText('เกินกำหนด');
  1431 |     await expect(queueRow(o.page, caseNo(22))).toHaveAttribute('data-sla-level', 'overdue');
  1432 |   });
  1433 | });
  1434 | 
  1435 | // ═══════════════════════════════════ NOTI ═══════════════════════════════════
  1436 | 
  1437 | /**
  1438 |  * TC-NOTI-01 ทั้งชุด: RESET → off.reg1 ล็อกอินที่ 09:00 (request แรก) → ตรวจผู้รับ 4 คน → CLOCK 16:31 → ตรวจเพิ่ม
  1439 |  * คืน session ของทุกคนเพื่อให้ TC-NOTI-02 ส่วน A ใช้ต่อ
  1440 |  */
  1441 | async function notiBaseline(browser: Browser): Promise<Record<'off.reg1' | 'off.reg2' | 'head1' | 'off.works1', { page: Page; api: APIRequestContext }>> {
  1442 |   await reset();
  1443 |   const reg1 = await staffSession(browser, 'off.reg1'); // request แรกหลัง reset ที่ 09:00
  1444 |   const reg2 = await staffSession(browser, 'off.reg2');
  1445 |   const head = await staffSession(browser, 'head1');
  1446 |   const works = await staffSession(browser, 'off.works1');
  1447 | 
  1448 |   const expected: Array<[{ page: Page; api: APIRequestContext }, string[], number]> = [
  1449 |     [reg1, keys([[24, 'near'], [22, 'near'], [20, 'overdue']]), 3],
  1450 |     [reg2, keys([[24, 'near']]), 1],
  1451 |     [head, keys([[20, 'overdue']]), 1],
  1452 |     [works, [], 0],
  1453 |   ];
  1454 |   for (const [s, exp, count] of expected) {
  1455 |     expect(await notificationKeys(s.api)).toEqual(exp);
  1456 |     await s.page.goto('/notifications');
  1457 |     await expect(tid(s.page, 'bell-count')).toHaveText(String(count));
  1458 |     await expect(tid(s.page, 'noti-item')).toHaveCount(count);
  1459 |     expect(await uiNotiKeys(s.page)).toEqual(exp);
  1460 |   }
  1461 |   await expect(rowBy(reg1.page, 'noti-item', 'data-case-no', caseNo(24))).toContainText('คำขอ EG-2569-000024 ใกล้ครบกำหนด');
  1462 |   await expect(rowBy(reg1.page, 'noti-item', 'data-case-no', caseNo(20))).toContainText('คำขอ EG-2569-000020 เกินกำหนด');
  1463 |   await expect(tid(works.page, 'noti-empty')).toHaveText(MSG.NOTI_EMPTY);
  1464 |   const apiItems = (await expectApi(reg1.api.get('/api/notifications'), 200)).items as any[];
  1465 |   expect(apiItems.find((n) => n.caseNo === caseNo(24))?.text).toBe('คำขอ EG-2569-000024 ใกล้ครบกำหนด');
  1466 |   expect(apiItems.find((n) => n.caseNo === caseNo(20))?.text).toBe('คำขอ EG-2569-000020 เกินกำหนด');
  1467 | 
  1468 |   // ต่อ: 16:31 + request ใด ๆ → …000022 เกินกำหนด
  1469 |   await setClock('2026-12-01T16:31:00+07:00');
  1470 |   await expectApi(reg1.api.get('/api/me'), 200);
  1471 |   expect(await notificationKeys(reg1.api)).toEqual(keys([[24, 'near'], [22, 'near'], [22, 'overdue'], [20, 'overdue']]));
  1472 |   expect(await notificationKeys(head.api)).toEqual(keys([[20, 'overdue'], [22, 'overdue']]));
  1473 |   expect(await notificationKeys(reg2.api)).toEqual(keys([[24, 'near']]));
  1474 |   for (const [s, n] of [[reg1, 4], [head, 2], [reg2, 1]] as const) {
  1475 |     await s.page.goto('/notifications');
  1476 |     await expect(tid(s.page, 'bell-count')).toHaveText(String(n));
  1477 |     await expect(tid(s.page, 'noti-item')).toHaveCount(n);
  1478 |   }
  1479 |   return { 'off.reg1': reg1, 'off.reg2': reg2, head1: head, 'off.works1': works };
  1480 | }
  1481 | 
  1482 | test('TC-NOTI-01 ผู้รับแจ้งเตือนตามระดับ', async ({ browser }) => {
  1483 |   await notiBaseline(browser);
  1484 | });
  1485 | 
  1486 | test('TC-NOTI-02 ไม่แจ้งซ้ำ ข้ามระดับ และขั้นรออนุมัติ/รอออกเอกสาร', async ({ browser }) => {
  1487 |   test.setTimeout(360_000);
  1488 | 
  1489 |   await test.step('ส่วน A ไม่แจ้งซ้ำ', async () => {
  1490 |     const s = await notiBaseline(browser);
  1491 |     const reg1 = s['off.reg1'];
  1492 |     const head = s.head1;
  1493 |     for (const x of [reg1, head]) {
  1494 |       for (let i = 0; i < 3; i++) await x.page.goto('/notifications');
  1495 |       for (let i = 0; i < 3; i++) await notificationKeys(x.api);
  1496 |       for (let i = 0; i < 2; i++) await x.page.goto('/officer/queue');
  1497 |     }
  1498 |     for (const [x, n] of [[reg1, 4], [head, 2]] as const) {
  1499 |       const k = await notificationKeys(x.api);
  1500 |       expect(k).toHaveLength(n);
  1501 |       expect(new Set(k).size).toBe(n); // (คำขอ, ระดับ, ผู้ใช้) มีได้ 1 รายการ
  1502 |       await x.page.goto('/notifications');
  1503 |       await expect(tid(x.page, 'bell-count')).toHaveText(String(n));
  1504 |     }
  1505 |   });
  1506 | 
  1507 |   await test.step('ส่วน B ข้ามระดับ (request แรกที่ ส. 5 ธ.ค. 10:00)', async () => {
  1508 |     await reset();
  1509 |     await setClock('2026-12-05T10:00:00+07:00');
  1510 |     const reg1 = await staffSession(browser, 'off.reg1'); // request แรก
  1511 |     const reg2 = await staffSession(browser, 'off.reg2');
  1512 |     const works = await staffSession(browser, 'off.works1');
  1513 |     const head = await staffSession(browser, 'head1');
  1514 |     const ov = (ns: number[]) => ns.map((n) => [n, 'overdue'] as [number, 'overdue']);
  1515 |     const expected: Array<[{ page: Page; api: APIRequestContext }, string[]]> = [
  1516 |       [reg1, keys(ov([20, 22, 23, 24, 28, 29, 30]))],
  1517 |       [reg2, keys([...ov([13, 15, 24, 25, 26, 27, 28, 29, 30]), [16, 'near']])],
  1518 |       [works, keys(ov([10]))],
  1519 |       [head, keys([...ov([10, 13, 14, 15, 20, 22, 23, 24, 25, 26, 27, 28, 29, 30]), [11, 'near']])],
  1520 |     ];
> 1521 |     for (const [x, exp] of expected) expect(await notificationKeys(x.api)).toEqual(exp);
       |                                                                            ^ Error: expect(received).toEqual(expected) // deep equality
  1522 |     // ไม่มี near ย้อนหลังของ …000024 · ผู้ถือ off.reg1 ของ 000020/000022 มีเฉพาะ overdue
  1523 |     for (const x of [reg1, reg2, head]) expect(only(await notificationKeys(x.api), 24)).toEqual(keys([[24, 'overdue']]));
  1524 |     for (const x of [reg1, head]) {
  1525 |       const k = await notificationKeys(x.api);
  1526 |       expect(only(k, 20)).toEqual(keys([[20, 'overdue']]));
  1527 |       expect(only(k, 22)).toEqual(keys([[22, 'overdue']]));
  1528 |     }
  1529 |     for (const [x, n] of [[reg1, 7], [reg2, 10], [works, 1], [head, 15]] as const) {
  1530 |       await x.page.goto('/notifications');
  1531 |       await expect(tid(x.page, 'bell-count')).toHaveText(String(n));
  1532 |       await expect(tid(x.page, 'noti-item')).toHaveCount(n);
  1533 |     }
  1534 |   });
  1535 | 
  1536 |   await test.step('ส่วน C ขั้นรออนุมัติ (…000014) และรอออกเอกสาร (…000019)', async () => {
  1537 |     await reset();
  1538 |     await setClock('2026-12-04T09:00:00+07:00');
  1539 |     const head = await loginStaff('head1');
  1540 |     const reg1 = await loginStaff('off.reg1');
  1541 |     const reg2 = await loginStaff('off.reg2');
  1542 |     expect(only(await notificationKeys(head), 14)).toEqual(keys([[14, 'near']]));
  1543 |     expect(only(await notificationKeys(reg1), 14)).toEqual([]);
  1544 |     expect(only(await notificationKeys(reg2), 14)).toEqual([]);
  1545 | 
  1546 |     // 1
  1547 |     await setClock('2026-12-04T16:31:00+07:00');
  1548 |     await expectApi(head.get('/api/me'), 200);
  1549 |     expect(only(await notificationKeys(head), 14)).toEqual(keys([[14, 'near'], [14, 'overdue']]));
  1550 |     expect(only(await notificationKeys(reg1), 14)).toEqual([]);
  1551 |     expect(only(await notificationKeys(reg2), 14)).toEqual([]);
  1552 | 
  1553 |     // 2
  1554 |     await setClock('2026-12-08T09:00:00+07:00');
  1555 |     await expectApi(head.get('/api/me'), 200);
  1556 |     expect(only(await notificationKeys(reg1), 19)).toEqual(keys([[19, 'near']]));
  1557 |     expect(only(await notificationKeys(reg2), 19)).toEqual([]);
  1558 |     expect(only(await notificationKeys(head), 19)).toEqual([]);
  1559 | 
  1560 |     // 3
  1561 |     await setClock('2026-12-09T16:31:00+07:00');
  1562 |     await expectApi(head.get('/api/me'), 200);
  1563 |     expect(only(await notificationKeys(reg1), 19)).toEqual(keys([[19, 'near'], [19, 'overdue']]));
  1564 |     expect(only(await notificationKeys(head), 19)).toEqual(keys([[19, 'overdue']]));
  1565 |     expect(only(await notificationKeys(reg2), 19)).toEqual([]);
  1566 |   });
  1567 | });
  1568 | 
```