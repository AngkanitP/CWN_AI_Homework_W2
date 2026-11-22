# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-RBAC-04 ผู้ดูแลระบบ: บริการ วันหยุด ผู้ใช้ และยอดที่ล็อก
- Location: tests/part2.spec.ts:1493:1

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: "2026-12-08T16:30:00+07:00"
Received: "2026-12-04T16:30:00+07:00"
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
            - link "คำขอของฉัน" [ref=e9] [cursor=pointer]:
              - /url: /citizen
      - generic [ref=e10]:
        - generic [ref=e11]:
          - text: สมชาย ใจดี
          - generic [ref=e12]: ประชาชน
        - button "ออกจากระบบ" [ref=e14] [cursor=pointer]
  - main [ref=e15]:
    - paragraph [ref=e16]:
      - link "← คำขอของฉัน" [ref=e17] [cursor=pointer]:
        - /url: /citizen
    - heading "ยื่นคำขอ ขออนุญาตประกอบกิจการ" [level=1] [ref=e18]
    - list "ขั้นตอนการยื่น" [ref=e19]:
      - listitem [ref=e20]: กรอกข้อมูล
      - listitem [ref=e21]: แนบเอกสาร
      - listitem [ref=e22]: ชำระเงิน
    - paragraph [ref=e23]:
      - strong [ref=e24]: 3/3 ชำระเงิน
    - paragraph [ref=e25]:
      - text: รหัสร่าง
      - strong [ref=e26]: DR-0002
    - paragraph [ref=e27]: ขออนุญาตประกอบกิจการ
    - region "ชำระเงินด้วย PromptPay QR (จำลอง)" [ref=e28]:
      - heading "ชำระเงินด้วย PromptPay QR (จำลอง)" [level=2] [ref=e29]
      - generic [ref=e30]:
        - paragraph [ref=e31]:
          - text: ยอดที่ต้องชำระ
          - strong [ref=e32]: ฿500
        - generic [ref=e33]:
          - img "QR PromptPay จำลอง เลขอ้างอิง PP-0001" [ref=e34]
          - paragraph [ref=e37]:
            - text: เลขอ้างอิง
            - strong [ref=e38]: PP-0001
          - paragraph [ref=e39]:
            - time [ref=e40]: หมดอายุ 1 ธ.ค. 2569 09:10
          - paragraph [ref=e41]:
            - text: สถานะการชำระ
            - generic [ref=e42]: รอชำระ
          - paragraph [ref=e43]:
            - button "ตรวจสอบการชำระเงิน" [ref=e44] [cursor=pointer]
  - contentinfo [ref=e45]:
    - paragraph [ref=e46]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  1475 |       const somying = role === 'anon' ? api : role === 'citizen' ? await loginCitizen(ID.SOMYING) : api;
  1476 |       for (const [label, call, exp] of APIS) {
  1477 |         const r = await call({ api, somying });
  1478 |         expect.soft(r.status(), `${role} ${label}`).toBe(exp[role]);
  1479 |       }
  1480 |     });
  1481 |   }
  1482 | 
  1483 |   await test.step('ส่วน C ขอบเขตแผนก', async () => {
  1484 |     await reset();
  1485 |     const works = await loginStaff('off.works1');
  1486 |     const reg1 = await loginStaff('off.reg1');
  1487 |     await expectApi(claimRaw(works, caseNo(28)), 403);
  1488 |     await expectApi(claimRaw(reg1, caseNo(10)), 403);
  1489 |     expect((await queueItems(works, 'all')).map((i) => i.caseNo)).toEqual([caseNo(10)]);
  1490 |   });
  1491 | });
  1492 | 
  1493 | test('TC-RBAC-04 ผู้ดูแลระบบ: บริการ วันหยุด ผู้ใช้ และยอดที่ล็อก', async ({ browser }) => {
  1494 |   test.setTimeout(240_000);
  1495 |   await reset();
  1496 |   const admin = await staffSession(browser, 'admin1');
  1497 |   const a = admin.page;
  1498 |   const HOLIDAYS = ['2026-12-07', '2026-12-10', '2026-12-31', '2027-01-01'];
  1499 | 
  1500 |   await test.step('1 วันหยุดตั้งต้น 4 วัน', async () => {
  1501 |     await a.goto('/admin/holidays');
  1502 |     await expect(tid(a, 'holiday-row')).toHaveCount(4);
  1503 |     expect(((await attrs(tid(a, 'holiday-row'), 'data-date')) as string[]).sort()).toEqual(HOLIDAYS);
  1504 |   });
  1505 | 
  1506 |   let sc!: APIRequestContext;
  1507 |   await test.step('2 NEW_PAID ก่อนแก้ → …000031 กำหนด 4 ธ.ค.', async () => {
  1508 |     const c = await newPaid({ idNo: ID.SOMCHAI, service: 'SV-01', qty: 1 });
  1509 |     sc = c.api;
  1510 |     expect(c.fee).toBe(20);
  1511 |     expect(c.caseNo).toBe(caseNo(31));
  1512 |     expect((await getCase(sc, caseNo(31))).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1513 |   });
  1514 | 
  1515 |   await test.step('3 แก้ค่าธรรมเนียม SV-01 = 25 · SV-02 = 600', async () => {
  1516 |     for (const [svc, fee] of [
  1517 |       ['SV-01', '25'],
  1518 |       ['SV-02', '600'],
  1519 |     ] as const) {
  1520 |       await a.goto('/admin/services');
  1521 |       await tid(a, `svc-fee-${svc}`).fill(fee);
  1522 |       await act(a, () => tid(a, `svc-save-${svc}`).click(), { reload: false });
  1523 |       await expect(tid(a, 'action-success'), svc).toBeVisible();
  1524 |     }
  1525 |     const items = (await expectApi(admin.api.get('/api/admin/services'), 200)).items as any[];
  1526 |     expect(items.find((i) => i.id === 'SV-01').fee).toBe(25);
  1527 |     expect(items.find((i) => i.id === 'SV-02').fee).toBe(600);
  1528 |   });
  1529 | 
  1530 |   await test.step('4 ร่างใหม่ใช้ค่าใหม่ · คำขอเดิมไม่เปลี่ยน', async () => {
  1531 |     const { page: c } = await pageFromApi(browser, sc);
  1532 |     await c.goto('/citizen/new/SV-01');
  1533 |     await fillField(tid(c, 'qty-input'), '5');
  1534 |     await expect(tid(c, 'fee-total')).toHaveText('฿125');
  1535 |     await fillField(tid(c, 'qty-input'), '1');
  1536 |     await expect(tid(c, 'fee-total')).toHaveText('฿25');
  1537 |     await c.goto('/citizen/new/SV-02');
  1538 |     await expect(tid(c, 'fee-total')).toHaveText('฿600');
  1539 |     expect((await createDraft(sc, 'SV-01', { qty: 5 })).fee).toBe(125);
  1540 |     expect((await createDraft(sc, 'SV-02')).fee).toBe(600);
  1541 |     await openCitizen(c, caseNo(30));
  1542 |     await expect(tid(c, 'case-fee')).toHaveText('฿20');
  1543 |   });
  1544 | 
  1545 |   await test.step('5 PP-0001 ยอดที่ล็อก ฿500', async () => {
  1546 |     const { page: c } = await pageFromApi(browser, sc);
  1547 |     await c.goto('/citizen/new/SV-02?draft=DR-0002');
  1548 |     await c.waitForLoadState('networkidle').catch(() => {});
  1549 |     const amt = tid(c, 'payment-amount');
  1550 |     if (!(await amt.isVisible())) {
  1551 |       // ร่างเปิดที่ขั้นก่อนหน้า → เดินไปขั้นชำระ (ร่างนี้แนบเอกสารครบแล้ว)
  1552 |       if (await tid(c, 'to-upload-btn').isVisible()) await tid(c, 'to-upload-btn').click();
  1553 |       await tid(c, 'to-payment-btn').click();
  1554 |     }
  1555 |     await expect(amt).toHaveText('฿500');
  1556 |     expect((await getPayment(sc, 'PP-0001')).amount).toBe(500);
  1557 |     await expectApi(payRaw('PP-0001', 600), 422, 'AMOUNT_MISMATCH');
  1558 |     expect((await pay('PP-0001', 500)).caseNo).toBe(caseNo(32));
  1559 |   });
  1560 | 
  1561 |   await test.step('6 เพิ่มวันหยุด 2 ธ.ค. → คำขอเดิมไม่คำนวณใหม่', async () => {
  1562 |     await a.goto('/admin/holidays');
  1563 |     await tid(a, 'holiday-date-input').fill('2026-12-02');
  1564 |     await tid(a, 'holiday-name-input').fill('วันหยุดทดสอบ');
  1565 |     await act(a, () => tid(a, 'holiday-add-btn').click());
  1566 |     await expect(tid(a, 'holiday-row')).toHaveCount(5);
  1567 |     await expect(rowBy(a, 'holiday-row', 'data-date', '2026-12-02')).toHaveCount(1);
  1568 |     expect((await getCase(sc, caseNo(31))).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1569 |   });
  1570 | 
  1571 |   await test.step('7 NEW_PAID หลังเพิ่มวันหยุด → …000033 กำหนด 8 ธ.ค.', async () => {
  1572 |     const c = await newPaid({ idNo: ID.SOMCHAI, service: 'SV-01', qty: 1 });
  1573 |     expect(c.fee).toBe(25);
  1574 |     expect(c.caseNo).toBe(caseNo(33));
> 1575 |     expect((await getCase(c.api, caseNo(33))).dueAt).toBe('2026-12-08T16:30:00+07:00');
       |                                                      ^ Error: expect(received).toBe(expected) // Object.is equality
  1576 |   });
  1577 | 
  1578 |   let exPage!: Page;
  1579 |   await test.step('8 เปลี่ยน exec1 เป็น auditor → ล็อกอินใหม่ไป /audit', async () => {
  1580 |     await expectApi(admin.api.put('/api/admin/users/exec1', { data: { role: 'auditor', dept: '' } }), 200);
  1581 |     const s = await newSession(browser);
  1582 |     exPage = s.page;
  1583 |     await uiStaffSubmit(exPage, 'exec1');
  1584 |     await waitPath(exPage, '/audit');
  1585 |     const res = await exPage.goto('/dashboard');
  1586 |     expect(res?.status()).toBe(403);
  1587 |     await expect(tid(exPage, 'forbidden-msg')).toHaveText(MSG.FORBIDDEN_PAGE);
  1588 |   });
  1589 | 
  1590 |   const ADMIN_DETAILS = ['SV-01 fee 20 → 25', 'SV-02 fee 500 → 600', 'holiday add 2026-12-02', 'exec1 role executive → auditor'];
  1591 |   const expectAdminChanges = async (n: number, details: string[]) => {
  1592 |     const rows = await uiAuditExpect(exPage, { event: 'ADMIN_CHANGE' }, n);
  1593 |     for (const r of rows) {
  1594 |       expect(r.actor).toBe('admin1');
  1595 |       expect(r.role).toBe('admin');
  1596 |     }
  1597 |     for (const d of details) expect(rows.some((r) => r.detail.includes(d)), `ADMIN_CHANGE "${d}"`).toBe(true);
  1598 |   };
  1599 | 
  1600 |   await test.step('9 Audit ADMIN_CHANGE 4 แถว', async () => {
  1601 |     await expectAdminChanges(4, ADMIN_DETAILS);
  1602 |   });
  1603 | 
  1604 |   await test.step('10 admin ทำรายการคำขอไม่ได้', async () => {
  1605 |     await expectApi(admin.api.post('/api/drafts', { data: { serviceId: 'SV-01', qty: 1 } }), 403);
  1606 |   });
  1607 | 
  1608 |   await test.step('11 ลบวันหยุด 2 ธ.ค.', async () => {
  1609 |     await a.goto('/admin/holidays');
  1610 |     const row = rowBy(a, 'holiday-row', 'data-date', '2026-12-02');
  1611 |     const inRow = row.getByTestId('holiday-delete-btn');
  1612 |     const btn = (await inRow.count()) ? inRow : rowBy(a, 'holiday-delete-btn', 'data-date', '2026-12-02');
  1613 |     await act(a, () => btn.click());
  1614 |     await expect(tid(a, 'holiday-row')).toHaveCount(4);
  1615 |     await expectAdminChanges(5, [...ADMIN_DETAILS, 'holiday delete 2026-12-02']);
  1616 |   });
  1617 | });
  1618 | 
  1619 | test('TC-RBAC-05 สิทธิ์เปิด/ดาวน์โหลดไฟล์แนบ', async ({ browser }) => {
  1620 |   test.setTimeout(240_000);
  1621 |   await reset();
  1622 |   const SV01 = ['id-card.pdf'];
  1623 |   const SV03 = ['deed.pdf', 'id-card.pdf', 'plan.pdf'];
  1624 | 
  1625 |   const reg1 = await staffSession(browser, 'off.reg1');
  1626 |   const reg2 = await staffSession(browser, 'off.reg2');
  1627 |   const sy = await citizenSession(browser, ID.SOMYING);
  1628 |   const works = await loginStaff('off.works1');
  1629 |   const head = await loginStaff('head1');
  1630 |   const sc = await loginCitizen(ID.SOMCHAI);
  1631 | 
  1632 |   // fileId ของแต่ละคำขอ (หัวหน้าเห็นทุกแผนก · คำขอ …000025 ใช้ของสมหญิงตาม TEST-PLAN)
  1633 |   const files: Record<number, Array<{ fileId: string; name: string }>> = {};
  1634 |   files[25] = (await expectApi(sy.api.get(`/api/cases/${caseNo(25)}/files`), 200)).items;
  1635 |   for (const n of [10, 11, 12]) files[n] = (await expectApi(head.get(`/api/cases/${caseNo(n)}/files`), 200)).items;
  1636 | 
  1637 |   async function check(label: string, api: APIRequestContext, n: number, exp: number, names?: string[]): Promise<void> {
  1638 |     const r = await api.get(`/api/cases/${caseNo(n)}/files`);
  1639 |     expect.soft(r.status(), `${label} /api/cases/${caseNo(n)}/files`).toBe(exp);
  1640 |     if (exp === 200 && names) {
  1641 |       const items = ((await bodyOf(r)).items ?? []) as Array<{ name: string }>;
  1642 |       expect.soft(items.map((i) => i.name).sort(), `${label} รายการไฟล์ ${caseNo(n)}`).toEqual(names);
  1643 |     }
  1644 |     for (const f of files[n]) {
  1645 |       const fr = await api.get(`/api/files/${f.fileId}`);
  1646 |       expect.soft(fr.status(), `${label} /api/files/${f.fileId} (${f.name} ของ ${caseNo(n)})`).toBe(exp);
  1647 |       if (exp === 200) {
  1648 |         expect.soft(fr.headers()['content-type'] ?? '', `${label} ${f.name}`).toContain('application/pdf');
  1649 |         expect.soft((await fr.body()).subarray(0, 4).toString('latin1'), `${label} ${f.name}`).toBe('%PDF');
  1650 |       }
  1651 |     }
  1652 |   }
  1653 | 
  1654 |   await test.step('ตาราง API', async () => {
  1655 |     await check('off.reg1', reg1.api, 25, 200, SV01);
  1656 |     await check('off.works1', works, 25, 403);
  1657 |     await check('off.reg2', reg2.api, 12, 200, SV03);
  1658 |     await check('off.works1', works, 12, 403);
  1659 |     await check('off.works1', works, 10, 200, SV03);
  1660 |     await check('off.reg1', reg1.api, 10, 200, SV03);
  1661 |     await check('off.works1', works, 11, 200, SV03);
  1662 |     await check('head1', head, 25, 200, SV01);
  1663 |     await check('head1', head, 10, 200, SV03);
  1664 |     await check('head1', head, 12, 200, SV03);
  1665 |     await check('สมหญิง', sy.api, 25, 200, SV01);
  1666 |     await check('สมชาย', sc, 25, 404);
  1667 |     for (const u of ['exec1', 'audit1', 'admin1'] as const) await check(u, await loginStaff(u), 25, 403);
  1668 |     await check('ไม่ล็อกอิน', await newApi(), 25, 401);
  1669 |     await expectApi(reg1.api.get('/api/files/999999999'), 404);
  1670 |   });
  1671 | 
  1672 |   await test.step('UI doc-item + ดาวน์โหลด', async () => {
  1673 |     await openOfficer(reg1.page, caseNo(25));
  1674 |     await expect(tid(reg1.page, 'doc-item')).toHaveCount(1);
  1675 |     const item = rowBy(reg1.page, 'doc-item', 'data-name', 'id-card.pdf');
```