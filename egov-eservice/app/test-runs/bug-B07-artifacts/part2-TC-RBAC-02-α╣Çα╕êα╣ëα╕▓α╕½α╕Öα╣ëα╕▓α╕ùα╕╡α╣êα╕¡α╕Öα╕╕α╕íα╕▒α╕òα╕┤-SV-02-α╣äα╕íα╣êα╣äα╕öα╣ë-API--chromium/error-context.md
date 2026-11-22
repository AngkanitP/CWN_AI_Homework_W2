# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-RBAC-02 เจ้าหน้าที่อนุมัติ SV-02 ไม่ได้ (API)
- Location: tests/part2.spec.ts:1352:1

# Error details

```
Error: http://localhost:3000/api/cases/EG-2569-000014/approve → 200 {"status":"APPROVED"}

expect(received).toBe(expected) // Object.is equality

Expected: 403
Received: 200
```

# Test source

```ts
  109 |   DRAFT: 'ร่าง',
  110 |   PENDING_PAYMENT: 'รอชำระเงิน',
  111 |   SUBMITTED: 'ส่งคำขอแล้ว',
  112 |   IN_REVIEW: 'กำลังตรวจสอบ',
  113 |   NEED_FIX: 'รอแก้ไขเอกสาร',
  114 |   PENDING_APPROVAL: 'รออนุมัติ',
  115 |   APPROVED: 'อนุมัติ',
  116 |   COMPLETED: 'เสร็จสิ้น',
  117 |   REJECTED: 'ไม่อนุมัติ',
  118 |   CANCELLED: 'ยกเลิก',
  119 | } as const;
  120 | 
  121 | export const LEVEL_TH = {
  122 |   normal: 'ปกติ',
  123 |   near: 'ใกล้ครบกำหนด',
  124 |   overdue: 'เกินกำหนด',
  125 |   paused: 'หยุดนับ',
  126 |   closed: 'ปิดแล้ว',
  127 | } as const;
  128 | export type SlaLevel = keyof typeof LEVEL_TH;
  129 | 
  130 | /** เลขคำขอ: caseNo(25) → 'EG-2569-000025' */
  131 | export const caseNo = (n: number, year = 2569): string => `EG-${year}-${String(n).padStart(6, '0')}`;
  132 | export const receiptNo = (n: number, year = 2569): string => `RC-${year}-${String(n).padStart(6, '0')}`;
  133 | /** ref ชำระ: ppRef(2) → 'PP-0002' */
  134 | export const ppRef = (n: number): string => `PP-${String(n).padStart(4, '0')}`;
  135 | export const draftId = (n: number): string => `DR-${String(n).padStart(4, '0')}`;
  136 | 
  137 | // ───────────────────────── ไฟล์ทดสอบ (TEST-DATA §11) ─────────────────────────
  138 | 
  139 | let fixturesReady = false;
  140 | /** path ของไฟล์ทดสอบใน e2e/fixtures/files (สร้างอัตโนมัติถ้ายังไม่มี) */
  141 | export function fixturePath(name: string): string {
  142 |   if (!fixturesReady) {
  143 |     makeFixtures();
  144 |     fixturesReady = true;
  145 |   }
  146 |   const p = path.join(FIXTURE_DIR, name);
  147 |   if (!fs.existsSync(p)) throw new Error(`ไม่มีไฟล์ทดสอบ ${name}`);
  148 |   return p;
  149 | }
  150 | export function fixtureBuffer(name: string): Buffer {
  151 |   return fs.readFileSync(fixturePath(name));
  152 | }
  153 | export function mimeOf(name: string): string {
  154 |   const ext = path.extname(name).toLowerCase();
  155 |   return ext === '.pdf' ? 'application/pdf' : ext === '.jpg' || ext === '.jpeg' ? 'image/jpeg' : ext === '.png' ? 'image/png' : 'text/plain';
  156 | }
  157 | export interface FilePayload {
  158 |   name: string;
  159 |   mimeType: string;
  160 |   buffer: Buffer;
  161 | }
  162 | export function filePayload(name: string, mimeType = mimeOf(name)): FilePayload {
  163 |   return { name, mimeType, buffer: fixtureBuffer(name) };
  164 | }
  165 | 
  166 | // ───────────────────────── context ที่เปิด + ปิดท้าย test ─────────────────────────
  167 | 
  168 | const openedApis: APIRequestContext[] = [];
  169 | const openedContexts: BrowserContext[] = [];
  170 | 
  171 | /** request context ใหม่ (cookie แยก) */
  172 | export async function newApi(): Promise<APIRequestContext> {
  173 |   const api = await pwRequest.newContext({ baseURL: BASE_URL });
  174 |   openedApis.push(api);
  175 |   return api;
  176 | }
  177 | 
  178 | /** ปิดทุก context ที่เปิดผ่าน helper (เรียกใน test.afterEach) */
  179 | export async function cleanup(): Promise<void> {
  180 |   while (openedContexts.length) await openedContexts.pop()!.close().catch(() => {});
  181 |   while (openedApis.length) await openedApis.pop()!.dispose().catch(() => {});
  182 | }
  183 | 
  184 | let hookApi: APIRequestContext | null = null;
  185 | /** context สำหรับ /api/test/* (ไม่ต้องล็อกอิน · ไม่ถูกปิดโดย cleanup) */
  186 | async function hooks(): Promise<APIRequestContext> {
  187 |   if (!hookApi) hookApi = await pwRequest.newContext({ baseURL: BASE_URL });
  188 |   return hookApi;
  189 | }
  190 | 
  191 | // ───────────────────────── ตรวจ response ─────────────────────────
  192 | 
  193 | /** อ่าน body เป็น JSON (ถ้าไม่ใช่ JSON คืน { _raw }) */
  194 | export async function bodyOf(res: APIResponse): Promise<any> {
  195 |   const text = await res.text().catch(() => '');
  196 |   if (!text) return {};
  197 |   try {
  198 |     return JSON.parse(text);
  199 |   } catch {
  200 |     return { _raw: text };
  201 |   }
  202 | }
  203 | 
  204 | /** ตรวจ HTTP status (+ code ของ error) แล้วคืน body */
  205 | export async function expectApi(res: APIResponse | Promise<APIResponse>, status: number, code?: string): Promise<any> {
  206 |   const r = await res;
  207 |   const body = await bodyOf(r);
  208 |   const info = `${r.url()} → ${r.status()} ${JSON.stringify(body).slice(0, 400)}`;
> 209 |   expect(r.status(), info).toBe(status);
      |                            ^ Error: http://localhost:3000/api/cases/EG-2569-000014/approve → 200 {"status":"APPROVED"}
  210 |   if (code !== undefined) expect(body.code, info).toBe(code);
  211 |   return body;
  212 | }
  213 | 
  214 | // ───────────────────────── test hook: RESET / CLOCK / pay ─────────────────────────
  215 | 
  216 | /** RESET: POST /api/test/reset → 200 {"ok":true,"now":T0} (ล้าง session ทุกคน) */
  217 | export async function reset(): Promise<void> {
  218 |   const body = await expectApi((await hooks()).post('/api/test/reset'), 200);
  219 |   expect(body.ok).toBe(true);
  220 |   expect(body.now).toBe(T0);
  221 | }
  222 | 
  223 | /** CLOCK(t): PUT /api/test/clock {"now":t} (นาฬิกาแช่แข็ง) */
  224 | export async function setClock(now: string): Promise<void> {
  225 |   const body = await expectApi((await hooks()).put('/api/test/clock', { data: { now } }), 200);
  226 |   expect(body.now).toBe(now);
  227 | }
  228 | 
  229 | export async function getClock(): Promise<string> {
  230 |   const body = await expectApi((await hooks()).get('/api/test/clock'), 200);
  231 |   return body.now;
  232 | }
  233 | 
  234 | /** POST /api/test/payments/<ref>/pay — คืน response ดิบ */
  235 | export async function payRaw(ref: string, amount: number): Promise<APIResponse> {
  236 |   return (await hooks()).post(`/api/test/payments/${ref}/pay`, { data: { amount } });
  237 | }
  238 | 
  239 | /** ชำระสำเร็จ (คาด 200 PAID) คืน { status, caseNo, receiptNo, duplicate } */
  240 | export async function pay(ref: string, amount: number): Promise<{ status: string; caseNo: string; receiptNo: string; duplicate: boolean }> {
  241 |   const body = await expectApi(payRaw(ref, amount), 200);
  242 |   expect(body.status).toBe('PAID');
  243 |   return body;
  244 | }
  245 | 
  246 | // ───────────────────────── ล็อกอินผ่าน API ─────────────────────────
  247 | 
  248 | /** LOGIN_C ผ่าน API: thaid/start + thaid/verify OTP 123456 (ใช้ api ที่ส่งมา หรือสร้างใหม่) */
  249 | export async function loginCitizen(idNo: string = ID.SOMCHAI, api?: APIRequestContext): Promise<APIRequestContext> {
  250 |   const ctx = api ?? (await newApi());
  251 |   const s = await expectApi(ctx.post('/api/auth/thaid/start', { data: { idNo } }), 200);
  252 |   expect(s.status).toBe('OTP_SENT');
  253 |   await expectApi(ctx.post('/api/auth/thaid/verify', { data: { idNo, otp: OTP_OK } }), 200);
  254 |   return ctx;
  255 | }
  256 | 
  257 | /** LOGIN_S ผ่าน API: POST /api/auth/staff/login รหัสผ่าน Test@1234 */
  258 | export async function loginStaff(username: StaffUser | string, api?: APIRequestContext, password = PASSWORD): Promise<APIRequestContext> {
  259 |   const ctx = api ?? (await newApi());
  260 |   const body = await expectApi(ctx.post('/api/auth/staff/login', { data: { username, password } }), 200);
  261 |   const info = STAFF[username as StaffUser];
  262 |   if (info) {
  263 |     expect(body.role).toBe(info.role);
  264 |     expect(body.landing).toBe(info.landing);
  265 |   }
  266 |   return ctx;
  267 | }
  268 | 
  269 | export async function logout(api: APIRequestContext): Promise<void> {
  270 |   await expectApi(api.post('/api/auth/logout'), 204);
  271 | }
  272 | 
  273 | // ───────────────────────── session ของ browser (หน้า + API cookie เดียวกัน) ─────────────────────────
  274 | 
  275 | export interface Session {
  276 |   context: BrowserContext;
  277 |   page: Page;
  278 |   /** context.request — ใช้ cookie เดียวกับหน้า */
  279 |   api: APIRequestContext;
  280 | }
  281 | 
  282 | /** browser context ใหม่ที่ยังไม่ล็อกอิน */
  283 | export async function newSession(browser: Browser): Promise<Session> {
  284 |   const context = await browser.newContext({
  285 |     baseURL: BASE_URL,
  286 |     locale: 'th-TH',
  287 |     timezoneId: 'Asia/Bangkok',
  288 |     viewport: { width: 1280, height: 900 },
  289 |   });
  290 |   openedContexts.push(context);
  291 |   const page = await context.newPage();
  292 |   page.on('dialog', (d) => d.accept().catch(() => {}));
  293 |   return { context, page, api: context.request };
  294 | }
  295 | 
  296 | /** browser context ที่ล็อกอินประชาชนแล้ว (ล็อกอินผ่าน API ของ context เดียวกัน) */
  297 | export async function citizenSession(browser: Browser, idNo: string = ID.SOMCHAI): Promise<Session> {
  298 |   const s = await newSession(browser);
  299 |   await loginCitizen(idNo, s.api);
  300 |   return s;
  301 | }
  302 | 
  303 | /** browser context ที่ล็อกอินเจ้าหน้าที่/บทบาทอื่นแล้ว */
  304 | export async function staffSession(browser: Browser, username: StaffUser): Promise<Session> {
  305 |   const s = await newSession(browser);
  306 |   await loginStaff(username, s.api);
  307 |   return s;
  308 | }
  309 | 
```