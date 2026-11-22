# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-DASH-02 Dashboard ย้อนหลัง พ.ย. ต.ค. รายปี
- Location: tests/part2.spec.ts:954:1

# Error details

```
Error: 2026-11 ALL ontimePct

expect(received).toBe(expected) // Object.is equality

Expected: 85.7
Received: 23.1
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
            - link "Dashboard" [ref=e9] [cursor=pointer]:
              - /url: /dashboard
      - generic [ref=e10]:
        - generic [ref=e11]:
          - text: ผู้บริหาร
          - generic [ref=e12]: ผู้บริหาร
        - button "ออกจากระบบ" [ref=e14] [cursor=pointer]
  - main [ref=e15]:
    - heading "Dashboard ผู้บริหาร" [level=1] [ref=e16]
    - paragraph [ref=e17]:
      - text: ข้อมูล ณ
      - time [ref=e18]: 1 ธ.ค. 2569 09:00
      - text: · ไม่แสดงข้อมูลส่วนบุคคลของผู้ยื่น
    - search "ตัวกรอง Dashboard" [ref=e19]:
      - generic [ref=e20]:
        - generic [ref=e21]: ช่วงเวลา
        - combobox "ช่วงเวลา" [ref=e22]:
          - option "ธ.ค. 2569"
          - option "พ.ย. 2569"
          - option "ต.ค. 2569" [selected]
          - option "ก.ย. 2569"
          - option "ส.ค. 2569"
          - option "ก.ค. 2569"
          - option "มิ.ย. 2569"
          - option "พ.ค. 2569"
          - option "เม.ย. 2569"
          - option "มี.ค. 2569"
          - option "ก.พ. 2569"
          - option "ม.ค. 2569"
          - option "ทั้งปี 2569"
          - option "ทั้งปี 2568"
      - generic [ref=e23]:
        - generic [ref=e24]: บริการ
        - combobox "บริการ" [ref=e25]:
          - option "ทุกบริการ" [selected]
          - option "SV-01 ขอหนังสือรับรอง"
          - option "SV-02 ขออนุญาตประกอบกิจการ"
          - option "SV-03 ขออนุญาตก่อสร้าง/ต่อเติมอาคาร"
      - generic [ref=e26]:
        - button "แสดงผล" [ref=e27] [cursor=pointer]
        - link "ส่งออก Excel" [ref=e28] [cursor=pointer]:
          - /url: /api/dashboard/export?format=xlsx&period=2026-10&service=ALL
        - link "ส่งออก PDF" [ref=e29] [cursor=pointer]:
          - /url: /api/dashboard/export?format=pdf&period=2026-10&service=ALL
    - region "ตัวชี้วัด" [ref=e30]:
      - heading "ตัวชี้วัด" [level=2] [ref=e31]
      - generic [ref=e32]:
        - generic [ref=e33]:
          - generic [ref=e34]: รับเรื่อง
          - generic [ref=e35]: "1"
        - generic [ref=e36]:
          - generic [ref=e37]: ปิดงาน
          - generic [ref=e38]: "1"
        - generic [ref=e39]:
          - generic [ref=e40]: ทันกำหนด %
          - generic [ref=e41]: 100.0%
          - generic [ref=e42]: ทันกำหนด 1 งาน
        - generic [ref=e43]:
          - generic [ref=e44]: งานคงค้าง (ณ ตอนนี้)
          - generic [ref=e45]: "21"
        - generic [ref=e46]:
          - generic [ref=e47]: เกินกำหนดคงค้าง (ณ ตอนนี้)
          - generic [ref=e48]: "1"
    - region "งานในมือรายเจ้าหน้าที่" [ref=e49]:
      - heading "งานในมือรายเจ้าหน้าที่" [level=2] [ref=e50]
      - table "จำนวนคำขอที่กำลังตรวจสอบซึ่งเจ้าหน้าที่แต่ละคนรับไว้ (ไม่ขึ้นกับตัวกรอง)" [ref=e52]:
        - caption [ref=e53]: จำนวนคำขอที่กำลังตรวจสอบซึ่งเจ้าหน้าที่แต่ละคนรับไว้ (ไม่ขึ้นกับตัวกรอง)
        - rowgroup [ref=e54]:
          - row [ref=e55]:
            - columnheader "เจ้าหน้าที่" [ref=e56]
            - columnheader "งานในมือ" [ref=e57]
        - rowgroup [ref=e58]:
          - row [ref=e59]:
            - cell "เจ้าหน้าที่ทะเบียน 1 (off.reg1)" [ref=e60]
            - cell "3" [ref=e61]
          - row [ref=e62]:
            - cell "เจ้าหน้าที่ทะเบียน 2 (off.reg2)" [ref=e63]
            - cell "9" [ref=e64]
          - row [ref=e65]:
            - cell "เจ้าหน้าที่โยธา 1 (off.works1)" [ref=e66]
            - cell "0" [ref=e67]
  - contentinfo [ref=e68]:
    - paragraph [ref=e69]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  90  |   deepKeys,
  91  |   piiHits,
  92  |   overflowX,
  93  |   axeSerious,
  94  |   unlabeledControls,
  95  |   focusInfo,
  96  |   tabTo,
  97  |   statusTextProblems,
  98  |   countInFile,
  99  |   type Kpis,
  100 |   type AuditRowUi,
  101 | } from '../helpers2';
  102 | 
  103 | test.afterEach(async () => {
  104 |   await cleanup2();
  105 |   await cleanup();
  106 | });
  107 | 
  108 | // ───────────────────────── ค่าคงที่และตัวช่วยเฉพาะไฟล์นี้ ─────────────────────────
  109 | 
  110 | const CODE_RE = /^[A-Z0-9]{8}$/;
  111 | const MASK_RE = /^X-XXXX-XXXXX-\d{2}-\d$/;
  112 | const ORIGIN = BASE_URL.replace(/\/+$/, '');
  113 | const R10 = 'xxxxxxxxxx'; // เหตุผล 10 ตัว (A-44)
  114 | const R9 = 'xxxxxxxxx'; // 9 ตัว
  115 | const SPACES10 = ' '.repeat(10);
  116 | 
  117 | const VERIFY_TH = { VALID: 'เอกสารถูกต้อง', EXPIRED: 'เอกสารหมดอายุ', TAMPERED: 'ลายเซ็นไม่ถูกต้อง', NOT_FOUND: 'ไม่พบเอกสาร' } as const;
  118 | type VerifyResult = keyof typeof VERIFY_TH;
  119 | 
  120 | /** เปิด /officer/cases/:no (officer/head) */
  121 | async function openOfficer(p: Page, no: string): Promise<void> {
  122 |   await p.goto(`/officer/cases/${no}`);
  123 |   await expect(tid(p, 'case-no')).toHaveText(no);
  124 | }
  125 | 
  126 | /** เปิด /citizen/cases/:no (ประชาชนเจ้าของ) */
  127 | async function openCitizen(p: Page, no: string): Promise<void> {
  128 |   await p.goto(`/citizen/cases/${no}`);
  129 |   await expect(tid(p, 'case-no')).toHaveText(no);
  130 | }
  131 | 
  132 | async function apiApprove(api: APIRequestContext, no: string): Promise<void> {
  133 |   const b = await expectApi(approveRaw(api, no), 200);
  134 |   expect(b.status).toBe('APPROVED');
  135 | }
  136 | 
  137 | async function apiIssue(api: APIRequestContext, no: string, docNo?: string): Promise<{ docNo: string; verifyCode: string }> {
  138 |   const b = await expectApi(issueRaw(api, no), 200);
  139 |   expect(b.status).toBe('COMPLETED');
  140 |   expect(b.verifyCode).toMatch(CODE_RE);
  141 |   if (docNo) expect(b.docNo).toBe(docNo);
  142 |   return b;
  143 | }
  144 | 
  145 | async function apiReject(api: APIRequestContext, no: string, reason = R10): Promise<void> {
  146 |   const b = await expectApi(rejectRaw(api, no, reason), 200);
  147 |   expect(b.status).toBe('REJECTED');
  148 | }
  149 | 
  150 | /** เปิด /verify/:code แล้วตรวจ HTTP + verify-result (ข้อความ + data-result) */
  151 | async function expectVerify(p: Page, code: string, result: VerifyResult): Promise<void> {
  152 |   const res = await p.goto(`/verify/${code}`);
  153 |   expect(res?.status(), `/verify/${code}`).toBe(result === 'NOT_FOUND' ? 404 : 200);
  154 |   expect(pathOf(p)).toBe(`/verify/${code}`);
  155 |   const el = tid(p, 'verify-result');
  156 |   await expect(el).toHaveText(VERIFY_TH[result]);
  157 |   await expect(el).toHaveAttribute('data-result', result);
  158 | }
  159 | 
  160 | /** ตั้งนาฬิกาแล้วเปิด /verify/:code */
  161 | async function verifyAt(p: Page, code: string, clock: string, result: VerifyResult, expires?: string): Promise<void> {
  162 |   await setClock(clock);
  163 |   await expectVerify(p, code, result);
  164 |   if (expires) await expect(tid(p, 'verify-expires')).toHaveAttribute('data-iso', expires);
  165 | }
  166 | 
  167 | /** verify-code บนหน้าเคส (8 ตัว) */
  168 | async function verifyCodeOnPage(p: Page): Promise<string> {
  169 |   await expect(tid(p, 'verify-code')).toHaveText(CODE_RE);
  170 |   return (await tid(p, 'verify-code').innerText()).trim();
  171 | }
  172 | 
  173 | /** เปิด /verify/<code> แบบไม่ล็อกอินแล้วตรวจผู้ลงนาม */
  174 | async function expectSigner(browser: import('@playwright/test').Browser, code: string, signer: string): Promise<void> {
  175 |   const { page } = await newSession(browser);
  176 |   await expectVerify(page, code, 'VALID');
  177 |   await expect(tid(page, 'verify-signer')).toHaveText(signer);
  178 | }
  179 | 
  180 | /** ลำดับ data-case-no ของแถว */
  181 | async function caseOrder(p: Page, testid: string): Promise<string[]> {
  182 |   return (await attrs(tid(p, testid), 'data-case-no')) as string[];
  183 | }
  184 | 
  185 | /** ตรวจผล API ของ Dashboard (เฉพาะช่องที่ส่งมา) */
  186 | function expectDash(d: any, k: Partial<Kpis> & { onTime?: number }, label = ''): void {
  187 |   if (k.received !== undefined) expect(d.received, `${label} received`).toBe(k.received);
  188 |   if (k.closed !== undefined) expect(d.closed, `${label} closed`).toBe(k.closed);
  189 |   if (k.onTime !== undefined) expect(d.onTime, `${label} onTime`).toBe(k.onTime);
> 190 |   if (k.pct !== undefined) expect(d.ontimePct, `${label} ontimePct`).toBe(pctValue(k.pct));
      |                                                                      ^ Error: 2026-11 ALL ontimePct
  191 |   if (k.backlog !== undefined) expect(d.backlog, `${label} backlog`).toBe(k.backlog);
  192 |   if (k.overdue !== undefined) expect(d.overdue, `${label} overdue`).toBe(k.overdue);
  193 | }
  194 | 
  195 | /** งานคงค้าง/เกินกำหนด "ณ ตอนนี้" ตามบริการ (TEST-DATA 7.2 · A-41) */
  196 | const NOW_BY_SERVICE: Record<string, { backlog: number; overdue: number }> = {
  197 |   ALL: { backlog: 21, overdue: 1 },
  198 |   'SV-01': { backlog: 11, overdue: 1 },
  199 |   'SV-02': { backlog: 7, overdue: 0 },
  200 |   'SV-03': { backlog: 3, overdue: 0 },
  201 | };
  202 | 
  203 | // ═══════════════════════════════════ WORKFLOW ═══════════════════════════════════
  204 | 
  205 | test('TC-WORKFLOW-01 SV-01 อนุมัติ + ออกเอกสาร', async ({ browser }) => {
  206 |   await reset();
  207 |   const NO = caseNo(25);
  208 |   const { page: p } = await staffSession(browser, 'off.reg2');
  209 | 
  210 |   await test.step('1 ปุ่มของผู้ถือเรื่อง SV-01', async () => {
  211 |     await openOfficer(p, NO);
  212 |     await expectStatus(p, 'IN_REVIEW');
  213 |     await expect(tid(p, 'approve-btn')).toHaveCount(1);
  214 |     await expect(tid(p, 'return-btn')).toHaveCount(1);
  215 |     await expect(tid(p, 'reject-btn')).toHaveCount(1);
  216 |     await expect(tid(p, 'forward-btn')).toHaveCount(0);
  217 |     await expect(tid(p, 'issue-btn')).toHaveCount(0);
  218 |     await expect(tid(p, 'case-fee')).toHaveText('฿60');
  219 |   });
  220 | 
  221 |   await test.step('2 off.reg1 อนุมัติ …000026 ที่ off.reg2 ถือ → 403', async () => {
  222 |     const reg1 = await loginStaff('off.reg1');
  223 |     await expectApi(approveRaw(reg1, caseNo(26)), 403, 'FORBIDDEN');
  224 |     expect((await getCase(reg1, caseNo(26))).status).toBe('IN_REVIEW');
  225 |   });
  226 | 
  227 |   await test.step('3 อนุมัติ', async () => {
  228 |     await act(p, () => tid(p, 'approve-btn').click());
  229 |     await expectStatus(p, 'APPROVED');
  230 |     await expect(tid(p, 'issue-btn')).toHaveCount(1);
  231 |     await expect(tid(p, 'approve-btn')).toHaveCount(0);
  232 |   });
  233 | 
  234 |   await test.step('4 ออกเอกสาร', async () => {
  235 |     await act(p, () => tid(p, 'issue-btn').click());
  236 |     await expectStatus(p, 'COMPLETED');
  237 |     await expect(tid(p, 'doc-no')).toHaveText('DOC-2569-000002');
  238 |     await verifyCodeOnPage(p);
  239 |     await expect(tid(p, 'closed-at')).toHaveAttribute('data-iso', T0);
  240 |     await expectLevel(p, 'closed');
  241 |   });
  242 | 
  243 |   await test.step('5 สมหญิงดาวน์โหลดเอกสาร PDF', async () => {
  244 |     const { page: c, api } = await citizenSession(browser, ID.SOMYING);
  245 |     await openCitizen(c, NO);
  246 |     await expectStatus(c, 'COMPLETED');
  247 |     await expect(tid(c, 'download-doc-btn')).toHaveCount(1);
  248 |     const f = await grabDownload(c, () => tid(c, 'download-doc-btn').click(), /pdf/i);
  249 |     expect(f.status).toBe(200);
  250 |     expect(f.contentType).toContain('application/pdf');
  251 |     expect(f.filename).toBe('DOC-2569-000002.pdf');
  252 |     expect(f.body.subarray(0, 4).toString('latin1')).toBe('%PDF');
  253 |     expect(pdfHasLine(pdfText(f.body), `docNo=DOC-2569-000002 caseNo=${NO}`), 'บรรทัด ASCII docNo/caseNo ใน PDF').toBe(true);
  254 | 
  255 |     const r = await api.get('/api/documents/DOC-2569-000002/pdf');
  256 |     expect(r.status()).toBe(200);
  257 |     expect(r.headers()['content-type']).toContain('application/pdf');
  258 |     expect(r.headers()['content-disposition'] ?? '').toContain('DOC-2569-000002.pdf');
  259 |   });
  260 | 
  261 |   await test.step('6 Dashboard ธ.ค. ALL', async () => {
  262 |     const ex = await loginStaff('exec1');
  263 |     expectDash(await getDashboard(ex, '2026-12'), { closed: 1, onTime: 1, received: 3, backlog: 20 });
  264 |   });
  265 | });
  266 | 
  267 | test('TC-WORKFLOW-02 SV-02 ผ่านหัวหน้า', async ({ browser }) => {
  268 |   const NO = caseNo(13);
  269 |   await reset();
  270 |   const reg2 = await staffSession(browser, 'off.reg2');
  271 |   const p = reg2.page;
  272 | 
  273 |   await test.step('1 ปุ่มของเจ้าหน้าที่ SV-02', async () => {
  274 |     await openOfficer(p, NO);
  275 |     await expect(tid(p, 'approve-btn')).toHaveCount(0);
  276 |     await expect(tid(p, 'forward-btn')).toHaveCount(1);
  277 |     await expect(tid(p, 'forward-target')).toHaveCount(0);
  278 |   });
  279 | 
  280 |   await test.step('2 ส่งต่อหัวหน้า', async () => {
  281 |     await uiForward(p);
  282 |     await expectStatus(p, 'PENDING_APPROVAL');
  283 |     await p.goto('/officer/queue');
  284 |     await expect(tid(p, 'workload-count')).toHaveText('8');
  285 |     await expect(queueRow(p, NO)).toHaveCount(0);
  286 |   });
  287 | 
  288 |   const head = await staffSession(browser, 'head1');
  289 |   const h = head.page;
  290 |   await test.step('3 /head/approvals 3 แถวเรียงตาม BR-16', async () => {
```