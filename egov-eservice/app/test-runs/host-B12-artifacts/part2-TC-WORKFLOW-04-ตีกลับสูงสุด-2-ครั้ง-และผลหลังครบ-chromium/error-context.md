# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-WORKFLOW-04 ตีกลับสูงสุด 2 ครั้ง และผลหลังครบ
- Location: tests\part2.spec.ts:409:1

# Error details

```
Error: expect(locator).toHaveCount(expected) failed

Locator:  getByTestId('return-btn')
Expected: 0
Received: 1
Timeout:  7000ms

Call log:
  - Expect "toHaveCount" getByTestId('return-btn') with timeout 7000ms
  - waiting for getByTestId('return-btn')
    17 × locator resolved to 1 element
       - unexpected value "1"

```

# Page snapshot

```yaml
- generic [active] [ref=f4e1]:
  - link "ข้ามไปเนื้อหาหลัก" [ref=f4e2] [cursor=pointer]:
    - /url: "#main"
  - banner [ref=f4e3]:
    - generic [ref=f4e4]:
      - link "e-Service กลาง เทศบาลนครตัวอย่าง" [ref=f4e5] [cursor=pointer]:
        - /url: /
      - navigation "เมนูหลัก" [ref=f4e6]:
        - list [ref=f4e7]:
          - listitem [ref=f4e8]:
            - link "คิวงาน" [ref=f4e9] [cursor=pointer]:
              - /url: /officer/queue
      - generic [ref=f4e10]:
        - generic [ref=f4e11]:
          - text: เจ้าหน้าที่ทะเบียน 1
          - generic [ref=f4e12]: เจ้าหน้าที่
        - link "แจ้งเตือน 3" [ref=f4e13] [cursor=pointer]:
          - /url: /notifications
          - text: แจ้งเตือน
          - generic [ref=f4e14]: "3"
        - button "ออกจากระบบ" [ref=f4e16] [cursor=pointer]
  - main [ref=f4e17]:
    - paragraph [ref=f4e18]:
      - link "← คิวงาน" [ref=f4e19] [cursor=pointer]:
        - /url: /officer/queue
    - heading "คำขอ EG-2569-000020" [level=1] [ref=f4e20]
    - region "รายละเอียดคำขอ" [ref=f4e21]:
      - heading "รายละเอียดคำขอ" [level=2] [ref=f4e22]
      - generic [ref=f4e23]:
        - term [ref=f4e24]: สถานะ
        - definition [ref=f4e25]:
          - generic [ref=f4e26]: กำลังตรวจสอบ
        - term [ref=f4e27]: บริการ
        - definition [ref=f4e28]: SV-01 ขอหนังสือรับรอง
        - term [ref=f4e29]: จำนวน
        - definition [ref=f4e30]: 1 ฉบับ
        - term [ref=f4e31]: ค่าธรรมเนียม
        - definition [ref=f4e32]: ฿20
        - term [ref=f4e33]: ผู้ยื่น
        - definition [ref=f4e34]: สมชาย ใจดี
        - term [ref=f4e35]: เลขบัตรประชาชน
        - definition [ref=f4e36]:
          - generic [ref=f4e37]:
            - text: X-XXXX-XXXXX-45-6
            - button "แสดงเลขเต็ม" [ref=f4e38] [cursor=pointer]
        - term [ref=f4e39]: ชำระเมื่อ
        - definition [ref=f4e40]:
          - time [ref=f4e41]: 25 พ.ย. 2569 10:00
        - term [ref=f4e42]: กำหนดเสร็จ
        - definition [ref=f4e43]:
          - time [ref=f4e44]: 30 พ.ย. 2569 16:30
        - term [ref=f4e45]: ระดับเตือน
        - definition [ref=f4e46]:
          - generic [ref=f4e47]: เกินกำหนด
        - term [ref=f4e48]: ผู้ถือเรื่อง
        - definition [ref=f4e49]: off.reg1
        - term [ref=f4e50]: ตีกลับแล้ว
        - definition [ref=f4e51]: 2 ครั้ง (สูงสุด 2)
        - term [ref=f4e52]: ผู้ออกเอกสาร
        - definition [ref=f4e53]: เจ้าหน้าที่ทะเบียน 1
    - region "ดำเนินการ" [ref=f4e54]:
      - heading "ดำเนินการ" [level=2] [ref=f4e55]
      - button "อนุมัติ" [ref=f4e58] [cursor=pointer]
      - group [ref=f4e59]:
        - generic "ตีกลับ" [ref=f4e60] [cursor=pointer]
      - group [ref=f4e61]:
        - generic "ไม่อนุมัติ" [ref=f4e62] [cursor=pointer]
    - region "เอกสารแนบ" [ref=f4e63]:
      - heading "เอกสารแนบ" [level=2] [ref=f4e64]
      - list [ref=f4e65]:
        - listitem [ref=f4e66]:
          - text: "บัตรประชาชน:"
          - link "id-card.pdf" [ref=f4e67] [cursor=pointer]:
            - /url: /api/files/f_seed_000020_id-card
          - text: (1 KB)
    - region "ไทม์ไลน์" [ref=f4e68]:
      - heading "ไทม์ไลน์" [level=2] [ref=f4e69]
      - list [ref=f4e70]:
        - listitem [ref=f4e71]:
          - time [ref=f4e72]: 25 พ.ย. 2569 10:00
          - text: · ชำระค่าธรรมเนียมและส่งคำขอแล้ว (ใบเสร็จ RC-2569-000020)
        - listitem [ref=f4e73]:
          - time [ref=f4e74]: 25 พ.ย. 2569 10:30
          - text: · off.reg1 รับเรื่อง
        - listitem [ref=f4e75]:
          - time [ref=f4e76]: 1 ธ.ค. 2569 09:00
          - text: "· off.reg1 ตีกลับ ครั้งที่ 1: xxxxxxxxxx"
        - listitem [ref=f4e77]:
          - time [ref=f4e78]: 1 ธ.ค. 2569 09:00
          - text: · ผู้ยื่นส่งแก้ไขเอกสาร (หยุดนับ 0 วันทำการ)
        - listitem [ref=f4e79]:
          - time [ref=f4e80]: 1 ธ.ค. 2569 09:00
          - text: "· off.reg1 ตีกลับ ครั้งที่ 2: xxxxxxxxxx"
        - listitem [ref=f4e81]:
          - time [ref=f4e82]: 1 ธ.ค. 2569 09:00
          - text: · ผู้ยื่นส่งแก้ไขเอกสาร (หยุดนับ 0 วันทำการ)
  - contentinfo [ref=f4e83]:
    - paragraph [ref=f4e84]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  339 |   await reset();
  340 |   const reg2 = await staffSession(browser, 'off.reg2');
  341 |   const p = reg2.page;
  342 | 
  343 |   await test.step('1 ขั้น 1/3 ฝ่ายทะเบียน', async () => {
  344 |     await openOfficer(p, NO);
  345 |     await expect(tid(p, 'case-step')).toHaveText('ขั้นตอน 1/3 · ฝ่ายทะเบียน');
  346 |     await expect(tid(p, 'case-fee')).toHaveText('฿1,010');
  347 |     await expect(tid(p, 'forward-btn')).toHaveCount(1);
  348 |   });
  349 | 
  350 |   await test.step('2 ส่งต่อ → ขั้น 2/3 ฝ่ายโยธา (ยัง IN_REVIEW ไม่มีผู้รับ)', async () => {
  351 |     await uiForward(p);
  352 |     await expectStatus(p, 'IN_REVIEW');
  353 |     await expect(tid(p, 'case-step')).toHaveText('ขั้นตอน 2/3 · ฝ่ายโยธา');
  354 |     await expect(tid(p, 'case-owner')).toHaveText('ยังไม่มีผู้รับ');
  355 |   });
  356 | 
  357 |   await test.step('3 คิวทะเบียนไม่มี …000012 (16 แถว) · งานในมือ off.reg2 = 8', async () => {
  358 |     await p.goto('/officer/queue');
  359 |     await expect(queueRow(p, NO)).toHaveCount(0);
  360 |     await expect(tid(p, 'queue-row')).toHaveCount(16);
  361 |     await expect(tid(p, 'workload-count')).toHaveText('8');
  362 |   });
  363 | 
  364 |   const works = await staffSession(browser, 'off.works1');
  365 |   const w = works.page;
  366 |   await test.step('4 คิวโยธา 2 แถว', async () => {
  367 |     await w.goto('/officer/queue');
  368 |     await expect(tid(w, 'queue-row')).toHaveCount(2);
  369 |     expect(await caseOrder(w, 'queue-row')).toEqual([caseNo(10), NO]);
  370 |     await expect(tid(w, 'claim-btn')).toHaveCount(2);
  371 |   });
  372 | 
  373 |   await test.step('5 off.reg1 claim ข้ามแผนก → 403', async () => {
  374 |     const reg1 = await loginStaff('off.reg1');
  375 |     await expectApi(claimRaw(reg1, NO), 403, 'FORBIDDEN');
  376 |   });
  377 | 
  378 |   await test.step('6 off.works1 รับเรื่องแล้วส่งต่อ → ขั้น 3/3 หัวหน้าฝ่าย', async () => {
  379 |     await act(w, () => queueRow(w, NO).getByTestId('claim-btn').click());
  380 |     await openOfficer(w, NO);
  381 |     await expect(tid(w, 'case-owner')).toHaveText('off.works1');
  382 |     await uiForward(w);
  383 |     await expectStatus(w, 'PENDING_APPROVAL');
  384 |     await expect(tid(w, 'case-step')).toHaveText('ขั้นตอน 3/3 · หัวหน้าฝ่าย');
  385 |   });
  386 | 
  387 |   await test.step('7 หัวหน้าอนุมัติ', async () => {
  388 |     const { page: h } = await staffSession(browser, 'head1');
  389 |     await h.goto('/head/approvals');
  390 |     await expect(tid(h, 'approval-row')).toHaveCount(3);
  391 |     await expect(rowBy(h, 'approval-row', 'data-case-no', NO)).toHaveCount(1);
  392 |     await rowBy(h, 'approval-row', 'data-case-no', NO).getByTestId('approval-open').click();
  393 |     await waitPath(h, `/officer/cases/${NO}`);
  394 |     await act(h, () => tid(h, 'approve-btn').click());
  395 |     await expectStatus(h, 'APPROVED');
  396 |   });
  397 | 
  398 |   await test.step('8 ผู้ออกเอกสาร = ทะเบียนขั้นแรก (off.reg2)', async () => {
  399 |     await openOfficer(w, NO);
  400 |     await expect(tid(w, 'issue-btn')).toHaveCount(0);
  401 |     await openOfficer(p, NO);
  402 |     await expect(tid(p, 'issue-btn')).toHaveCount(1);
  403 |     await act(p, () => tid(p, 'issue-btn').click());
  404 |     await expectStatus(p, 'COMPLETED');
  405 |     await expectSigner(browser, await verifyCodeOnPage(p), STAFF.head1.name);
  406 |   });
  407 | });
  408 | 
  409 | test('TC-WORKFLOW-04 ตีกลับสูงสุด 2 ครั้ง และผลหลังครบ', async ({ browser }) => {
  410 |   test.setTimeout(240_000);
  411 | 
  412 |   await test.step('ส่วน A SV-01 …000020 ตีกลับครั้งที่ 1 2 ✓ ครั้งที่ 3 ✗ (จับ B12)', async () => {
  413 |     await reset();
  414 |     const NO = caseNo(20);
  415 |     const r1 = await staffSession(browser, 'off.reg1');
  416 |     const p = r1.page;
  417 |     const sc = await loginCitizen(ID.SOMCHAI);
  418 |     await openOfficer(p, NO);
  419 |     await expect(tid(p, 'return-count')).toHaveText('0');
  420 | 
  421 |     await uiReturn(p, R10);
  422 |     await expectStatus(p, 'NEED_FIX');
  423 |     await expect(tid(p, 'return-count')).toHaveText('1');
  424 | 
  425 |     await resubmit(sc, NO);
  426 |     const back = await getCase(r1.api, NO);
  427 |     expect(back.status).toBe('IN_REVIEW');
  428 |     expect(back.owner).toBe('off.reg1');
  429 | 
  430 |     await openOfficer(p, NO);
  431 |     await expectStatus(p, 'IN_REVIEW');
  432 |     await uiReturn(p, R10);
  433 |     await expectStatus(p, 'NEED_FIX');
  434 |     await expect(tid(p, 'return-count')).toHaveText('2');
  435 | 
  436 |     await resubmit(sc, NO);
  437 |     await openOfficer(p, NO);
  438 |     await expectStatus(p, 'IN_REVIEW');
> 439 |     await expect(tid(p, 'return-btn')).toHaveCount(0);
      |                                        ^ Error: expect(locator).toHaveCount(expected) failed
  440 |     const err = await expectApi(returnRaw(r1.api, NO, R10), 409, 'RETURN_LIMIT');
  441 |     expect(err.message).toBe(MSG.RETURN_LIMIT);
  442 |     const c = await getCase(r1.api, NO);
  443 |     expect(c.status).toBe('IN_REVIEW');
  444 |     expect(c.returnCount).toBe(2);
  445 |     await p.reload();
  446 |     await expectStatus(p, 'IN_REVIEW');
  447 |     await expect(tid(p, 'return-count')).toHaveText('2');
  448 |     await expect(tid(p, 'approve-btn')).toHaveCount(1);
  449 |     await expect(tid(p, 'reject-btn')).toHaveCount(1);
  450 |   });
  451 | 
  452 |   await test.step('ส่วน B seed …000023 ตีกลับแล้ว 2 ครั้ง', async () => {
  453 |     await reset();
  454 |     const NO = caseNo(23);
  455 |     const r1 = await staffSession(browser, 'off.reg1');
  456 |     const p = r1.page;
  457 |     await openOfficer(p, NO);
  458 |     await expect(tid(p, 'return-count')).toHaveText('2');
  459 |     await expect(tid(p, 'return-btn')).toHaveCount(0);
  460 |     const err = await expectApi(returnRaw(r1.api, NO, R10), 409, 'RETURN_LIMIT');
  461 |     expect(err.message).toBe(MSG.RETURN_LIMIT);
  462 |     expect((await getCase(r1.api, NO)).status).toBe('IN_REVIEW');
  463 |     await p.reload();
  464 |     await expectStatus(p, 'IN_REVIEW');
  465 |     await expect(tid(p, 'approve-btn')).toHaveCount(1);
  466 |     await expect(tid(p, 'reject-btn')).toHaveCount(1);
  467 |   });
  468 | 
  469 |   await test.step('ส่วน C SV-02 …000013 หลังตีกลับครบ → ส่งต่อหัวหน้าเท่านั้น', async () => {
  470 |     await reset();
  471 |     const NO = caseNo(13);
  472 |     const NOTE = 'ส่งต่อให้หัวหน้าพิจารณา';
  473 |     const r2 = await staffSession(browser, 'off.reg2');
  474 |     const p = r2.page;
  475 |     const sc = await loginCitizen(ID.SOMCHAI);
  476 |     expect((await returnCase(r2.api, NO, R10)).returnCount).toBe(1);
  477 |     await resubmit(sc, NO);
  478 |     expect((await returnCase(r2.api, NO, R10)).returnCount).toBe(2);
  479 |     await resubmit(sc, NO);
  480 | 
  481 |     await openOfficer(p, NO);
  482 |     await expectStatus(p, 'IN_REVIEW');
  483 |     await expect(tid(p, 'return-btn')).toHaveCount(0);
  484 |     await expect(tid(p, 'approve-btn')).toHaveCount(0);
  485 |     await expect(tid(p, 'reject-btn')).toHaveCount(0);
  486 |     await expect(tid(p, 'forward-btn')).toHaveCount(1);
  487 |     await expectApi(rejectRaw(r2.api, NO, R10), 403);
  488 |     expect((await getCase(r2.api, NO)).status).toBe('IN_REVIEW');
  489 | 
  490 |     await uiForward(p, NOTE);
  491 |     await expectStatus(p, 'PENDING_APPROVAL');
  492 | 
  493 |     const auditor = await staffSession(browser, 'audit1');
  494 |     await uiAudit(auditor.page, { event: 'FORWARD' });
  495 |     const row = rowBy(auditor.page, 'audit-row', 'data-case-no', NO);
  496 |     await expect(row).toHaveCount(1);
  497 |     await expect(row.getByTestId('audit-detail')).toContainText(NOTE);
  498 | 
  499 |     const { page: h } = await staffSession(browser, 'head1');
  500 |     await openOfficer(h, NO);
  501 |     await expect(tid(h, 'reject-btn')).toHaveCount(1);
  502 |     await expect(tid(h, 'approve-btn')).toHaveCount(1);
  503 |   });
  504 | });
  505 | 
  506 | test('TC-WORKFLOW-05 เหตุผล ≥ 10 ตัวอักษร (ตีกลับ/ไม่อนุมัติ)', async ({ browser }) => {
  507 |   test.setTimeout(240_000);
  508 | 
  509 |   await test.step('ส่วน A ตีกลับ …000020 (off.reg1)', async () => {
  510 |     await reset();
  511 |     const NO = caseNo(20);
  512 |     const r1 = await staffSession(browser, 'off.reg1');
  513 |     const p = r1.page;
  514 |     await openOfficer(p, NO);
  515 | 
  516 |     for (const [label, reason] of [
  517 |       ['9 ตัว', R9],
  518 |       ['เว้นวรรค 10 ตัว', SPACES10],
  519 |     ] as const) {
  520 |       await uiReturn(p, reason, false);
  521 |       await expect(tid(p, 'return-reason-error'), label).toHaveText(MSG.REASON_TOO_SHORT);
  522 |       const e = await expectApi(returnRaw(r1.api, NO, reason), 400, 'REASON_TOO_SHORT');
  523 |       expect(e.message).toBe(MSG.REASON_TOO_SHORT);
  524 |       expect((await getCase(r1.api, NO)).status, label).toBe('IN_REVIEW');
  525 |     }
  526 |     await openOfficer(p, NO);
  527 |     await expectStatus(p, 'IN_REVIEW');
  528 | 
  529 |     await uiReturn(p, R10);
  530 |     await expectStatus(p, 'NEED_FIX');
  531 |     const { page: c } = await citizenSession(browser, ID.SOMCHAI);
  532 |     await openCitizen(c, NO);
  533 |     await expect(tid(c, 'return-reason-display')).toHaveText(R10);
  534 |   });
  535 | 
  536 |   await test.step('ส่วน B ไม่อนุมัติ SV-01 …000026 (off.reg2)', async () => {
  537 |     await reset();
  538 |     const NO = caseNo(26);
  539 |     const r2 = await staffSession(browser, 'off.reg2');
```