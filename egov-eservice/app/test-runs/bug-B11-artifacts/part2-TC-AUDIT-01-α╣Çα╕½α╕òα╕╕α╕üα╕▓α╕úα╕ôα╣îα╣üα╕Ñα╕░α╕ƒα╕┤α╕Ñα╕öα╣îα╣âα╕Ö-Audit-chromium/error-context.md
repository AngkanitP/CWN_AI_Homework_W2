# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-AUDIT-01 เหตุการณ์และฟิลด์ใน Audit
- Location: tests/part2.spec.ts:1107:1

# Error details

```
Error: expect(locator).toHaveText(expected) failed

Locator:  getByTestId('audit-count')
Expected: "16"
Received: "15"
Timeout:  7000ms

Call log:
  - Expect "toHaveText" getByTestId('audit-count') with timeout 7000ms
  - waiting for getByTestId('audit-count')
    18 × locator resolved to <strong data-testid="audit-count">15</strong>
       - unexpected value "15"

```

```yaml
- strong: "15"
```

# Test source

```ts
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
  179 |   if (k.pct !== undefined) await expect(tid(p, 'kpi-ontime-pct')).toHaveText(k.pct);
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
> 246 |   await expect(tid(p, 'audit-count')).toHaveText(String(count));
      |                                       ^ Error: expect(locator).toHaveText(expected) failed
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
  280 |     if (!box.got) box.bypassed = d.url();
  281 |   };
  282 |   const handler = async (route: Route) => {
  283 |     const req = route.request();
  284 |     if (box.got || req.method() !== 'GET' || !['document', 'fetch', 'xhr', 'other'].includes(req.resourceType())) {
  285 |       await route.continue().catch(() => {});
  286 |       return;
  287 |     }
  288 |     let resp;
  289 |     try {
  290 |       resp = await route.fetch();
  291 |     } catch {
  292 |       await route.continue().catch(() => {});
  293 |       return;
  294 |     }
  295 |     const h = resp.headers();
  296 |     const body = await resp.body();
  297 |     const ct = h['content-type'] ?? '';
  298 |     const cd = h['content-disposition'] ?? '';
  299 |     if (!box.got && (/attachment|filename/i.test(cd) || want.test(ct))) {
  300 |       box.got = { url: req.url(), status: resp.status(), contentType: ct, disposition: cd, filename: dispositionName(cd), body };
  301 |     }
  302 |     await route.fulfill({ response: resp, body }).catch(() => {});
  303 |   };
  304 |   await ctx.route('**/*', handler);
  305 |   p.on('download', onDownload);
  306 |   try {
  307 |     await click();
  308 |     await expect.poll(() => !!box.got || !!box.bypassed, { timeout: 20_000, message: `ไม่ได้ไฟล์ดาวน์โหลด (${want})` }).toBe(true);
  309 |   } finally {
  310 |     p.off('download', onDownload);
  311 |     await ctx.unroute('**/*', handler).catch(() => {});
  312 |   }
  313 |   if (!box.got) throw new Error(`ดาวน์โหลด ${box.bypassed} ไม่ผ่าน context.route (ลิงก์มีแอตทริบิวต์ download?) จึงตรวจ status/Content-Type ไม่ได้`);
  314 |   return box.got;
  315 | }
  316 | 
  317 | // ───────────────────────── PDF (ข้อความที่เครื่องอ่านได้) ─────────────────────────
  318 | 
  319 | function pdfLiteral(s: string, i: number): [string, number] {
  320 |   // s[i] === '('
  321 |   let depth = 1;
  322 |   let out = '';
  323 |   i++;
  324 |   while (i < s.length && depth > 0) {
  325 |     const c = s[i];
  326 |     if (c === '\\') {
  327 |       const n = s[i + 1];
  328 |       const map: Record<string, string> = { n: '\n', r: '\r', t: '\t', b: '\b', f: '\f', '(': '(', ')': ')', '\\': '\\' };
  329 |       if (n in map) {
  330 |         out += map[n];
  331 |         i += 2;
  332 |       } else if (/[0-7]/.test(n)) {
  333 |         const oct = /^[0-7]{1,3}/.exec(s.slice(i + 1, i + 4))![0];
  334 |         out += String.fromCharCode(parseInt(oct, 8));
  335 |         i += 1 + oct.length;
  336 |       } else if (n === '\r' || n === '\n') {
  337 |         i += n === '\r' && s[i + 2] === '\n' ? 3 : 2;
  338 |       } else {
  339 |         out += n ?? '';
  340 |         i += 2;
  341 |       }
  342 |       continue;
  343 |     }
  344 |     if (c === '(') depth++;
  345 |     if (c === ')') depth--;
  346 |     if (depth > 0) out += c;
```