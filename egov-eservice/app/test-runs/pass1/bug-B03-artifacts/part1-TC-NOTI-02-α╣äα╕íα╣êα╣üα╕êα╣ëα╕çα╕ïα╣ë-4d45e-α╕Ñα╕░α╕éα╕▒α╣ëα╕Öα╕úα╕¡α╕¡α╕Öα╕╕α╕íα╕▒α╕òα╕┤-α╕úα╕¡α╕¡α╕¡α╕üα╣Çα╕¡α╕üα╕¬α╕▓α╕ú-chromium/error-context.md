# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-NOTI-02 ไม่แจ้งซ้ำ ข้ามระดับ และขั้นรออนุมัติ/รอออกเอกสาร
- Location: tests/part1.spec.ts:1478:1

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
  1413 |     const somying = await citizenSession(browser, ID.SOMYING);
  1414 |     await somying.page.goto(`/citizen/cases/${caseNo(1)}`);
  1415 |     await expectLevel(somying.page, 'closed');
  1416 | 
  1417 |     await setClock('2026-12-01T16:30:00+07:00');
  1418 |     await o.page.goto('/officer/queue');
  1419 |     await expect(queueRow(o.page, caseNo(22)).getByTestId('row-sla-level')).toHaveText('ใกล้ครบกำหนด');
  1420 |     await setClock('2026-12-01T16:31:00+07:00');
  1421 |     await o.page.goto('/officer/queue');
  1422 |     await expect(queueRow(o.page, caseNo(22)).getByTestId('row-sla-level')).toHaveText('เกินกำหนด');
  1423 |     await expect(queueRow(o.page, caseNo(22))).toHaveAttribute('data-sla-level', 'overdue');
  1424 |   });
  1425 | });
  1426 | 
  1427 | // ═══════════════════════════════════ NOTI ═══════════════════════════════════
  1428 | 
  1429 | /**
  1430 |  * TC-NOTI-01 ทั้งชุด: RESET → off.reg1 ล็อกอินที่ 09:00 (request แรก) → ตรวจผู้รับ 4 คน → CLOCK 16:31 → ตรวจเพิ่ม
  1431 |  * คืน session ของทุกคนเพื่อให้ TC-NOTI-02 ส่วน A ใช้ต่อ
  1432 |  */
  1433 | async function notiBaseline(browser: Browser): Promise<Record<'off.reg1' | 'off.reg2' | 'head1' | 'off.works1', { page: Page; api: APIRequestContext }>> {
  1434 |   await reset();
  1435 |   const reg1 = await staffSession(browser, 'off.reg1'); // request แรกหลัง reset ที่ 09:00
  1436 |   const reg2 = await staffSession(browser, 'off.reg2');
  1437 |   const head = await staffSession(browser, 'head1');
  1438 |   const works = await staffSession(browser, 'off.works1');
  1439 | 
  1440 |   const expected: Array<[{ page: Page; api: APIRequestContext }, string[], number]> = [
  1441 |     [reg1, keys([[24, 'near'], [22, 'near'], [20, 'overdue']]), 3],
  1442 |     [reg2, keys([[24, 'near']]), 1],
  1443 |     [head, keys([[20, 'overdue']]), 1],
  1444 |     [works, [], 0],
  1445 |   ];
  1446 |   for (const [s, exp, count] of expected) {
  1447 |     expect(await notificationKeys(s.api)).toEqual(exp);
  1448 |     await s.page.goto('/notifications');
  1449 |     await expect(tid(s.page, 'bell-count')).toHaveText(String(count));
  1450 |     await expect(tid(s.page, 'noti-item')).toHaveCount(count);
  1451 |     expect(await uiNotiKeys(s.page)).toEqual(exp);
  1452 |   }
  1453 |   await expect(rowBy(reg1.page, 'noti-item', 'data-case-no', caseNo(24))).toContainText('คำขอ EG-2569-000024 ใกล้ครบกำหนด');
  1454 |   await expect(rowBy(reg1.page, 'noti-item', 'data-case-no', caseNo(20))).toContainText('คำขอ EG-2569-000020 เกินกำหนด');
  1455 |   await expect(tid(works.page, 'noti-empty')).toHaveText(MSG.NOTI_EMPTY);
  1456 |   const apiItems = (await expectApi(reg1.api.get('/api/notifications'), 200)).items as any[];
  1457 |   expect(apiItems.find((n) => n.caseNo === caseNo(24))?.text).toBe('คำขอ EG-2569-000024 ใกล้ครบกำหนด');
  1458 |   expect(apiItems.find((n) => n.caseNo === caseNo(20))?.text).toBe('คำขอ EG-2569-000020 เกินกำหนด');
  1459 | 
  1460 |   // ต่อ: 16:31 + request ใด ๆ → …000022 เกินกำหนด
  1461 |   await setClock('2026-12-01T16:31:00+07:00');
  1462 |   await expectApi(reg1.api.get('/api/me'), 200);
  1463 |   expect(await notificationKeys(reg1.api)).toEqual(keys([[24, 'near'], [22, 'near'], [22, 'overdue'], [20, 'overdue']]));
  1464 |   expect(await notificationKeys(head.api)).toEqual(keys([[20, 'overdue'], [22, 'overdue']]));
  1465 |   expect(await notificationKeys(reg2.api)).toEqual(keys([[24, 'near']]));
  1466 |   for (const [s, n] of [[reg1, 4], [head, 2], [reg2, 1]] as const) {
  1467 |     await s.page.goto('/notifications');
  1468 |     await expect(tid(s.page, 'bell-count')).toHaveText(String(n));
  1469 |     await expect(tid(s.page, 'noti-item')).toHaveCount(n);
  1470 |   }
  1471 |   return { 'off.reg1': reg1, 'off.reg2': reg2, head1: head, 'off.works1': works };
  1472 | }
  1473 | 
  1474 | test('TC-NOTI-01 ผู้รับแจ้งเตือนตามระดับ', async ({ browser }) => {
  1475 |   await notiBaseline(browser);
  1476 | });
  1477 | 
  1478 | test('TC-NOTI-02 ไม่แจ้งซ้ำ ข้ามระดับ และขั้นรออนุมัติ/รอออกเอกสาร', async ({ browser }) => {
  1479 |   test.setTimeout(360_000);
  1480 | 
  1481 |   await test.step('ส่วน A ไม่แจ้งซ้ำ', async () => {
  1482 |     const s = await notiBaseline(browser);
  1483 |     const reg1 = s['off.reg1'];
  1484 |     const head = s.head1;
  1485 |     for (const x of [reg1, head]) {
  1486 |       for (let i = 0; i < 3; i++) await x.page.goto('/notifications');
  1487 |       for (let i = 0; i < 3; i++) await notificationKeys(x.api);
  1488 |       for (let i = 0; i < 2; i++) await x.page.goto('/officer/queue');
  1489 |     }
  1490 |     for (const [x, n] of [[reg1, 4], [head, 2]] as const) {
  1491 |       const k = await notificationKeys(x.api);
  1492 |       expect(k).toHaveLength(n);
  1493 |       expect(new Set(k).size).toBe(n); // (คำขอ, ระดับ, ผู้ใช้) มีได้ 1 รายการ
  1494 |       await x.page.goto('/notifications');
  1495 |       await expect(tid(x.page, 'bell-count')).toHaveText(String(n));
  1496 |     }
  1497 |   });
  1498 | 
  1499 |   await test.step('ส่วน B ข้ามระดับ (request แรกที่ ส. 5 ธ.ค. 10:00)', async () => {
  1500 |     await reset();
  1501 |     await setClock('2026-12-05T10:00:00+07:00');
  1502 |     const reg1 = await staffSession(browser, 'off.reg1'); // request แรก
  1503 |     const reg2 = await staffSession(browser, 'off.reg2');
  1504 |     const works = await staffSession(browser, 'off.works1');
  1505 |     const head = await staffSession(browser, 'head1');
  1506 |     const ov = (ns: number[]) => ns.map((n) => [n, 'overdue'] as [number, 'overdue']);
  1507 |     const expected: Array<[{ page: Page; api: APIRequestContext }, string[]]> = [
  1508 |       [reg1, keys(ov([20, 22, 23, 24, 28, 29, 30]))],
  1509 |       [reg2, keys([...ov([13, 15, 24, 25, 26, 27, 28, 29, 30]), [16, 'near']])],
  1510 |       [works, keys(ov([10]))],
  1511 |       [head, keys([...ov([10, 13, 14, 15, 20, 22, 23, 24, 25, 26, 27, 28, 29, 30]), [11, 'near']])],
  1512 |     ];
> 1513 |     for (const [x, exp] of expected) expect(await notificationKeys(x.api)).toEqual(exp);
       |                                                                            ^ Error: expect(received).toEqual(expected) // deep equality
  1514 |     // ไม่มี near ย้อนหลังของ …000024 · ผู้ถือ off.reg1 ของ 000020/000022 มีเฉพาะ overdue
  1515 |     for (const x of [reg1, reg2, head]) expect(only(await notificationKeys(x.api), 24)).toEqual(keys([[24, 'overdue']]));
  1516 |     for (const x of [reg1, head]) {
  1517 |       const k = await notificationKeys(x.api);
  1518 |       expect(only(k, 20)).toEqual(keys([[20, 'overdue']]));
  1519 |       expect(only(k, 22)).toEqual(keys([[22, 'overdue']]));
  1520 |     }
  1521 |     for (const [x, n] of [[reg1, 7], [reg2, 10], [works, 1], [head, 15]] as const) {
  1522 |       await x.page.goto('/notifications');
  1523 |       await expect(tid(x.page, 'bell-count')).toHaveText(String(n));
  1524 |       await expect(tid(x.page, 'noti-item')).toHaveCount(n);
  1525 |     }
  1526 |   });
  1527 | 
  1528 |   await test.step('ส่วน C ขั้นรออนุมัติ (…000014) และรอออกเอกสาร (…000019)', async () => {
  1529 |     await reset();
  1530 |     await setClock('2026-12-04T09:00:00+07:00');
  1531 |     const head = await loginStaff('head1');
  1532 |     const reg1 = await loginStaff('off.reg1');
  1533 |     const reg2 = await loginStaff('off.reg2');
  1534 |     expect(only(await notificationKeys(head), 14)).toEqual(keys([[14, 'near']]));
  1535 |     expect(only(await notificationKeys(reg1), 14)).toEqual([]);
  1536 |     expect(only(await notificationKeys(reg2), 14)).toEqual([]);
  1537 | 
  1538 |     // 1
  1539 |     await setClock('2026-12-04T16:31:00+07:00');
  1540 |     await expectApi(head.get('/api/me'), 200);
  1541 |     expect(only(await notificationKeys(head), 14)).toEqual(keys([[14, 'near'], [14, 'overdue']]));
  1542 |     expect(only(await notificationKeys(reg1), 14)).toEqual([]);
  1543 |     expect(only(await notificationKeys(reg2), 14)).toEqual([]);
  1544 | 
  1545 |     // 2
  1546 |     await setClock('2026-12-08T09:00:00+07:00');
  1547 |     await expectApi(head.get('/api/me'), 200);
  1548 |     expect(only(await notificationKeys(reg1), 19)).toEqual(keys([[19, 'near']]));
  1549 |     expect(only(await notificationKeys(reg2), 19)).toEqual([]);
  1550 |     expect(only(await notificationKeys(head), 19)).toEqual([]);
  1551 | 
  1552 |     // 3
  1553 |     await setClock('2026-12-09T16:31:00+07:00');
  1554 |     await expectApi(head.get('/api/me'), 200);
  1555 |     expect(only(await notificationKeys(reg1), 19)).toEqual(keys([[19, 'near'], [19, 'overdue']]));
  1556 |     expect(only(await notificationKeys(head), 19)).toEqual(keys([[19, 'overdue']]));
  1557 |     expect(only(await notificationKeys(reg2), 19)).toEqual([]);
  1558 |   });
  1559 | });
  1560 | 
```