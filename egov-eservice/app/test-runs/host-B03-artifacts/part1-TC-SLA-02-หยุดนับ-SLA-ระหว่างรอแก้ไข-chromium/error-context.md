# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-SLA-02 หยุดนับ SLA ระหว่างรอแก้ไข
- Location: tests\part1.spec.ts:1257:1

# Error details

```
Error: expect(locator).toHaveAttribute(expected) failed

Locator:  getByTestId('sla-due')
Expected: "2026-12-08T16:30:00+07:00"
Received: "2026-12-07T16:30:00+07:00"
Timeout:  7000ms

Call log:
  - Expect "toHaveAttribute" getByTestId('sla-due') with timeout 7000ms
  - waiting for getByTestId('sla-due')
    17 × locator resolved to <time data-testid="sla-due" data-iso="2026-12-07T16:30:00+07:00" datetime="2026-12-07T16:30:00+07:00">7 ธ.ค. 2569 16:30</time>
       - unexpected value "2026-12-07T16:30:00+07:00"

```

```yaml
- time: 7 ธ.ค. 2569 16:30
```

# Test source

```ts
  1   | /**
  2   |  * part1.spec.ts · TEST-PLAN ชุด 1 (22 TC): AUTH FEE SUBMIT UPLOAD PAY QUEUE SLA NOTI
  3   |  *
  4   |  * - ทุก TC เริ่มด้วย reset() (POST /api/test/reset) แล้วล็อกอินใหม่ใน context ใหม่ทุกครั้งหลัง reset
  5   |  * - ค่าคาดหวังทุกตัวคัดจาก TEST-PLAN / TEST-DATA / CONTRACT (คิดจากกฎ ไม่ได้อ่านจากหน้าจอ)
  6   |  * - ส่วนที่เป็นสิทธิ์/บั๊ก (เช่น B08 รับเรื่องซ้อน) ยิง API ตรงเสมอ ไม่ตรวจแค่ปุ่มหาย
  7   |  */
  8   | import { test, expect, type Browser, type Page, type APIRequestContext } from '@playwright/test';
  9   | import {
  10  |   ID,
  11  |   MSG,
  12  |   STAFF,
  13  |   T0,
  14  |   OTP_BAD,
  15  |   OTP_OK,
  16  |   STATUS_TH,
  17  |   LEVEL_TH,
  18  |   type SlaLevel,
  19  |   type StaffUser,
  20  |   type PendingDraft,
  21  |   caseNo,
  22  |   receiptNo,
  23  |   ppRef,
  24  |   reset,
  25  |   setClock,
  26  |   cleanup,
  27  |   newApi,
  28  |   expectApi,
  29  |   bodyOf,
  30  |   pay,
  31  |   payRaw,
  32  |   loginCitizen,
  33  |   loginStaff,
  34  |   logout,
  35  |   newSession,
  36  |   citizenSession,
  37  |   staffSession,
  38  |   uiThaidStart,
  39  |   uiSubmitOtp,
  40  |   uiLoginCitizen,
  41  |   uiStaffSubmit,
  42  |   uiLogout,
  43  |   waitPath,
  44  |   createDraft,
  45  |   upload,
  46  |   uploadRaw,
  47  |   createQr,
  48  |   filePayload,
  49  |   newPending,
  50  |   newPaid,
  51  |   getCase,
  52  |   myCases,
  53  |   myDrafts,
  54  |   getPayment,
  55  |   claim,
  56  |   claimRaw,
  57  |   returnCase,
  58  |   resubmit,
  59  |   cancelRaw,
  60  |   queueItems,
  61  |   notificationKeys,
  62  |   auditItems,
  63  |   rowBy,
  64  |   queueRow,
  65  |   fileItem,
  66  |   attrs,
  67  |   texts,
  68  |   withMutation,
  69  |   fillField,
  70  |   uiWizardToUpload,
  71  |   uiUpload,
  72  |   uiRemoveFile,
  73  |   uiQueueFilter,
  74  | } from '../helpers';
  75  | 
  76  | test.afterEach(async () => {
  77  |   await cleanup();
  78  | });
  79  | 
  80  | /** ฿ + คั่นหลักพัน (CONTRACT 0.2) */
  81  | const baht = (n: number): string => `฿${n.toLocaleString('en-US')}`;
  82  | const tid = (p: Page, id: string) => p.getByTestId(id);
  83  | 
  84  | /** ตรวจ sla-due (ข้อความ + data-iso) */
  85  | async function expectDue(p: Page, text: string | null, iso: string): Promise<void> {
  86  |   const due = tid(p, 'sla-due');
> 87  |   await expect(due).toHaveAttribute('data-iso', iso);
      |                     ^ Error: expect(locator).toHaveAttribute(expected) failed
  88  |   if (text) await expect(due).toHaveText(text);
  89  | }
  90  | 
  91  | /** ตรวจ sla-level (ข้อความไทย + data-level) */
  92  | async function expectLevel(p: Page, level: SlaLevel): Promise<void> {
  93  |   const el = tid(p, 'sla-level');
  94  |   await expect(el).toHaveText(LEVEL_TH[level]);
  95  |   await expect(el).toHaveAttribute('data-level', level);
  96  | }
  97  | 
  98  | /** ตรวจ case-status (ข้อความไทย + data-status) */
  99  | async function expectStatus(p: Page, status: keyof typeof STATUS_TH): Promise<void> {
  100 |   const el = tid(p, 'case-status');
  101 |   await expect(el).toHaveText(STATUS_TH[status]);
  102 |   await expect(el).toHaveAttribute('data-status', status);
  103 | }
  104 | 
  105 | /** ลำดับ data-case-no ของแถวคิวบนจอ */
  106 | async function queueOrder(p: Page): Promise<string[]> {
  107 |   return (await attrs(tid(p, 'queue-row'), 'data-case-no')) as string[];
  108 | }
  109 | 
  110 | /** แถวคิวที่มี claim-btn */
  111 | async function claimableRows(p: Page): Promise<string[]> {
  112 |   return tid(p, 'queue-row').evaluateAll((els) =>
  113 |     els.filter((e) => e.querySelector('[data-testid="claim-btn"]')).map((e) => e.getAttribute('data-case-no') ?? ''),
  114 |   );
  115 | }
  116 | 
  117 | /** ชุดแจ้งเตือนบนหน้า /notifications: ['EG-…:near', …] เรียงแล้ว */
  118 | async function uiNotiKeys(p: Page): Promise<string[]> {
  119 |   return tid(p, 'noti-item').evaluateAll((els) =>
  120 |     els.map((e) => `${e.getAttribute('data-case-no')}:${e.getAttribute('data-level')}`).sort(),
  121 |   );
  122 | }
  123 | 
  124 | const keys = (pairs: Array<[number, 'near' | 'overdue']>): string[] => pairs.map(([n, l]) => `${caseNo(n)}:${l}`).sort();
  125 | 
  126 | /** กรองชุดแจ้งเตือนเฉพาะคำขอเดียว */
  127 | const only = (all: string[], n: number): string[] => all.filter((k) => k.startsWith(`${caseNo(n)}:`));
  128 | 
  129 | /** อ่าน workload-count บน /officer/queue */
  130 | async function expectWorkload(p: Page, n: number): Promise<void> {
  131 |   await p.goto('/officer/queue');
  132 |   await expect(tid(p, 'workload-count')).toHaveText(String(n));
  133 | }
  134 | 
  135 | // ═══════════════════════════════════ AUTH ═══════════════════════════════════
  136 | 
  137 | test('TC-AUTH-01 เลขบัตร 13 หลัก + checksum', async ({ browser }) => {
  138 |   await reset();
  139 |   const { page: p } = await newSession(browser);
  140 |   const api = await newApi();
  141 | 
  142 |   const invalid = ['110170012345', '11017001234567', ID.BAD_CHECKSUM, '11017001234ab'];
  143 |   for (const v of invalid) {
  144 |     await test.step(`ปฏิเสธ ${v}`, async () => {
  145 |       await p.goto('/login');
  146 |       await tid(p, 'login-tab-citizen').click();
  147 |       await tid(p, 'thaid-id-input').fill(v);
  148 |       await expect(tid(p, 'thaid-id-input')).toHaveValue(v); // ไม่จำกัด maxlength (A-45)
  149 |       await tid(p, 'thaid-submit').click();
  150 |       await expect(tid(p, 'thaid-error')).toHaveText(MSG.INVALID_ID);
  151 |       await expect(tid(p, 'otp-step')).toBeHidden();
  152 |       await expectApi(api.post('/api/auth/thaid/start', { data: { idNo: v } }), 400, 'INVALID_ID');
  153 |     });
  154 |   }
  155 | 
  156 |   const valid = [ID.SOMCHAI, ID.SOMYING, ID.PITI, ID.MANA];
  157 |   for (const v of valid) {
  158 |     await test.step(`รับ ${v}`, async () => {
  159 |       await p.goto('/login');
  160 |       await tid(p, 'login-tab-citizen').click();
  161 |       await tid(p, 'thaid-id-input').fill(v);
  162 |       await expect(tid(p, 'thaid-submit')).toHaveText('เข้าสู่ระบบด้วย ThaiD (จำลอง)');
  163 |       await tid(p, 'thaid-submit').click();
  164 |       await expect(tid(p, 'otp-step')).toBeVisible();
  165 |       await expect(tid(p, 'thaid-error')).toBeHidden();
  166 |       const body = await expectApi(api.post('/api/auth/thaid/start', { data: { idNo: v } }), 200);
  167 |       expect(body).toMatchObject({ status: 'OTP_SENT' });
  168 |     });
  169 |   }
  170 | });
  171 | 
  172 | test('TC-AUTH-02 OTP ผิด 3 ครั้งล็อก 15 นาที', async ({ browser }) => {
  173 |   test.setTimeout(300_000);
  174 |   const LOCK_UNTIL = '2026-12-01T09:15:00+07:00';
  175 | 
  176 |   /** กรอก OTP บนหน้า: ถ้าช่อง OTP ไม่แสดง (เช่น หลังล็อก) ให้เริ่มใหม่ด้วยเลขบัตร */
  177 |   async function uiTryOtp(p: Page, idNo: string, otp: string): Promise<void> {
  178 |     if (!(await tid(p, 'otp-input').isVisible())) {
  179 |       await uiThaidStart(p, idNo);
  180 |       await expect(tid(p, 'otp-step').or(tid(p, 'lock-message')).first()).toBeVisible();
  181 |     }
  182 |     const input = tid(p, 'otp-input');
  183 |     if ((await input.isVisible()) && (await input.isEnabled())) await uiSubmitOtp(p, otp);
  184 |   }
  185 | 
  186 |   await test.step('หน้าจอ: ขั้น 1–8', async () => {
  187 |     await reset();
```