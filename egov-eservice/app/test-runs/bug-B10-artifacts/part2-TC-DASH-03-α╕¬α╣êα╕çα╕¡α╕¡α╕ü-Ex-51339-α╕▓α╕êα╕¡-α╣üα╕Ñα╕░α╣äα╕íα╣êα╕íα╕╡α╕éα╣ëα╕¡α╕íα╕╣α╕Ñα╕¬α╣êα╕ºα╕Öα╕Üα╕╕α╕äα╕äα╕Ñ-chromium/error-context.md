# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-DASH-03 ส่งออก Excel/PDF เท่าหน้าจอ และไม่มีข้อมูลส่วนบุคคล
- Location: tests/part2.spec.ts:981:1

# Error details

```
Error: expect(locator).toHaveText(expected) failed

Locator:  getByTestId('kpi-ontime-pct')
Expected: "85.7%"
Received: "23.1%"
Timeout:  7000ms

Call log:
  - Expect "toHaveText" getByTestId('kpi-ontime-pct') with timeout 7000ms
  - waiting for getByTestId('kpi-ontime-pct')
    18 × locator resolved to <div class="value" data-testid="kpi-ontime-pct">23.1%</div>
       - unexpected value "23.1%"

```

```yaml
- text: 23.1%
```

# Test source

