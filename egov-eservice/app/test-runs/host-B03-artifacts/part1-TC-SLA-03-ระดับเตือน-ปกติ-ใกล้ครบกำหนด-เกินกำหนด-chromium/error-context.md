# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-SLA-03 ระดับเตือน ปกติ / ใกล้ครบกำหนด / เกินกำหนด
- Location: tests\part1.spec.ts:1357:1

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: "near"
Received: "normal"
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
          - text: ปิติ มีสุข
          - generic [ref=e12]: ประชาชน
        - button "ออกจากระบบ" [ref=e14] [cursor=pointer]
  - main [ref=e15]:
    - paragraph [ref=e16]:
      - link "← คำขอของฉัน" [ref=e17] [cursor=pointer]:
        - /url: /citizen
    - heading "คำขอ EG-2569-000016" [level=1] [ref=e18]
    - region "รายละเอียดคำขอ" [ref=e19]:
      - heading "รายละเอียดคำขอ" [level=2] [ref=e20]
      - generic [ref=e21]:
        - term [ref=e22]: สถานะ
        - definition [ref=e23]:
          - generic [ref=e24]: กำลังตรวจสอบ
        - term [ref=e25]: บริการ
        - definition [ref=e26]: SV-02 ขออนุญาตประกอบกิจการ
        - term [ref=e27]: ค่าธรรมเนียม
        - definition [ref=e28]: ฿500
        - term [ref=e29]: เลขใบเสร็จ
        - definition [ref=e30]: RC-2569-000016
        - term [ref=e31]: ชำระเมื่อ
        - definition [ref=e32]:
          - time [ref=e33]: 23 พ.ย. 2569 09:00
        - term [ref=e34]: กำหนดเสร็จ
        - definition [ref=e35]:
          - time [ref=e36]: 8 ธ.ค. 2569 16:30
        - term [ref=e37]: ระดับเตือน
        - definition [ref=e38]:
          - generic [ref=e39]: ปกติ
        - term [ref=e40]: ผู้ยื่น
        - definition [ref=e41]: ปิติ มีสุข
        - term [ref=e42]: เลขบัตรประชาชน
        - definition [ref=e43]: 1-9099-00555-01-5
    - region "เอกสารแนบ" [ref=e44]:
      - heading "เอกสารแนบ" [level=2] [ref=e45]
      - list [ref=e46]:
        - listitem [ref=e47]:
          - text: "บัตรประชาชน:"
          - link "id-card.pdf" [ref=e48] [cursor=pointer]:
            - /url: /api/files/f_seed_000016_id-card
          - text: (1 KB)
        - listitem [ref=e49]:
          - text: "แผนที่ตั้ง:"
          - link "map.pdf" [ref=e50] [cursor=pointer]:
            - /url: /api/files/f_seed_000016_map
          - text: (1 KB)
    - region "ไทม์ไลน์" [ref=e51]:
      - heading "ไทม์ไลน์" [level=2] [ref=e52]
      - list [ref=e53]:
        - listitem [ref=e54]:
          - time [ref=e55]: 23 พ.ย. 2569 09:00
          - text: · ชำระค่าธรรมเนียมและส่งคำขอแล้ว (ใบเสร็จ RC-2569-000016)
        - listitem [ref=e56]:
          - time [ref=e57]: 23 พ.ย. 2569 09:30
          - text: · เจ้าหน้าที่รับเรื่อง
  - contentinfo [ref=e58]:
    - paragraph [ref=e59]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  1263 |     await reset();
  1264 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1265 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1266 |     expect(paid.caseNo).toBe(NEW);
  1267 |     expect((await getCase(c.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1268 | 
  1269 |     await setClock('2026-12-02T11:00:00+07:00');
  1270 |     const o = await staffSession(browser, 'off.reg1');
  1271 |     await claim(o.api, NEW);
  1272 |     await returnCase(o.api, NEW, 'xxxxxxxxxx');
  1273 |     await o.page.goto(`/officer/cases/${NEW}`);
  1274 |     await expectStatus(o.page, 'NEED_FIX');
  1275 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1276 |     await expectStatus(c.page, 'NEED_FIX');
  1277 |     await expectLevel(c.page, 'paused');
  1278 |     await expect(tid(c.page, 'fix-deadline')).toHaveAttribute('data-iso', '2026-12-09T11:00:00+07:00');
  1279 | 
  1280 |     await setClock('2026-12-03T10:00:00+07:00');
  1281 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1282 |     await tid(c.page, 'submit-fix-btn').click();
  1283 |     await expectStatus(c.page, 'IN_REVIEW');
  1284 |     await expectDue(c.page, '8 ธ.ค. 2569 16:30', '2026-12-08T16:30:00+07:00');
  1285 |     await expectLevel(c.page, 'normal');
  1286 |     const got = await getCase(o.api, NEW);
  1287 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1288 |     expect(got.owner).toBe('off.reg1');
  1289 |     await o.page.goto(`/officer/cases/${NEW}`);
  1290 |     await expect(tid(o.page, 'case-owner')).toHaveText('off.reg1');
  1291 |   });
  1292 | 
  1293 |   await test.step('ส่วน 2 seed …000017 ส่งแก้ 1 ธ.ค. 09:00 (หยุด 2 วัน)', async () => {
  1294 |     await reset();
  1295 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1296 |     await c.page.goto(`/citizen/cases/${F01}`);
  1297 |     await expectLevel(c.page, 'paused');
  1298 |     await expect(tid(c.page, 'sla-due')).toHaveAttribute('data-iso', '2026-11-27T16:30:00+07:00');
  1299 |     await tid(c.page, 'submit-fix-btn').click();
  1300 |     await expectStatus(c.page, 'IN_REVIEW');
  1301 |     await expectDue(c.page, '1 ธ.ค. 2569 16:30', '2026-12-01T16:30:00+07:00');
  1302 |     await expectLevel(c.page, 'near');
  1303 |     const reg1 = await loginStaff('off.reg1');
  1304 |     const got = await getCase(reg1, F01);
  1305 |     expect(got.dueAt).toBe('2026-12-01T16:30:00+07:00');
  1306 |     expect(got.owner).toBe('off.reg1');
  1307 |   });
  1308 | 
  1309 |   await test.step('ส่วน 3 ส่งแก้ …000017 วันที่ 4 ธ.ค. 10:00 (หยุด 5 วัน)', async () => {
  1310 |     await reset();
  1311 |     await setClock('2026-12-04T10:00:00+07:00');
  1312 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1313 |     const r = await resubmit(c.api, F01);
  1314 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1315 |     const got = await getCase(c.api, F01);
  1316 |     expect(got.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1317 |     expect(got.slaLevel).toBe('near');
  1318 |     await c.page.goto(`/citizen/cases/${F01}`);
  1319 |     await expectLevel(c.page, 'near');
  1320 |   });
  1321 | 
  1322 |   await test.step('ส่วน 4 ตีกลับและส่งแก้วันเดียวกัน (หยุด 0 วัน)', async () => {
  1323 |     await reset();
  1324 |     const paid = await newPaid({ idNo: ID.SOMCHAI, service: 'SV-01', qty: 1 });
  1325 |     expect(paid.caseNo).toBe(NEW);
  1326 |     await setClock('2026-12-02T09:00:00+07:00');
  1327 |     const reg1 = await loginStaff('off.reg1');
  1328 |     await claim(reg1, NEW);
  1329 |     await returnCase(reg1, NEW);
  1330 |     await setClock('2026-12-02T15:00:00+07:00');
  1331 |     const r = await resubmit(paid.api, NEW);
  1332 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1333 |     expect((await getCase(paid.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1334 |   });
  1335 | 
  1336 |   await test.step('ส่วน 5 คร่อมสุดสัปดาห์/วันหยุด ส่งแก้หลัง 16:30', async () => {
  1337 |     await reset();
  1338 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1339 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1340 |     expect(paid.caseNo).toBe(NEW);
  1341 |     await setClock('2026-12-04T10:00:00+07:00');
  1342 |     const reg1 = await loginStaff('off.reg1');
  1343 |     await claim(reg1, NEW);
  1344 |     await returnCase(reg1, NEW);
  1345 |     await setClock('2026-12-08T17:00:00+07:00');
  1346 |     const r = await resubmit(c.api, NEW);
  1347 |     expect(r.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1348 |     const got = await getCase(c.api, NEW);
  1349 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1350 |     expect(got.slaLevel).toBe('overdue');
  1351 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1352 |     await expectDue(c.page, '8 ธ.ค. 2569 16:30', '2026-12-08T16:30:00+07:00');
  1353 |     await expectLevel(c.page, 'overdue');
  1354 |   });
  1355 | });
  1356 | 
  1357 | test('TC-SLA-03 ระดับเตือน ปกติ / ใกล้ครบกำหนด / เกินกำหนด', async ({ browser }) => {
  1358 |   test.setTimeout(300_000);
  1359 | 
  1360 |   async function levelAt(s: { page: Page; api: APIRequestContext }, no: string, clock: string, level: SlaLevel): Promise<void> {
  1361 |     await test.step(`${no} @ ${clock} → ${level}`, async () => {
  1362 |       await setClock(clock);
> 1363 |       expect((await getCase(s.api, no)).slaLevel).toBe(level);
       |                                                   ^ Error: expect(received).toBe(expected) // Object.is equality
  1364 |       await s.page.goto(`/citizen/cases/${no}`);
  1365 |       await expectLevel(s.page, level);
  1366 |     });
  1367 |   }
  1368 | 
  1369 |   await test.step('ส่วน A คำขอใหม่ กำหนด ศ. 4 ธ.ค. 16:30', async () => {
  1370 |     await reset();
  1371 |     const s = await citizenSession(browser, ID.SOMCHAI);
  1372 |     const paid = await newPaid({ api: s.api, service: 'SV-01', qty: 1 });
  1373 |     expect(paid.caseNo).toBe(caseNo(31));
  1374 |     const rows: Array<[string, SlaLevel]> = [
  1375 |       ['2026-12-01T09:00:00+07:00', 'normal'],
  1376 |       ['2026-12-02T09:00:00+07:00', 'normal'],
  1377 |       ['2026-12-03T09:00:00+07:00', 'near'],
  1378 |       ['2026-12-04T16:30:00+07:00', 'near'],
  1379 |       ['2026-12-04T16:30:01+07:00', 'overdue'],
  1380 |       ['2026-12-04T16:31:00+07:00', 'overdue'],
  1381 |       ['2026-12-05T10:00:00+07:00', 'overdue'],
  1382 |     ];
  1383 |     for (const [clock, level] of rows) await levelAt(s, paid.caseNo, clock, level);
  1384 |   });
  1385 | 
  1386 |   await test.step('ส่วน B seed …000016 กำหนด อ. 8 ธ.ค. 16:30', async () => {
  1387 |     await reset();
  1388 |     const s = await citizenSession(browser, ID.PITI);
  1389 |     const rows: Array<[string, SlaLevel]> = [
  1390 |       ['2026-12-03T09:00:00+07:00', 'normal'],
  1391 |       ['2026-12-04T09:00:00+07:00', 'near'],
  1392 |       ['2026-12-08T16:30:00+07:00', 'near'],
  1393 |       ['2026-12-08T16:31:00+07:00', 'overdue'],
  1394 |     ];
  1395 |     for (const [clock, level] of rows) await levelAt(s, caseNo(16), clock, level);
  1396 |   });
  1397 | 
  1398 |   await test.step('ส่วน C seed ที่ 09:00 (คิว + หน้าเคส)', async () => {
  1399 |     await reset();
  1400 |     const o = await staffSession(browser, 'off.reg1');
  1401 |     await o.page.goto('/officer/queue');
  1402 |     const expected: Array<[number, SlaLevel]> = [
  1403 |       [20, 'overdue'],
  1404 |       [22, 'near'],
  1405 |       [24, 'near'],
  1406 |       [25, 'normal'],
  1407 |     ];
  1408 |     for (const [n, level] of expected) {
  1409 |       const row = queueRow(o.page, caseNo(n));
  1410 |       await expect(row.getByTestId('row-sla-level')).toHaveText(LEVEL_TH[level]);
  1411 |       await expect(row).toHaveAttribute('data-sla-level', level);
  1412 |     }
  1413 |     for (const [n, level] of expected) {
  1414 |       await o.page.goto(`/officer/cases/${caseNo(n)}`);
  1415 |       await expectLevel(o.page, level);
  1416 |       expect((await getCase(o.api, caseNo(n))).slaLevel).toBe(level);
  1417 |     }
  1418 |     const somchai = await citizenSession(browser, ID.SOMCHAI);
  1419 |     await somchai.page.goto(`/citizen/cases/${caseNo(17)}`);
  1420 |     await expectLevel(somchai.page, 'paused');
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
```