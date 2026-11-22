# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-RBAC-01 ประชาชนเปิดคำขอคนอื่นไม่ได้ (IDOR)
- Location: tests\part2.spec.ts:1316:1

# Error details

```
Error: สมหญิงเปิด /citizen/cases/EG-2569-000005 (ของสมชาย) ต้องได้ HTTP

expect(received).toBe(expected) // Object.is equality

Expected: 404
Received: 200
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
          - text: สมหญิง รักไทย
          - generic [ref=e12]: ประชาชน
        - button "ออกจากระบบ" [ref=e14] [cursor=pointer]
  - main [ref=e15]:
    - paragraph [ref=e16]:
      - link "← คำขอของฉัน" [ref=e17] [cursor=pointer]:
        - /url: /citizen
    - heading "คำขอ EG-2569-000005" [level=1] [ref=e18]
    - region "รายละเอียดคำขอ" [ref=e19]:
      - heading "รายละเอียดคำขอ" [level=2] [ref=e20]
      - generic [ref=e21]:
        - term [ref=e22]: สถานะ
        - definition [ref=e23]:
          - generic [ref=e24]: เสร็จสิ้น
        - term [ref=e25]: บริการ
        - definition [ref=e26]: SV-01 ขอหนังสือรับรอง
        - term [ref=e27]: ข้อมูลที่กรอก
        - definition [ref=e28]: จำนวน 1 ฉบับ
        - term [ref=e29]: ค่าธรรมเนียม
        - definition [ref=e30]: ฿20
        - term [ref=e31]: เลขใบเสร็จ
        - definition [ref=e32]: RC-2569-000005
        - term [ref=e33]: ชำระเมื่อ
        - definition [ref=e34]:
          - time [ref=e35]: 3 พ.ย. 2569 11:00
        - term [ref=e36]: กำหนดเสร็จ
        - definition [ref=e37]:
          - time [ref=e38]: 6 พ.ย. 2569 16:30
        - term [ref=e39]: ระดับเตือน
        - definition [ref=e40]:
          - generic [ref=e41]: ปิดแล้ว
        - term [ref=e42]: ปิดงานเมื่อ
        - definition [ref=e43]:
          - time [ref=e44]: 5 พ.ย. 2569 10:00
        - term [ref=e45]: ผู้ยื่น
        - definition [ref=e46]: สมชาย ใจดี
        - term [ref=e47]: เลขบัตรประชาชน
        - definition [ref=e48]: 1-1017-00123-45-6
    - region "เอกสารดิจิทัล" [ref=e49]:
      - heading "เอกสารดิจิทัล" [level=2] [ref=e50]
      - generic [ref=e51]:
        - term [ref=e52]: เลขเอกสาร
        - definition [ref=e53]: DOC-2569-000001
        - term [ref=e54]: รหัสตรวจสอบ
        - definition [ref=e55]: K7M2Q9XA
        - term [ref=e56]: ใช้ได้ถึง
        - definition [ref=e57]:
          - time [ref=e58]: 2 ก.พ. 2570
      - generic [ref=e59]:
        - img "QR ตรวจสอบเอกสาร" [ref=e60]
        - paragraph [ref=e63]:
          - link "http://localhost:3000/verify/K7M2Q9XA" [ref=e64] [cursor=pointer]:
            - /url: http://localhost:3000/verify/K7M2Q9XA
      - paragraph [ref=e65]:
        - link "ดาวน์โหลดเอกสาร" [ref=e66] [cursor=pointer]:
          - /url: /api/documents/DOC-2569-000001/pdf
    - region "เอกสารแนบ" [ref=e67]:
      - heading "เอกสารแนบ" [level=2] [ref=e68]
      - list [ref=e69]:
        - listitem [ref=e70]:
          - text: "บัตรประชาชน:"
          - link "id-card.pdf" [ref=e71] [cursor=pointer]:
            - /url: /api/files/f_seed_000005_id-card
          - text: (1 KB)
    - region "ไทม์ไลน์" [ref=e72]:
      - heading "ไทม์ไลน์" [level=2] [ref=e73]
      - list [ref=e74]:
        - listitem [ref=e75]:
          - time [ref=e76]: 3 พ.ย. 2569 11:00
          - text: · ชำระค่าธรรมเนียมและส่งคำขอแล้ว (ใบเสร็จ RC-2569-000005)
        - listitem [ref=e77]:
          - time [ref=e78]: 3 พ.ย. 2569 11:30
          - text: · เจ้าหน้าที่รับเรื่อง
        - listitem [ref=e79]:
          - time [ref=e80]: 5 พ.ย. 2569 09:30
          - text: · อนุมัติ
        - listitem [ref=e81]:
          - time [ref=e82]: 5 พ.ย. 2569 10:00
          - text: · ออกเอกสารดิจิทัล DOC-2569-000001
  - contentinfo [ref=e83]:
    - paragraph [ref=e84]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  1223 | 
  1224 | test('TC-AUDIT-02 Audit แก้/ลบไม่ได้ (405)', async ({ browser }) => {
  1225 |   await reset();
  1226 |   const auditor = await loginStaff('audit1');
  1227 |   const before = await auditItems(auditor);
  1228 |   expect(before).toHaveLength(1);
  1229 |   expect(before[0].event).toBe('STAFF_LOGIN');
  1230 |   const id = before[0].id;
  1231 | 
  1232 |   const admin = await loginStaff('admin1');
  1233 |   for (const [who, api] of [
  1234 |     ['admin1', admin],
  1235 |     ['audit1', auditor],
  1236 |   ] as const) {
  1237 |     await test.step(`${who} แก้/ลบ Audit → 405`, async () => {
  1238 |       const calls: Array<[string, () => Promise<APIResponse>]> = [
  1239 |         [`PUT /api/audit/${id}`, () => api.put(`/api/audit/${id}`, { data: { detail: 'x' } })],
  1240 |         [`PATCH /api/audit/${id}`, () => api.patch(`/api/audit/${id}`, { data: { detail: 'x' } })],
  1241 |         [`DELETE /api/audit/${id}`, () => api.delete(`/api/audit/${id}`)],
  1242 |         ['PUT /api/audit', () => api.put('/api/audit', { data: { detail: 'x' } })],
  1243 |         ['DELETE /api/audit', () => api.delete('/api/audit')],
  1244 |         ['DELETE /api/audit/999999', () => api.delete('/api/audit/999999')],
  1245 |       ];
  1246 |       for (const [label, call] of calls) {
  1247 |         const r = await call();
  1248 |         const b = await bodyOf(r);
  1249 |         expect.soft(r.status(), `${who} ${label}`).toBe(405);
  1250 |         expect.soft(b.code, `${who} ${label}`).toBe('METHOD_NOT_ALLOWED');
  1251 |       }
  1252 |     });
  1253 |   }
  1254 | 
  1255 |   await test.step('ข้อมูลเดิมครบ เพิ่มเฉพาะ STAFF_LOGIN ของ admin1', async () => {
  1256 |     const after = await auditItems(auditor);
  1257 |     for (const b of before) expect(after).toContainEqual(b);
  1258 |     expect(after).toHaveLength(before.length + 1);
  1259 |     const added = after.filter((a) => !before.some((b) => b.id === a.id));
  1260 |     expect(added).toHaveLength(1);
  1261 |     expect(added[0].event).toBe('STAFF_LOGIN');
  1262 |     expect(added[0].username).toBe('admin1');
  1263 |   });
  1264 | 
  1265 |   await test.step('UI ไม่มีปุ่มแก้/ลบ · admin อ่าน Audit ไม่ได้', async () => {
  1266 |     const { page: p } = await pageFromApi(browser, auditor);
  1267 |     await p.goto('/audit');
  1268 |     await expect(tid(p, 'audit-row')).not.toHaveCount(0);
  1269 |     await expect(tid(p, 'audit-edit-btn')).toHaveCount(0);
  1270 |     await expect(tid(p, 'audit-delete-btn')).toHaveCount(0);
  1271 |     await expectApi(admin.get('/api/audit'), 403);
  1272 |   });
  1273 | });
  1274 | 
  1275 | test('TC-AUDIT-03 กรองช่วงวันที่ตามเวลาไทย', async ({ browser }) => {
  1276 |   await reset();
  1277 |   const L: Record<string, { iso: string; user: StaffUser }> = {
  1278 |     L1: { iso: '2026-11-30T23:59:59+07:00', user: 'off.reg1' },
  1279 |     L2: { iso: '2026-12-01T00:00:00+07:00', user: 'off.reg2' },
  1280 |     L3: { iso: '2026-12-01T23:59:59+07:00', user: 'off.works1' },
  1281 |     L4: { iso: '2026-12-02T00:00:00+07:00', user: 'off.reg1' },
  1282 |     L5: { iso: '2026-12-02T09:00:00+07:00', user: 'audit1' },
  1283 |   };
  1284 |   let auditor!: APIRequestContext;
  1285 |   for (const [k, { iso, user }] of Object.entries(L)) {
  1286 |     await setClock(iso);
  1287 |     const api = await loginStaff(user);
  1288 |     if (k === 'L5') auditor = api;
  1289 |   }
  1290 |   const { page: p } = await pageFromApi(browser, auditor);
  1291 | 
  1292 |   const CASES: Array<{ from: string; to: string; actor?: string; rows: string[] }> = [
  1293 |     { from: '2026-12-01', to: '2026-12-01', rows: ['L2', 'L3'] },
  1294 |     { from: '2026-11-30', to: '2026-11-30', rows: ['L1'] },
  1295 |     { from: '2026-11-30', to: '2026-12-01', rows: ['L1', 'L2', 'L3'] },
  1296 |     { from: '2026-12-02', to: '', rows: ['L4', 'L5'] },
  1297 |     { from: '', to: '2026-11-30', rows: ['L1'] },
  1298 |     { from: '2026-12-01', to: '2026-12-02', rows: ['L2', 'L3', 'L4', 'L5'] },
  1299 |     { from: '2026-12-01', to: '2026-12-01', actor: 'off.reg2', rows: ['L2'] },
  1300 |   ];
  1301 |   for (const c of CASES) {
  1302 |     await test.step(`from=${c.from || '(ว่าง)'} to=${c.to || '(ว่าง)'}${c.actor ? ` actor=${c.actor}` : ''}`, async () => {
  1303 |       // ใหม่ → เก่า
  1304 |       const want = c.rows.map((k) => L[k]).sort((a, b) => b.iso.localeCompare(a.iso));
  1305 |       const rows = await uiAuditExpect(p, { from: c.from, to: c.to, actor: c.actor }, want.length);
  1306 |       expect(rows.map((r) => r.iso)).toEqual(want.map((w) => w.iso));
  1307 |       expect(rows.map((r) => r.actor)).toEqual(want.map((w) => w.user));
  1308 |       const api = await auditItems(auditor, { from: c.from || undefined, to: c.to || undefined, actor: c.actor });
  1309 |       expect(api.map((a) => a.time).sort()).toEqual(want.map((w) => w.iso).sort());
  1310 |     });
  1311 |   }
  1312 | });
  1313 | 
  1314 | // ═══════════════════════════════════ RBAC ═══════════════════════════════════
  1315 | 
  1316 | test('TC-RBAC-01 ประชาชนเปิดคำขอคนอื่นไม่ได้ (IDOR)', async ({ browser }) => {
  1317 |   await reset();
  1318 |   const sy = await citizenSession(browser, ID.SOMYING);
  1319 |   const p = sy.page;
  1320 | 
  1321 |   await test.step('UI คำขอของสมชาย → 404', async () => {
  1322 |     const res = await p.goto(`/citizen/cases/${caseNo(5)}`);
> 1323 |     expect(res?.status(), `สมหญิงเปิด /citizen/cases/${caseNo(5)} (ของสมชาย) ต้องได้ HTTP`).toBe(404);
       |                                                                                             ^ Error: สมหญิงเปิด /citizen/cases/EG-2569-000005 (ของสมชาย) ต้องได้ HTTP
  1324 |     await expect(tid(p, 'not-found-msg')).toHaveText(MSG.NOT_FOUND);
  1325 |     await expect(tid(p, 'case-no')).toHaveCount(0);
  1326 |     await expect(tid(p, 'case-status')).toHaveCount(0);
  1327 |     expect(await p.content()).not.toContain('สมชาย');
  1328 |   });
  1329 | 
  1330 |   await test.step('API ของคนอื่น = ไม่มีจริง (404 เหมือนกันทุกตัวอักษร)', async () => {
  1331 |     const other = await sy.api.get(`/api/cases/${caseNo(5)}`);
  1332 |     const none = await sy.api.get('/api/cases/EG-2569-999999');
  1333 |     expect(other.status()).toBe(404);
  1334 |     expect(none.status()).toBe(404);
  1335 |     expect(await bodyOf(other)).toEqual({ code: 'NOT_FOUND', message: MSG.NOT_FOUND });
  1336 |     expect(await none.text()).toBe(await other.text());
  1337 |     await expectApi(sy.api.get('/api/documents/DOC-2569-000001/pdf'), 404);
  1338 |     await expectApi(sy.api.get('/api/drafts/DR-0001'), 404);
  1339 |     await expectApi(sy.api.post(`/api/cases/${caseNo(30)}/cancel`), 404);
  1340 |   });
  1341 | 
  1342 |   await test.step('ของตัวเองเปิดได้ · สมชายเปิดของตัวเองได้', async () => {
  1343 |     const res = await p.goto(`/citizen/cases/${caseNo(7)}`);
  1344 |     expect(res?.status()).toBe(200);
  1345 |     await expect(tid(p, 'case-no')).toHaveText(caseNo(7));
  1346 |     const sc = await loginCitizen(ID.SOMCHAI);
  1347 |     await expectApi(sc.get(`/api/cases/${caseNo(5)}`), 200);
  1348 |     expect((await getCase(sc, caseNo(30))).status).toBe('SUBMITTED');
  1349 |   });
  1350 | });
  1351 | 
  1352 | test('TC-RBAC-02 เจ้าหน้าที่อนุมัติ SV-02 ไม่ได้ (API)', async ({ browser }) => {
  1353 |   await reset();
  1354 |   const reg2 = await staffSession(browser, 'off.reg2');
  1355 | 
  1356 |   await test.step('1–3 off.reg2 approve/reject SV-02 ทาง API → 403', async () => {
  1357 |     await expectApi(approveRaw(reg2.api, caseNo(14)), 403, 'FORBIDDEN');
  1358 |     expect((await getCase(reg2.api, caseNo(14))).status).toBe('PENDING_APPROVAL');
  1359 |     await expectApi(approveRaw(reg2.api, caseNo(13)), 403, 'FORBIDDEN');
  1360 |     expect((await getCase(reg2.api, caseNo(13))).status).toBe('IN_REVIEW');
  1361 |     await expectApi(rejectRaw(reg2.api, caseNo(14), R10), 403);
  1362 |     expect((await getCase(reg2.api, caseNo(14))).status).toBe('PENDING_APPROVAL');
  1363 |   });
  1364 | 
  1365 |   await test.step('4 UI ไม่มี approve-btn', async () => {
  1366 |     for (const n of [13, 14]) {
  1367 |       await openOfficer(reg2.page, caseNo(n));
  1368 |       await expect(tid(reg2.page, 'approve-btn')).toHaveCount(0);
  1369 |     }
  1370 |   });
  1371 | 
  1372 |   await test.step('5–6 head1: SV-01 → 403 · SV-02 รออนุมัติ → 200', async () => {
  1373 |     const head = await loginStaff('head1');
  1374 |     await expectApi(approveRaw(head, caseNo(25)), 403);
  1375 |     expect((await getCase(head, caseNo(25))).status).toBe('IN_REVIEW');
  1376 |     await apiApprove(head, caseNo(14));
  1377 |   });
  1378 | 
  1379 |   await test.step('7 Audit APPROVE มีเฉพาะ head1', async () => {
  1380 |     const { page: a } = await staffSession(browser, 'audit1');
  1381 |     const rows = await uiAuditExpect(a, { event: 'APPROVE' }, 1);
  1382 |     expect(rows[0].actor).toBe('head1');
  1383 |     expect(rows[0].caseNo).toBe(caseNo(14));
  1384 |   });
  1385 | });
  1386 | 
  1387 | test('TC-RBAC-03 ตารางสิทธิ์หน้า/API ตามบทบาท', async ({ browser }) => {
  1388 |   test.setTimeout(300_000);
  1389 |   type Role = 'anon' | 'citizen' | 'officer' | 'head' | 'executive' | 'auditor' | 'admin';
  1390 |   const ROLES: Role[] = ['anon', 'citizen', 'officer', 'head', 'executive', 'auditor', 'admin'];
  1391 |   const USER: Partial<Record<Role, StaffUser>> = { officer: 'off.reg1', head: 'head1', executive: 'exec1', auditor: 'audit1', admin: 'admin1' };
  1392 |   const by = <T,>(...v: T[]): Record<Role, T> => Object.fromEntries(ROLES.map((r, i) => [r, v[i]])) as Record<Role, T>;
  1393 | 
  1394 |   type PageExp = 'ok' | 403 | 'login';
  1395 |   const PAGES: Array<[string, Record<Role, PageExp>]> = [
  1396 |     ['/citizen', by<PageExp>('login', 'ok', 403, 403, 403, 403, 403)],
  1397 |     ['/officer/queue', by<PageExp>('login', 403, 'ok', 'ok', 403, 403, 403)],
  1398 |     ['/head/approvals', by<PageExp>('login', 403, 403, 'ok', 403, 403, 403)],
  1399 |     ['/dashboard', by<PageExp>('login', 403, 403, 403, 'ok', 403, 403)],
  1400 |     ['/audit', by<PageExp>('login', 403, 403, 403, 403, 'ok', 403)],
  1401 |     ['/admin/services', by<PageExp>('login', 403, 403, 403, 403, 403, 'ok')],
  1402 |     ['/admin/holidays', by<PageExp>('login', 403, 403, 403, 403, 403, 'ok')],
  1403 |     ['/admin/users', by<PageExp>('login', 403, 403, 403, 403, 403, 'ok')],
  1404 |     ['/notifications', by<PageExp>('login', 403, 'ok', 'ok', 403, 403, 403)],
  1405 |     ['/verify/K7M2Q9XA', by<PageExp>('ok', 'ok', 'ok', 'ok', 'ok', 'ok', 'ok')],
  1406 |   ];
  1407 | 
  1408 |   type Ctx = { api: APIRequestContext; somying: APIRequestContext };
  1409 |   const APIS: Array<[string, (c: Ctx) => Promise<APIResponse>, Record<Role, number>]> = [
  1410 |     ['GET /api/officer/queue', (c) => c.api.get('/api/officer/queue'), by(401, 403, 200, 200, 403, 403, 403)],
  1411 |     ['GET /api/notifications', (c) => c.api.get('/api/notifications'), by(401, 403, 200, 200, 403, 403, 403)],
  1412 |     ['GET /api/dashboard', (c) => c.api.get('/api/dashboard?period=2026-12&service=ALL'), by(401, 403, 403, 403, 200, 403, 403)],
  1413 |     ['GET /api/audit', (c) => c.api.get('/api/audit'), by(401, 403, 403, 403, 403, 200, 403)],
  1414 |     ['GET /api/admin/services', (c) => c.api.get('/api/admin/services'), by(401, 403, 403, 403, 403, 403, 200)],
  1415 |     ['POST /api/drafts', (c) => c.api.post('/api/drafts', { data: { serviceId: 'SV-01', qty: 1 } }), by(401, 201, 403, 403, 403, 403, 403)],
  1416 |     ['GET /api/cases/EG-2569-000025', (c) => c.somying.get(`/api/cases/${caseNo(25)}`), by(401, 200, 200, 200, 403, 403, 403)],
  1417 |     // แถว claim เรียกท้ายสุด (ผู้ถือเรื่องยังไม่เปลี่ยนก่อน)
  1418 |     ['POST claim EG-2569-000028', (c) => c.api.post(`/api/officer/cases/${caseNo(28)}/claim`), by(401, 403, 200, 403, 403, 403, 403)],
  1419 |   ];
  1420 | 
  1421 |   const NAVS = ['nav-my-cases', 'nav-queue', 'nav-approvals', 'nav-dashboard', 'nav-audit', 'nav-admin-services', 'nav-admin-holidays', 'nav-admin-users', 'nav-bell'];
  1422 |   const NAV_OF: Partial<Record<Role, string[]>> = {
  1423 |     citizen: ['nav-my-cases'],
```