```ts
  79  |   page.on('dialog', (d) => d.accept().catch(() => {}));
  80  |   return { context, page, api: context.request };
  81  | }
  82  | 
  83  | // ───────────────────────── ทำรายการบนหน้าจอ ─────────────────────────
  84  | 
  85  | /** รอให้หน้า navigate (ถ้ามี) ภายในเวลาสั้น ๆ แล้วรอโหลดเสร็จ */
  86  | export async function settle(p: Page, action: () => Promise<unknown>, navTimeout = 1_500): Promise<void> {
  87  |   const nav = p.waitForEvent('framenavigated', { predicate: (f) => f === p.mainFrame(), timeout: navTimeout }).catch(() => null);
  88  |   await action();
  89  |   await nav;
  90  |   await p.waitForLoadState('load').catch(() => {});
  91  |   await p.waitForLoadState('networkidle', { timeout: 5_000 }).catch(() => {});
  92  | }
  93  | 
  94  | /**
  95  |  * ทำรายการที่ส่งข้อมูลขึ้นเซิร์ฟเวอร์ (รอ response แรกที่ไม่ใช่ GET)
  96  |  * - ถ้าหน้า navigate เอง (form POST → redirect / location.reload) รอหน้าใหม่โหลด
  97  |  * - ถ้าไม่ navigate และ reload = true → reload ให้ได้สถานะล่าสุดจากเซิร์ฟเวอร์
  98  |  * - ใช้ reload = false เมื่อจะตรวจข้อความ error / toast / full-id ที่แสดงเฉพาะหน้านั้น
  99  |  */
  100 | export async function act(p: Page, action: () => Promise<unknown>, opts: { reload?: boolean } = {}): Promise<void> {
  101 |   const reload = opts.reload ?? true;
  102 |   let navigated = false;
  103 |   const onNav = (f: Frame) => {
  104 |     if (f === p.mainFrame()) navigated = true;
  105 |   };
  106 |   p.on('framenavigated', onNav);
  107 |   try {
  108 |     await withMutation(p, action);
  109 |     if (!navigated) {
  110 |       await p
  111 |         .waitForEvent('framenavigated', { predicate: (f) => f === p.mainFrame(), timeout: 1_500 })
  112 |         .then(() => (navigated = true))
  113 |         .catch(() => {});
  114 |     }
  115 |     await p.waitForLoadState('load').catch(() => {});
  116 |     if (!navigated && reload) await p.reload();
  117 |   } finally {
  118 |     p.off('framenavigated', onNav);
  119 |   }
  120 | }
  121 | 
  122 | /** เปิดฟอร์มเหตุผล (กดปุ่มเปิดถ้าช่องยังไม่แสดง) กรอก แล้วกดยืนยัน */
  123 | async function reasonForm(p: Page, openBtn: string, input: string, submit: string, reason: string, reload: boolean): Promise<void> {
  124 |   const box = tid(p, input);
  125 |   if (!(await box.isVisible())) await tid(p, openBtn).click();
  126 |   await expect(box).toBeVisible();
  127 |   await box.fill(reason);
  128 |   await act(p, () => tid(p, submit).click(), { reload });
  129 | }
  130 | 
  131 | /** return-btn → return-reason → return-submit */
  132 | export const uiReturn = (p: Page, reason: string, reload = true) => reasonForm(p, 'return-btn', 'return-reason', 'return-submit', reason, reload);
  133 | /** reject-btn → reject-reason → reject-submit */
  134 | export const uiReject = (p: Page, reason: string, reload = true) => reasonForm(p, 'reject-btn', 'reject-reason', 'reject-submit', reason, reload);
  135 | /** show-full-id-btn → unmask-reason → unmask-submit (ไม่ reload: เลขเต็มเห็นเฉพาะในหน้านั้น) */
  136 | export const uiUnmask = (p: Page, reason: string) => reasonForm(p, 'show-full-id-btn', 'unmask-reason', 'unmask-submit', reason, false);
  137 | 
  138 | /** กรอก forward-note (ถ้ามี) แล้วกด forward-btn */
  139 | export async function uiForward(p: Page, note?: string): Promise<void> {
  140 |   if (note !== undefined) await tid(p, 'forward-note').fill(note);
  141 |   await act(p, () => tid(p, 'forward-btn').click());
  142 | }
  143 | 
  144 | /** เลือกค่าใน select แล้วรอหน้าอัปเดต (รองรับทั้ง onchange submit และ fetch) */
  145 | export async function uiSelect(p: Page, testid: string, value: string): Promise<void> {
  146 |   const sel = tid(p, testid);
  147 |   if ((await sel.inputValue()) === value) return;
  148 |   await settle(p, () => sel.selectOption(value));
  149 |   await expect(tid(p, testid)).toHaveValue(value);
  150 | }
  151 | 
  152 | // ───────────────────────── Dashboard ─────────────────────────
  153 | 
  154 | export interface Kpis {
  155 |   received: number;
  156 |   closed: number;
  157 |   /** ข้อความ kpi-ontime-pct เช่น '85.7%' หรือ '–' */
  158 |   pct: string;
  159 |   backlog: number;
  160 |   overdue: number;
  161 | }
  162 | 
  163 | /** GET /api/dashboard?period=…&service=… (executive) */
  164 | export async function getDashboard(api: APIRequestContext, period: string, service = 'ALL'): Promise<any> {
  165 |   return expectApi(api.get(`/api/dashboard?period=${period}&service=${service}`), 200);
  166 | }
  167 | 
  168 | /** /dashboard เลือก period-select + service-select */
  169 | export async function uiDashboard(p: Page, period: string, service = 'ALL'): Promise<void> {
  170 |   if (pathOf(p) !== '/dashboard') await p.goto('/dashboard');
  171 |   await uiSelect(p, 'period-select', period);
  172 |   await uiSelect(p, 'service-select', service);
  173 | }
  174 | 
  175 | /** ตรวจ kpi-* บนจอ (เฉพาะช่องที่ส่งมา) */
  176 | export async function expectKpis(p: Page, k: Partial<Kpis>): Promise<void> {
  177 |   if (k.received !== undefined) await expect(tid(p, 'kpi-received')).toHaveText(String(k.received));
  178 |   if (k.closed !== undefined) await expect(tid(p, 'kpi-closed')).toHaveText(String(k.closed));
> 179 |   if (k.pct !== undefined) await expect(tid(p, 'kpi-ontime-pct')).toHaveText(k.pct);
      |                                                                   ^ Error: expect(locator).toHaveText(expected) failed
  180 |   if (k.backlog !== undefined) await expect(tid(p, 'kpi-backlog')).toHaveText(String(k.backlog));
  181 |   if (k.overdue !== undefined) await expect(tid(p, 'kpi-overdue')).toHaveText(String(k.overdue));
  182 | }
  183 | 
  184 | /** ค่าที่ API ต้องได้จากข้อความทันกำหนด % ('85.7%' → 85.7 · '–' → null) */
  185 | export const pctValue = (pct: string): number | null => (pct === '–' ? null : Number(pct.replace('%', '')));
  186 | 
  187 | // ───────────────────────── Audit ─────────────────────────
  188 | 
  189 | export interface AuditFilter {
  190 |   actor?: string;
  191 |   event?: string;
  192 |   from?: string;
  193 |   to?: string;
  194 | }
  195 | 
  196 | /** เปิด /audit ใหม่ กรอกตัวกรองทุกช่อง (ว่าง = ไม่กรอง) แล้วกด audit-apply-btn */
  197 | export async function uiAudit(p: Page, f: AuditFilter = {}): Promise<void> {
  198 |   await p.goto('/audit');
  199 |   await tid(p, 'audit-filter-actor').fill(f.actor ?? '');
  200 |   await tid(p, 'audit-filter-event').selectOption(f.event ?? '');
  201 |   await tid(p, 'audit-filter-from').fill(f.from ?? '');
  202 |   await tid(p, 'audit-filter-to').fill(f.to ?? '');
  203 |   await settle(p, () => tid(p, 'audit-apply-btn').click());
  204 | }
  205 | 
  206 | export interface AuditRowUi {
  207 |   id: string;
  208 |   event: string;
  209 |   actor: string;
  210 |   caseNo: string;
  211 |   iso: string;
  212 |   actorText: string;
  213 |   role: string;
  214 |   eventText: string;
  215 |   caseText: string;
  216 |   transition: string;
  217 |   detail: string;
  218 | }
  219 | 
  220 | /** อ่านทุกแถว audit-row บนจอ (ลำดับตามจอ) */
  221 | export async function auditRowsUi(p: Page): Promise<AuditRowUi[]> {
  222 |   return tid(p, 'audit-row').evaluateAll((rows) =>
  223 |     rows.map((r) => {
  224 |       const cell = (id: string) => r.querySelector(`[data-testid="${id}"]`);
  225 |       const txt = (id: string) => (cell(id)?.textContent ?? '').replace(/\s+/g, ' ').trim();
  226 |       return {
  227 |         id: r.getAttribute('data-id') ?? '',
  228 |         event: r.getAttribute('data-event') ?? '',
  229 |         actor: r.getAttribute('data-actor') ?? '',
  230 |         caseNo: r.getAttribute('data-case-no') ?? '',
  231 |         iso: cell('audit-time')?.getAttribute('data-iso') ?? '',
  232 |         actorText: txt('audit-actor'),
  233 |         role: txt('audit-role'),
  234 |         eventText: txt('audit-event'),
  235 |         caseText: txt('audit-case-no'),
  236 |         transition: txt('audit-transition'),
  237 |         detail: txt('audit-detail'),
  238 |       };
  239 |     }),
  240 |   );
  241 | }
  242 | 
  243 | /** กรองบนจอแล้วตรวจ audit-count + จำนวนแถว แล้วคืนแถว */
  244 | export async function uiAuditExpect(p: Page, f: AuditFilter, count: number): Promise<AuditRowUi[]> {
  245 |   await uiAudit(p, f);
  246 |   await expect(tid(p, 'audit-count')).toHaveText(String(count));
  247 |   await expect(tid(p, 'audit-row')).toHaveCount(count);
  248 |   return auditRowsUi(p);
  249 | }
  250 | 
  251 | // ───────────────────────── ดาวน์โหลด ─────────────────────────
  252 | 
  253 | export interface Grabbed {
  254 |   url: string;
  255 |   status: number;
  256 |   contentType: string;
  257 |   disposition: string;
  258 |   filename: string;
  259 |   body: Buffer;
  260 | }
  261 | 
  262 | /** ชื่อไฟล์จาก Content-Disposition (รองรับ filename*=UTF-8'') */
  263 | export function dispositionName(h: string): string {
  264 |   const star = /filename\*\s*=\s*[^']*'[^']*'([^;]+)/i.exec(h);
  265 |   if (star) return decodeURIComponent(star[1].trim().replace(/^"|"$/g, ''));
  266 |   const m = /filename\s*=\s*"?([^";]+)"?/i.exec(h);
  267 |   return m ? m[1].trim() : '';
  268 | }
  269 | 
  270 | /**
  271 |  * กดปุ่ม/ลิงก์ดาวน์โหลดแล้วดักไฟล์ที่ได้ (ผ่าน context.route → เซิร์ฟเวอร์ถูกเรียกครั้งเดียว)
  272 |  * ใช้ได้ทั้งลิงก์ <a href>, form GET, fetch + blob และแท็บใหม่ · `want` = regex ของ Content-Type ที่ต้องการ
  273 |  * ลิงก์ที่มีแอตทริบิวต์ `download` ใช้ไม่ได้: Chromium ส่งไปตัวจัดการดาวน์โหลดตรง ไม่ผ่าน context.route
  274 |  * (อ่าน status/header ไม่ได้) → ล้มทันทีพร้อมบอกสาเหตุ แทนที่จะรอจนหมดเวลา
  275 |  */
  276 | export async function grabDownload(p: Page, click: () => Promise<unknown>, want: RegExp): Promise<Grabbed> {
  277 |   const box: { got?: Grabbed; bypassed?: string } = {};
  278 |   const ctx = p.context();
  279 |   const onDownload = (d: { url(): string }) => {
```