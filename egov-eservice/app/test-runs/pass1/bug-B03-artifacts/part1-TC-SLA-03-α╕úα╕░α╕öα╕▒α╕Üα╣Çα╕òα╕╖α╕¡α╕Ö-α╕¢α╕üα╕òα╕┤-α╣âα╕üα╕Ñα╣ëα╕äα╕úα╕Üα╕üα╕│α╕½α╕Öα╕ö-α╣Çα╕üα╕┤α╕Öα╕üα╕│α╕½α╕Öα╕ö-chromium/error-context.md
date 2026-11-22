# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-SLA-03 ระดับเตือน ปกติ / ใกล้ครบกำหนด / เกินกำหนด
- Location: tests/part1.spec.ts:1349:1

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
  1255 |     await reset();
  1256 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1257 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1258 |     expect(paid.caseNo).toBe(NEW);
  1259 |     expect((await getCase(c.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1260 | 
  1261 |     await setClock('2026-12-02T11:00:00+07:00');
  1262 |     const o = await staffSession(browser, 'off.reg1');
  1263 |     await claim(o.api, NEW);
  1264 |     await returnCase(o.api, NEW, 'xxxxxxxxxx');
  1265 |     await o.page.goto(`/officer/cases/${NEW}`);
  1266 |     await expectStatus(o.page, 'NEED_FIX');
  1267 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1268 |     await expectStatus(c.page, 'NEED_FIX');
  1269 |     await expectLevel(c.page, 'paused');
  1270 |     await expect(tid(c.page, 'fix-deadline')).toHaveAttribute('data-iso', '2026-12-09T11:00:00+07:00');
  1271 | 
  1272 |     await setClock('2026-12-03T10:00:00+07:00');
  1273 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1274 |     await tid(c.page, 'submit-fix-btn').click();
  1275 |     await expectStatus(c.page, 'IN_REVIEW');
  1276 |     await expectDue(c.page, '8 ธ.ค. 2569 16:30', '2026-12-08T16:30:00+07:00');
  1277 |     await expectLevel(c.page, 'normal');
  1278 |     const got = await getCase(o.api, NEW);
  1279 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1280 |     expect(got.owner).toBe('off.reg1');
  1281 |     await o.page.goto(`/officer/cases/${NEW}`);
  1282 |     await expect(tid(o.page, 'case-owner')).toHaveText('off.reg1');
  1283 |   });
  1284 | 
  1285 |   await test.step('ส่วน 2 seed …000017 ส่งแก้ 1 ธ.ค. 09:00 (หยุด 2 วัน)', async () => {
  1286 |     await reset();
  1287 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1288 |     await c.page.goto(`/citizen/cases/${F01}`);
  1289 |     await expectLevel(c.page, 'paused');
  1290 |     await expect(tid(c.page, 'sla-due')).toHaveAttribute('data-iso', '2026-11-27T16:30:00+07:00');
  1291 |     await tid(c.page, 'submit-fix-btn').click();
  1292 |     await expectStatus(c.page, 'IN_REVIEW');
  1293 |     await expectDue(c.page, '1 ธ.ค. 2569 16:30', '2026-12-01T16:30:00+07:00');
  1294 |     await expectLevel(c.page, 'near');
  1295 |     const reg1 = await loginStaff('off.reg1');
  1296 |     const got = await getCase(reg1, F01);
  1297 |     expect(got.dueAt).toBe('2026-12-01T16:30:00+07:00');
  1298 |     expect(got.owner).toBe('off.reg1');
  1299 |   });
  1300 | 
  1301 |   await test.step('ส่วน 3 ส่งแก้ …000017 วันที่ 4 ธ.ค. 10:00 (หยุด 5 วัน)', async () => {
  1302 |     await reset();
  1303 |     await setClock('2026-12-04T10:00:00+07:00');
  1304 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1305 |     const r = await resubmit(c.api, F01);
  1306 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1307 |     const got = await getCase(c.api, F01);
  1308 |     expect(got.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1309 |     expect(got.slaLevel).toBe('near');
  1310 |     await c.page.goto(`/citizen/cases/${F01}`);
  1311 |     await expectLevel(c.page, 'near');
  1312 |   });
  1313 | 
  1314 |   await test.step('ส่วน 4 ตีกลับและส่งแก้วันเดียวกัน (หยุด 0 วัน)', async () => {
  1315 |     await reset();
  1316 |     const paid = await newPaid({ idNo: ID.SOMCHAI, service: 'SV-01', qty: 1 });
  1317 |     expect(paid.caseNo).toBe(NEW);
  1318 |     await setClock('2026-12-02T09:00:00+07:00');
  1319 |     const reg1 = await loginStaff('off.reg1');
  1320 |     await claim(reg1, NEW);
  1321 |     await returnCase(reg1, NEW);
  1322 |     await setClock('2026-12-02T15:00:00+07:00');
  1323 |     const r = await resubmit(paid.api, NEW);
  1324 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1325 |     expect((await getCase(paid.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1326 |   });
  1327 | 
  1328 |   await test.step('ส่วน 5 คร่อมสุดสัปดาห์/วันหยุด ส่งแก้หลัง 16:30', async () => {
  1329 |     await reset();
  1330 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1331 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1332 |     expect(paid.caseNo).toBe(NEW);
  1333 |     await setClock('2026-12-04T10:00:00+07:00');
  1334 |     const reg1 = await loginStaff('off.reg1');
  1335 |     await claim(reg1, NEW);
  1336 |     await returnCase(reg1, NEW);
  1337 |     await setClock('2026-12-08T17:00:00+07:00');
  1338 |     const r = await resubmit(c.api, NEW);
  1339 |     expect(r.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1340 |     const got = await getCase(c.api, NEW);
  1341 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1342 |     expect(got.slaLevel).toBe('overdue');
  1343 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1344 |     await expectDue(c.page, '8 ธ.ค. 2569 16:30', '2026-12-08T16:30:00+07:00');
  1345 |     await expectLevel(c.page, 'overdue');
  1346 |   });
  1347 | });
  1348 | 
  1349 | test('TC-SLA-03 ระดับเตือน ปกติ / ใกล้ครบกำหนด / เกินกำหนด', async ({ browser }) => {
  1350 |   test.setTimeout(300_000);
  1351 | 
  1352 |   async function levelAt(s: { page: Page; api: APIRequestContext }, no: string, clock: string, level: SlaLevel): Promise<void> {
  1353 |     await test.step(`${no} @ ${clock} → ${level}`, async () => {
  1354 |       await setClock(clock);
> 1355 |       expect((await getCase(s.api, no)).slaLevel).toBe(level);
       |                                                   ^ Error: expect(received).toBe(expected) // Object.is equality
  1356 |       await s.page.goto(`/citizen/cases/${no}`);
  1357 |       await expectLevel(s.page, level);
  1358 |     });
  1359 |   }
  1360 | 
  1361 |   await test.step('ส่วน A คำขอใหม่ กำหนด ศ. 4 ธ.ค. 16:30', async () => {
  1362 |     await reset();
  1363 |     const s = await citizenSession(browser, ID.SOMCHAI);
  1364 |     const paid = await newPaid({ api: s.api, service: 'SV-01', qty: 1 });
  1365 |     expect(paid.caseNo).toBe(caseNo(31));
  1366 |     const rows: Array<[string, SlaLevel]> = [
  1367 |       ['2026-12-01T09:00:00+07:00', 'normal'],
  1368 |       ['2026-12-02T09:00:00+07:00', 'normal'],
  1369 |       ['2026-12-03T09:00:00+07:00', 'near'],
  1370 |       ['2026-12-04T16:30:00+07:00', 'near'],
  1371 |       ['2026-12-04T16:30:01+07:00', 'overdue'],
  1372 |       ['2026-12-04T16:31:00+07:00', 'overdue'],
  1373 |       ['2026-12-05T10:00:00+07:00', 'overdue'],
  1374 |     ];
  1375 |     for (const [clock, level] of rows) await levelAt(s, paid.caseNo, clock, level);
  1376 |   });
  1377 | 
  1378 |   await test.step('ส่วน B seed …000016 กำหนด อ. 8 ธ.ค. 16:30', async () => {
  1379 |     await reset();
  1380 |     const s = await citizenSession(browser, ID.PITI);
  1381 |     const rows: Array<[string, SlaLevel]> = [
  1382 |       ['2026-12-03T09:00:00+07:00', 'normal'],
  1383 |       ['2026-12-04T09:00:00+07:00', 'near'],
  1384 |       ['2026-12-08T16:30:00+07:00', 'near'],
  1385 |       ['2026-12-08T16:31:00+07:00', 'overdue'],
  1386 |     ];
  1387 |     for (const [clock, level] of rows) await levelAt(s, caseNo(16), clock, level);
  1388 |   });
  1389 | 
  1390 |   await test.step('ส่วน C seed ที่ 09:00 (คิว + หน้าเคส)', async () => {
  1391 |     await reset();
  1392 |     const o = await staffSession(browser, 'off.reg1');
  1393 |     await o.page.goto('/officer/queue');
  1394 |     const expected: Array<[number, SlaLevel]> = [
  1395 |       [20, 'overdue'],
  1396 |       [22, 'near'],
  1397 |       [24, 'near'],
  1398 |       [25, 'normal'],
  1399 |     ];
  1400 |     for (const [n, level] of expected) {
  1401 |       const row = queueRow(o.page, caseNo(n));
  1402 |       await expect(row.getByTestId('row-sla-level')).toHaveText(LEVEL_TH[level]);
  1403 |       await expect(row).toHaveAttribute('data-sla-level', level);
  1404 |     }
  1405 |     for (const [n, level] of expected) {
  1406 |       await o.page.goto(`/officer/cases/${caseNo(n)}`);
  1407 |       await expectLevel(o.page, level);
  1408 |       expect((await getCase(o.api, caseNo(n))).slaLevel).toBe(level);
  1409 |     }
  1410 |     const somchai = await citizenSession(browser, ID.SOMCHAI);
  1411 |     await somchai.page.goto(`/citizen/cases/${caseNo(17)}`);
  1412 |     await expectLevel(somchai.page, 'paused');
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
```