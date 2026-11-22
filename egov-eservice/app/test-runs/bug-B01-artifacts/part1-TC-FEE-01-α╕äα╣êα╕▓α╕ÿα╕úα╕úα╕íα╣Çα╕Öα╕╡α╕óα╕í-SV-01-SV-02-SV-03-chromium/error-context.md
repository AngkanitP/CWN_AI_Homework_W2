# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-FEE-01 ค่าธรรมเนียม SV-01 / SV-02 / SV-03
- Location: tests/part1.spec.ts:408:1

# Error details

```
Error: expect(locator).toHaveText(expected) failed

Locator:  getByTestId('fee-total')
Expected: "฿1,010"
Received: "฿1,000"
Timeout:  7000ms

Call log:
  - Expect "toHaveText" getByTestId('fee-total') with timeout 7000ms
  - waiting for getByTestId('fee-total')
    18 × locator resolved to <strong aria-live="polite" data-testid="fee-total">฿1,000</strong>
       - unexpected value "฿1,000"

```

```yaml
- strong: ฿1,000
```

# Test source

```ts
  316 |       await expect(tid(p, 'reg-error-mobile')).toHaveText(MSG.INVALID_MOBILE);
  317 |       expect(new URL(p.url()).pathname).toBe('/register');
  318 |     });
  319 |   }
  320 |   // 5 ไม่ติ๊กยินยอม
  321 |   await submitReg('0845678901', false);
  322 |   await expect(tid(p, 'reg-error-consent')).toHaveText(MSG.CONSENT_REQUIRED);
  323 |   expect(new URL(p.url()).pathname).toBe('/register');
  324 |   // 6 ถูกต้อง อีเมลว่าง
  325 |   await submitReg('0845678901', true);
  326 |   await waitPath(p, '/citizen');
  327 |   await expect(tid(p, 'citizen-welcome')).toHaveText('สวัสดี มานะ ตั้งใจ');
  328 |   // 7 ออกแล้วเข้าใหม่ → /citizen ตรง ๆ
  329 |   await uiLogout(p);
  330 |   await uiLoginCitizen(p, ID.MANA);
  331 |   await waitPath(p, '/citizen');
  332 | 
  333 |   // 8 API (RESET)
  334 |   await reset();
  335 |   const api = await newApi();
  336 |   await expectApi(api.post('/api/auth/thaid/start', { data: { idNo: ID.MANA } }), 200);
  337 |   const v = await expectApi(api.post('/api/auth/thaid/verify', { data: { idNo: ID.MANA, otp: OTP_OK } }), 200);
  338 |   expect(v.registered).toBe(false);
  339 |   const b1 = await expectApi(
  340 |     api.post('/api/auth/register', { data: { mobile: '081234567', email: '', consent: true } }),
  341 |     400,
  342 |     'INVALID_MOBILE',
  343 |   );
  344 |   expect(b1.message).toBe(MSG.INVALID_MOBILE);
  345 |   const b2 = await expectApi(
  346 |     api.post('/api/auth/register', { data: { mobile: '0845678901', email: '', consent: false } }),
  347 |     400,
  348 |     'CONSENT_REQUIRED',
  349 |   );
  350 |   expect(b2.message).toBe(MSG.CONSENT_REQUIRED);
  351 | });
  352 | 
  353 | test('TC-AUTH-04 เจ้าหน้าที่ SSO จำลองและหน้าตั้งต้นตามบทบาท', async ({ browser }) => {
  354 |   await reset();
  355 |   const { page: p } = await newSession(browser);
  356 | 
  357 |   for (const [username, info] of Object.entries(STAFF) as Array<[StaffUser, (typeof STAFF)[StaffUser]]>) {
  358 |     await test.step(username, async () => {
  359 |       await p.goto('/login');
  360 |       await tid(p, 'login-tab-staff').click();
  361 |       await expect(tid(p, 'staff-submit')).toHaveText('เข้าสู่ระบบเจ้าหน้าที่ (SSO ภาครัฐ จำลอง)');
  362 |       await tid(p, 'staff-username').fill(username);
  363 |       await tid(p, 'staff-password').fill('Test@1234');
  364 |       await tid(p, 'staff-submit').click();
  365 |       await waitPath(p, info.landing);
  366 |       await expect(tid(p, 'user-name')).toHaveText(info.name);
  367 |       const role = tid(p, 'user-role');
  368 |       await expect(role).toHaveText(info.roleText);
  369 |       await expect(role).toHaveAttribute('data-role', info.role);
  370 |       if (info.dept) await expect(role).toHaveAttribute('data-dept', info.dept);
  371 |       await uiLogout(p);
  372 |     });
  373 |   }
  374 | 
  375 |   await test.step('API: role / dept / landing', async () => {
  376 |     for (const [username, info] of Object.entries(STAFF) as Array<[StaffUser, (typeof STAFF)[StaffUser]]>) {
  377 |       const api = await newApi();
  378 |       const b = await expectApi(api.post('/api/auth/staff/login', { data: { username, password: 'Test@1234' } }), 200);
  379 |       expect(b.role).toBe(info.role);
  380 |       expect(b.landing).toBe(info.landing);
  381 |       if (info.dept) expect(b.dept).toBe(info.dept);
  382 |     }
  383 |   });
  384 | 
  385 |   for (const [username, password] of [
  386 |     ['off.reg1', 'wrong'],
  387 |     ['nobody', 'Test@1234'],
  388 |     [ID.SOMCHAI, 'Test@1234'],
  389 |   ]) {
  390 |     await test.step(`ล็อกอินไม่ได้: ${username} / ${password}`, async () => {
  391 |       await uiStaffSubmit(p, username, password);
  392 |       await expect(tid(p, 'staff-error')).toHaveText(MSG.INVALID_CREDENTIALS);
  393 |       expect(new URL(p.url()).pathname).toBe('/login');
  394 |       const api = await newApi();
  395 |       const b = await expectApi(api.post('/api/auth/staff/login', { data: { username, password } }), 401, 'INVALID_CREDENTIALS');
  396 |       expect(b.message).toBe(MSG.INVALID_CREDENTIALS);
  397 |     });
  398 |   }
  399 | 
  400 |   await test.step('หลังออกจากระบบเปิด /officer/queue → /login', async () => {
  401 |     await p.goto('/officer/queue');
  402 |     await waitPath(p, '/login');
  403 |   });
  404 | });
  405 | 
  406 | // ═══════════════════════════════════ FEE ═══════════════════════════════════
  407 | 
  408 | test('TC-FEE-01 ค่าธรรมเนียม SV-01 / SV-02 / SV-03', async ({ browser }) => {
  409 |   await reset();
  410 |   const { page: p, api } = await citizenSession(browser, ID.SOMCHAI);
  411 | 
  412 |   type Row = { v: number; fee?: number; err?: string; code?: string };
  413 |   async function check(input: 'area-input' | 'qty-input', r: Row): Promise<void> {
  414 |     await fillField(tid(p, input), String(r.v));
  415 |     if (r.fee !== undefined) {
> 416 |       await expect(tid(p, 'fee-total')).toHaveText(baht(r.fee));
      |                                         ^ Error: expect(locator).toHaveText(expected) failed
  417 |       await expect(tid(p, 'fee-error')).toBeHidden();
  418 |       await expect(tid(p, 'to-upload-btn')).toBeEnabled();
  419 |     } else {
  420 |       await expect(tid(p, 'fee-total')).toHaveText('–');
  421 |       await expect(tid(p, 'fee-error')).toHaveText(r.err!);
  422 |       await expect(tid(p, 'to-upload-btn')).toBeDisabled();
  423 |     }
  424 |   }
  425 |   async function checkApi(data: Record<string, unknown>, r: Row): Promise<void> {
  426 |     if (r.fee !== undefined) {
  427 |       const b = await expectApi(api.post('/api/drafts', { data }), 201);
  428 |       expect(b.fee).toBe(r.fee);
  429 |     } else {
  430 |       const b = await expectApi(api.post('/api/drafts', { data }), 400, r.code);
  431 |       expect(b.message).toBe(r.err);
  432 |     }
  433 |   }
  434 | 
  435 |   // SV-03: 1–100 = ฿1,000 · 101–500 = 1,000 + 10 × (พื้นที่ − 100)
  436 |   const sv03: Row[] = [
  437 |     { v: 0, err: MSG.INVALID_AREA, code: 'INVALID_AREA' },
  438 |     { v: -1, err: MSG.INVALID_AREA, code: 'INVALID_AREA' },
  439 |     { v: 1, fee: 1000 },
  440 |     { v: 100, fee: 1000 },
  441 |     { v: 101, fee: 1010 },
  442 |     { v: 102, fee: 1020 },
  443 |     { v: 250, fee: 2500 },
  444 |     { v: 300, fee: 3000 },
  445 |     { v: 499, fee: 4990 },
  446 |     { v: 500, fee: 5000 },
  447 |     { v: 501, err: MSG.AREA_TOO_LARGE, code: 'AREA_TOO_LARGE' },
  448 |   ];
  449 |   await p.goto('/citizen/new/SV-03');
  450 |   for (const r of sv03) {
  451 |     await test.step(`SV-03 พื้นที่ ${r.v}`, async () => {
  452 |       await check('area-input', r);
  453 |       await checkApi({ serviceId: 'SV-03', areaSqm: r.v }, r);
  454 |     });
  455 |   }
  456 | 
  457 |   // SV-01: ฿20 ต่อฉบับ 1–5
  458 |   const sv01: Row[] = [
  459 |     { v: 0, err: MSG.INVALID_QTY, code: 'INVALID_QTY' },
  460 |     { v: 1, fee: 20 },
  461 |     { v: 2, fee: 40 },
  462 |     { v: 3, fee: 60 },
  463 |     { v: 4, fee: 80 },
  464 |     { v: 5, fee: 100 },
  465 |     { v: 6, err: MSG.INVALID_QTY, code: 'INVALID_QTY' },
  466 |   ];
  467 |   await p.goto('/citizen/new/SV-01');
  468 |   for (const r of sv01) {
  469 |     await test.step(`SV-01 จำนวน ${r.v}`, async () => {
  470 |       await check('qty-input', r);
  471 |       await checkApi({ serviceId: 'SV-01', qty: r.v }, r);
  472 |     });
  473 |   }
  474 | 
  475 |   await test.step('SV-02 ไม่มีช่องกรอก ฿500', async () => {
  476 |     await p.goto('/citizen/new/SV-02');
  477 |     await expect(tid(p, 'fee-total')).toHaveText('฿500');
  478 |     await expect(tid(p, 'qty-input')).toHaveCount(0);
  479 |     await expect(tid(p, 'area-input')).toHaveCount(0);
  480 |     const b = await expectApi(api.post('/api/drafts', { data: { serviceId: 'SV-02' } }), 201);
  481 |     expect(b.fee).toBe(500);
  482 |   });
  483 | });
  484 | 
  485 | // ═══════════════════════════════════ SUBMIT ═══════════════════════════════════
  486 | 
  487 | test('TC-SUBMIT-01 ยื่นคำขอ SV-01 ครบวงจร', async ({ browser }) => {
  488 |   await reset();
  489 |   const { page: p } = await citizenSession(browser, ID.SOMCHAI);
  490 |   const NO = caseNo(31);
  491 | 
  492 |   await test.step('1 กรอกข้อมูล', async () => {
  493 |     await p.goto('/citizen');
  494 |     await tid(p, 'start-service-SV-01').click();
  495 |     await waitPath(p, '/citizen/new/SV-01');
  496 |     await expect(tid(p, 'wizard-step')).toHaveText('1/3 กรอกข้อมูล');
  497 |     await fillField(tid(p, 'qty-input'), '2');
  498 |     await expect(tid(p, 'fee-total')).toHaveText('฿40');
  499 |     await tid(p, 'to-upload-btn').click();
  500 |   });
  501 | 
  502 |   await test.step('2 แนบเอกสาร', async () => {
  503 |     await expect(tid(p, 'wizard-step')).toHaveText('2/3 แนบเอกสาร');
  504 |     await expect(tid(p, 'to-payment-btn')).toBeDisabled();
  505 |     await uiUpload(p, 'id-card', 'id-card.pdf');
  506 |     await expect(tid(p, 'file-item')).toHaveCount(1);
  507 |     await expect(tid(p, 'file-item')).toHaveAttribute('data-doc-key', 'id-card');
  508 |     await expect(tid(p, 'to-payment-btn')).toBeEnabled();
  509 |     await tid(p, 'to-payment-btn').click();
  510 |   });
  511 | 
  512 |   await test.step('3 ชำระเงิน สร้าง QR', async () => {
  513 |     await expect(tid(p, 'wizard-step')).toHaveText('3/3 ชำระเงิน');
  514 |     await expect(tid(p, 'payment-amount')).toHaveText('฿40');
  515 |     await tid(p, 'create-qr-btn').click();
  516 |     await expect(tid(p, 'qr-ref')).toHaveText('PP-0002');
```