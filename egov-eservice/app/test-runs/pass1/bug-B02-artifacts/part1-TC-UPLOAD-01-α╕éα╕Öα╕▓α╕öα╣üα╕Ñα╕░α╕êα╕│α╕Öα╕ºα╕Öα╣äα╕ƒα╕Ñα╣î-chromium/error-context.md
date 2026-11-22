# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-UPLOAD-01 ขนาดและจำนวนไฟล์
- Location: tests/part1.spec.ts:739:1

# Error details

```
Error: expect(locator).toHaveCount(expected) failed

Locator:  getByTestId('file-item')
Expected: 1
Received: 0
Timeout:  7000ms

Call log:
  - Expect "toHaveCount" getByTestId('file-item') with timeout 7000ms
  - waiting for getByTestId('file-item')
    18 × locator resolved to 0 elements
       - unexpected value "0"

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
            - link "คำขอของฉัน" [ref=f1e9] [cursor=pointer]:
              - /url: /citizen
      - generic [ref=f1e10]:
        - generic [ref=f1e11]:
          - text: สมชาย ใจดี
          - generic [ref=f1e12]: ประชาชน
        - button "ออกจากระบบ" [ref=f1e14] [cursor=pointer]
  - main [ref=f1e15]:
    - paragraph [ref=f1e16]:
      - link "← คำขอของฉัน" [ref=f1e17] [cursor=pointer]:
        - /url: /citizen
    - heading "ยื่นคำขอ ขอหนังสือรับรอง" [level=1] [ref=f1e18]
    - list "ขั้นตอนการยื่น" [ref=f1e19]:
      - listitem [ref=f1e20]: กรอกข้อมูล
      - listitem [ref=f1e21]: แนบเอกสาร
      - listitem [ref=f1e22]: ชำระเงิน
    - paragraph [ref=f1e23]:
      - strong [ref=f1e24]: 2/3 แนบเอกสาร
    - paragraph [ref=f1e25]:
      - text: รหัสร่าง
      - strong [ref=f1e26]: DR-0003
    - paragraph [ref=f1e27]: จำนวน 1 ฉบับ · ค่าธรรมเนียม ฿20
    - region "แนบเอกสาร" [ref=f1e28]:
      - heading "แนบเอกสาร" [level=2] [ref=f1e29]
      - paragraph [ref=f1e30]: รองรับ PDF, JPG, PNG ไฟล์ละไม่เกิน 5 MB · แนบได้สูงสุด 5 ไฟล์ต่อคำขอ (แนบแล้ว 0 ไฟล์)
      - generic [ref=f1e31]:
        - generic [ref=f1e32]: บัตรประชาชน ✱ (บังคับ) · PDF, JPG, PNG ไม่เกิน 5 MB
        - button "บัตรประชาชน ✱ (บังคับ) · PDF, JPG, PNG ไม่เกิน 5 MB" [ref=f1e33]
      - generic [ref=f1e34]:
        - generic [ref=f1e35]: เอกสารเพิ่มเติม (ไม่บังคับ) · PDF, JPG, PNG ไม่เกิน 5 MB
        - button "เอกสารเพิ่มเติม (ไม่บังคับ) · PDF, JPG, PNG ไม่เกิน 5 MB" [ref=f1e36]
      - alert [ref=f1e38]: ไฟล์ใหญ่เกิน 5 MB
      - heading "ไฟล์ที่แนบแล้ว" [level=3] [ref=f1e39]
      - list
      - paragraph [ref=f1e41]: "ยังขาดเอกสาร: บัตรประชาชน"
      - paragraph [ref=f1e42]:
        - link "ย้อนกลับ" [ref=f1e43] [cursor=pointer]:
          - /url: /citizen/new/SV-01?draft=DR-0003&step=1
        - button "ไปชำระเงิน" [disabled] [ref=f1e44]
  - contentinfo [ref=f1e45]:
    - paragraph [ref=f1e46]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  652 |     expect(await myCases(api)).toHaveLength(10);
  653 |     expect(await myDrafts(api)).toHaveLength(3);
  654 |   });
  655 | 
  656 |   await test.step('ส่วน B ยกเลิก (RESET)', async () => {
  657 |     await reset();
  658 |     const { page: p } = await citizenSession(browser, ID.SOMCHAI);
  659 |     await p.goto(`/citizen/cases/${S03}`);
  660 |     await expect(tid(p, 'cancel-case-btn')).toHaveCount(1);
  661 |     await tid(p, 'cancel-case-btn').click();
  662 |     await expect(tid(p, 'cancel-confirm-text')).toHaveText(MSG.NO_REFUND);
  663 |     await tid(p, 'confirm-cancel-btn').click();
  664 |     await expectStatus(p, 'CANCELLED');
  665 |     await expect(tid(p, 'no-refund-note')).toHaveText(MSG.NO_REFUND);
  666 |     await expect(tid(p, 'cancel-case-btn')).toHaveCount(0);
  667 | 
  668 |     const o = await staffSession(browser, 'off.reg1');
  669 |     await o.page.goto('/officer/queue');
  670 |     await expect(tid(o.page, 'queue-row')).toHaveCount(16);
  671 |     await expect(queueRow(o.page, S03)).toHaveCount(0);
  672 | 
  673 |     const e = await staffSession(browser, 'exec1');
  674 |     await e.page.goto('/dashboard');
  675 |     await expect(tid(e.page, 'kpi-backlog')).toHaveText('20');
  676 |     await expect(tid(e.page, 'kpi-received')).toHaveText('3');
  677 |   });
  678 | 
  679 |   await test.step('ส่วน C ยกเลิกไม่ได้เมื่อมีผู้รับ (RESET)', async () => {
  680 |     await reset();
  681 |     const reg1 = await loginStaff('off.reg1');
  682 |     await claim(reg1, S03);
  683 |     const { page: p, api } = await citizenSession(browser, ID.SOMCHAI);
  684 |     await p.goto(`/citizen/cases/${S03}`);
  685 |     await expectStatus(p, 'IN_REVIEW');
  686 |     await expect(tid(p, 'cancel-case-btn')).toHaveCount(0);
  687 |     const b = await expectApi(cancelRaw(api, S03), 409, 'CANNOT_CANCEL');
  688 |     expect(b.message).toBe(MSG.CANNOT_CANCEL);
  689 |     await expectApi(cancelRaw(api, caseNo(13)), 409, 'CANNOT_CANCEL');
  690 |     expect((await getCase(api, S03)).status).toBe('IN_REVIEW');
  691 |     expect((await getCase(api, caseNo(13))).status).toBe('IN_REVIEW');
  692 |   });
  693 | 
  694 |   await test.step('ส่วน E ลบร่าง (RESET)', async () => {
  695 |     await reset();
  696 |     const { page: p, api } = await citizenSession(browser, ID.SOMCHAI);
  697 |     await expectApi(api.delete('/api/drafts/DR-0001'), 204);
  698 |     await expectApi(api.get('/api/drafts/DR-0001'), 404, 'NOT_FOUND');
  699 |     await p.goto('/citizen');
  700 |     await expect(tid(p, 'my-draft-row')).toHaveCount(1);
  701 |     await expect(tid(p, 'my-draft-row')).toHaveAttribute('data-draft-id', 'DR-0002');
  702 |     await expectApi(api.delete('/api/drafts/DR-0002'), 204);
  703 |     await expectApi(api.get('/api/payments/PP-0001'), 404);
  704 |     await expectApi(payRaw('PP-0001', 500), 404);
  705 |     expect(await myCases(api)).toHaveLength(10);
  706 |   });
  707 | 
  708 |   await test.step('ส่วน F ยกเลิกชนกับรับเรื่อง (RESET · คนละ context)', async () => {
  709 |     await reset();
  710 |     const citizen = await loginCitizen(ID.SOMCHAI);
  711 |     const reg1 = await loginStaff('off.reg1');
  712 |     const [rc, rl] = await Promise.all([cancelRaw(citizen, S03), claimRaw(reg1, S03)]);
  713 |     const cs = rc.status();
  714 |     const ls = rl.status();
  715 |     const cb = await bodyOf(rc);
  716 |     const lb = await bodyOf(rl);
  717 |     expect([cs, ls].filter((s) => s === 200), `cancel=${cs} ${JSON.stringify(cb)} claim=${ls} ${JSON.stringify(lb)}`).toHaveLength(1);
  718 |     const c = await getCase(reg1, S03);
  719 |     const mine = await queueItems(reg1, 'mine');
  720 |     if (cs === 200) {
  721 |       expect(ls).toBe(409);
  722 |       expect(lb.code).toBe('INVALID_STATE');
  723 |       expect(c.status).toBe('CANCELLED');
  724 |       expect(c.owner || null).toBeNull();
  725 |       expect(mine).toHaveLength(3);
  726 |     } else {
  727 |       expect(ls).toBe(200);
  728 |       expect(cs).toBe(409);
  729 |       expect(cb.code).toBe('CANNOT_CANCEL');
  730 |       expect(c.status).toBe('IN_REVIEW');
  731 |       expect(c.owner).toBe('off.reg1');
  732 |       expect(mine).toHaveLength(4);
  733 |     }
  734 |   });
  735 | });
  736 | 
  737 | // ═══════════════════════════════════ UPLOAD ═══════════════════════════════════
  738 | 
  739 | test('TC-UPLOAD-01 ขนาดและจำนวนไฟล์', async ({ browser }) => {
  740 |   test.setTimeout(240_000);
  741 |   await reset();
  742 |   const { page: p, api } = await citizenSession(browser, ID.SOMCHAI);
  743 |   const items = tid(p, 'file-item');
  744 | 
  745 |   await test.step('ขนาด (หน้าจอ)', async () => {
  746 |     await uiWizardToUpload(p, 'SV-01', { qty: 1 });
  747 |     await uiUpload(p, 'id-card', 'size-5242879.pdf');
  748 |     await expect(items).toHaveCount(1);
  749 |     await uiRemoveFile(p, 'size-5242879.pdf');
  750 | 
  751 |     await uiUpload(p, 'id-card', 'size-5242880.pdf');
> 752 |     await expect(items).toHaveCount(1); // ขอบ ≤ 5 MB รับ (B02)
      |                         ^ Error: expect(locator).toHaveCount(expected) failed
  753 |     await expect(tid(p, 'upload-error')).toBeHidden();
  754 |     await uiRemoveFile(p, 'size-5242880.pdf');
  755 | 
  756 |     await uiUpload(p, 'id-card', 'size-5242881.pdf');
  757 |     await expect(tid(p, 'upload-error')).toHaveText(MSG.FILE_TOO_LARGE);
  758 |     await expect(items).toHaveCount(0);
  759 |   });
  760 | 
  761 |   await test.step('ขนาด (API)', async () => {
  762 |     const d = await createDraft(api, 'SV-01', { qty: 1 });
  763 |     const a = await upload(api, d.draftId, 'id-card', 'size-5242879.pdf');
  764 |     expect(a.size).toBe(5242879);
  765 |     const b = await upload(api, d.draftId, 'extra', 'size-5242880.pdf');
  766 |     expect(b.size).toBe(5242880);
  767 |     const c = await expectApi(uploadRaw(api, d.draftId, 'extra', 'size-5242881.pdf'), 400, 'FILE_TOO_LARGE');
  768 |     expect(c.message).toBe(MSG.FILE_TOO_LARGE);
  769 |   });
  770 | 
  771 |   await test.step('จำนวน (หน้าจอ)', async () => {
  772 |     await uiWizardToUpload(p, 'SV-01', { qty: 1 });
  773 |     await uiUpload(p, 'id-card', 'id-card.pdf');
  774 |     await expect(items).toHaveCount(1);
  775 |     for (let i = 1; i <= 4; i++) {
  776 |       await uiUpload(p, 'extra', `multi-${i}.pdf`);
  777 |       await expect(items).toHaveCount(1 + i);
  778 |     }
  779 |     await expect(tid(p, 'upload-error')).toBeHidden();
  780 |     await uiUpload(p, 'extra', 'multi-5.pdf');
  781 |     await expect(tid(p, 'upload-error')).toHaveText(MSG.FILE_COUNT);
  782 |     await expect(items).toHaveCount(5);
  783 |     await expect(fileItem(p, 'multi-5.pdf')).toHaveCount(0);
  784 | 
  785 |     await uiRemoveFile(p, 'multi-4.pdf');
  786 |     await uiUpload(p, 'extra', 'multi-5.pdf');
  787 |     await expect(items).toHaveCount(5);
  788 |     await expect(fileItem(p, 'multi-5.pdf')).toHaveCount(1);
  789 |   });
  790 | 
  791 |   await test.step('จำนวน (API) 400 FILE_COUNT', async () => {
  792 |     const d = await createDraft(api, 'SV-01', { qty: 1 });
  793 |     await upload(api, d.draftId, 'id-card', 'id-card.pdf');
  794 |     for (let i = 1; i <= 4; i++) await upload(api, d.draftId, 'extra', `multi-${i}.pdf`);
  795 |     const b = await expectApi(uploadRaw(api, d.draftId, 'extra', 'multi-5.pdf'), 400, 'FILE_COUNT');
  796 |     expect(b.message).toBe(MSG.FILE_COUNT);
  797 |   });
  798 | });
  799 | 
  800 | test('TC-UPLOAD-02 ชนิดไฟล์จากเนื้อไฟล์', async ({ browser }) => {
  801 |   await reset();
  802 |   const { page: p, api } = await citizenSession(browser, ID.SOMCHAI);
  803 |   const items = tid(p, 'file-item');
  804 |   const rejected = [
  805 |     filePayload('fake-text.pdf'),
  806 |     filePayload('fake-text.jpg'),
  807 |     filePayload('exe-as.png'),
  808 |     filePayload('notes.txt'),
  809 |     filePayload('fake-text.pdf', 'application/pdf'), // ไม่เชื่อ Content-Type (A-49)
  810 |   ];
  811 | 
  812 |   await test.step('หน้าจอ', async () => {
  813 |     await uiWizardToUpload(p, 'SV-01', { qty: 1 });
  814 |     for (const name of ['ok-id.pdf', 'real.jpg', 'real.png']) {
  815 |       await uiUpload(p, 'id-card', name);
  816 |       await expect(items).toHaveCount(1);
  817 |       await expect(fileItem(p, name)).toHaveCount(1);
  818 |       await uiRemoveFile(p, name);
  819 |     }
  820 |     for (const f of rejected) {
  821 |       await uiUpload(p, 'id-card', f);
  822 |       await expect(tid(p, 'upload-error')).toHaveText(MSG.FILE_TYPE);
  823 |       await expect(items).toHaveCount(0);
  824 |     }
  825 |   });
  826 | 
  827 |   await test.step('API: รับ PDF JPG PNG', async () => {
  828 |     for (const name of ['ok-id.pdf', 'real.jpg', 'real.png']) {
  829 |       const d = await createDraft(api, 'SV-01', { qty: 1 });
  830 |       const b = await upload(api, d.draftId, 'id-card', name);
  831 |       expect(b.docKey).toBe('id-card');
  832 |       expect(b.size).toBe(1024);
  833 |     }
  834 |   });
  835 | 
  836 |   await test.step('API: ปฏิเสธ 400 FILE_TYPE และไม่ถูกเก็บ', async () => {
  837 |     const d = await createDraft(api, 'SV-01', { qty: 1 });
  838 |     const before = await expectApi(api.get(`/api/drafts/${d.draftId}`), 200);
  839 |     for (const f of rejected) {
  840 |       const b = await expectApi(uploadRaw(api, d.draftId, 'id-card', f), 400, 'FILE_TYPE');
  841 |       expect(b.message).toBe(MSG.FILE_TYPE);
  842 |     }
  843 |     const after = await expectApi(api.get(`/api/drafts/${d.draftId}`), 200);
  844 |     if (Array.isArray(before.files) || Array.isArray(after.files)) expect(after.files ?? []).toHaveLength((before.files ?? []).length);
  845 |     // ไฟล์ที่ถูกปฏิเสธไม่ถูกนับ: แนบไฟล์ถูกได้อีกครบ 5
  846 |     await upload(api, d.draftId, 'id-card', 'id-card.pdf');
  847 |     for (let i = 1; i <= 4; i++) await upload(api, d.draftId, 'extra', `multi-${i}.pdf`);
  848 |     await expectApi(api.post(`/api/drafts/${d.draftId}/payment`), 201);
  849 |   });
  850 | });
  851 | 
  852 | // ═══════════════════════════════════ PAY ═══════════════════════════════════
```