# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-SLA-01 กำหนดเสร็จตามตารางวันที่
- Location: tests/part1.spec.ts:1229:1

# Error details

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: "2026-12-08T16:30:00+07:00"
Received: "2026-12-07T16:30:00+07:00"
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
          - text: สมชาย ใจดี
          - generic [ref=e12]: ประชาชน
        - button "ออกจากระบบ" [ref=e14] [cursor=pointer]
  - main [ref=e15]:
    - paragraph [ref=e16]:
      - link "← คำขอของฉัน" [ref=e17] [cursor=pointer]:
        - /url: /citizen
    - heading "คำขอ EG-2569-000031" [level=1] [ref=e18]
    - region "รายละเอียดคำขอ" [ref=e19]:
      - heading "รายละเอียดคำขอ" [level=2] [ref=e20]
      - generic [ref=e21]:
        - term [ref=e22]: สถานะ
        - definition [ref=e23]:
          - generic [ref=e24]: ส่งคำขอแล้ว
        - term [ref=e25]: บริการ
        - definition [ref=e26]: SV-01 ขอหนังสือรับรอง
        - term [ref=e27]: ข้อมูลที่กรอก
        - definition [ref=e28]: จำนวน 1 ฉบับ
        - term [ref=e29]: ค่าธรรมเนียม
        - definition [ref=e30]: ฿20
        - term [ref=e31]: เลขใบเสร็จ
        - definition [ref=e32]: RC-2569-000031
        - term [ref=e33]: ชำระเมื่อ
        - definition [ref=e34]:
          - time [ref=e35]: 1 ธ.ค. 2569 16:29
        - term [ref=e36]: กำหนดเสร็จ
        - definition [ref=e37]:
          - time [ref=e38]: 4 ธ.ค. 2569 16:30
        - term [ref=e39]: ระดับเตือน
        - definition [ref=e40]:
          - generic [ref=e41]: ปกติ
        - term [ref=e42]: ผู้ยื่น
        - definition [ref=e43]: สมชาย ใจดี
        - term [ref=e44]: เลขบัตรประชาชน
        - definition [ref=e45]: 1-1017-00123-45-6
    - region "ยกเลิกคำขอ" [ref=e46]:
      - heading "ยกเลิกคำขอ" [level=2] [ref=e47]
      - paragraph [ref=e48]: ยกเลิกได้เฉพาะคำขอที่ยังไม่มีเจ้าหน้าที่รับเรื่อง
      - paragraph [ref=e49]:
        - button "ยกเลิกคำขอ" [ref=e50] [cursor=pointer]
    - region "เอกสารแนบ" [ref=e51]:
      - heading "เอกสารแนบ" [level=2] [ref=e52]
      - list [ref=e53]:
        - listitem [ref=e54]:
          - text: "บัตรประชาชน:"
          - link "id-card.pdf" [ref=e55] [cursor=pointer]:
            - /url: /api/files/f_af9930d48182b76aa0de9877
          - text: (1 KB)
    - region "ไทม์ไลน์" [ref=e56]:
      - heading "ไทม์ไลน์" [level=2] [ref=e57]
      - list [ref=e58]:
        - listitem [ref=e59]:
          - time [ref=e60]: 1 ธ.ค. 2569 16:29
          - text: · ชำระค่าธรรมเนียมและส่งคำขอแล้ว (ใบเสร็จ RC-2569-000031)
  - contentinfo [ref=e61]:
    - paragraph [ref=e62]: e-Service กลาง เทศบาลนครตัวอย่าง (หน่วยงานสมมติ) · ThaiD, PromptPay และลายเซ็นดิจิทัลเป็นระบบจำลอง
```

# Test source

```ts
  1150 |     expect((await getCase(reg2, NO)).owner).toBe('off.reg1');
  1151 |     expect(await queueItems(reg2, 'mine')).toHaveLength(9);
  1152 |     const s2 = await staffSession(browser, 'off.reg2');
  1153 |     await expectWorkload(s2.page, 9);
  1154 |     await expectApi(claimRaw(reg1, NO), 409, 'ALREADY_CLAIMED');
  1155 |     expect((await getCase(reg1, NO)).owner).toBe('off.reg1');
  1156 |     expect(await claimAuditCount(NO)).toBe(1);
  1157 |   });
  1158 | });
  1159 | 
  1160 | test('TC-QUEUE-03 งานในมือสูงสุด 10', async ({ browser }) => {
  1161 |   test.setTimeout(240_000);
  1162 |   await reset();
  1163 |   let s = await staffSession(browser, 'off.reg2');
  1164 |   let p = s.page;
  1165 |   const claimUi = async (n: number) => {
  1166 |     await p.goto('/officer/queue');
  1167 |     await withMutation(p, () => queueRow(p, caseNo(n)).getByTestId('claim-btn').click());
  1168 |   };
  1169 | 
  1170 |   // 1
  1171 |   await expectWorkload(p, 9);
  1172 |   // 2 ครั้งที่ 10
  1173 |   await claimUi(28);
  1174 |   await expect(tid(p, 'action-error')).toBeHidden();
  1175 |   await expectWorkload(p, 10);
  1176 |   expect((await getCase(s.api, caseNo(28))).owner).toBe('off.reg2');
  1177 |   // 3 ครั้งที่ 11 → เพดาน
  1178 |   await claimUi(29);
  1179 |   await expect(tid(p, 'action-error')).toHaveText(MSG.WORKLOAD_LIMIT);
  1180 |   const lim = await expectApi(claimRaw(s.api, caseNo(29)), 409, 'WORKLOAD_LIMIT');
  1181 |   expect(lim.message).toBe(MSG.WORKLOAD_LIMIT);
  1182 |   const c29 = await getCase(s.api, caseNo(29));
  1183 |   expect(c29.status).toBe('SUBMITTED');
  1184 |   expect(c29.owner || null).toBeNull();
  1185 |   await expectWorkload(p, 10);
  1186 |   // 4 อนุมัติ …000025 (SV-01 ของตัวเอง) → APPROVED ไม่นับ
  1187 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1188 |   await tid(p, 'approve-btn').click();
  1189 |   await expectStatus(p, 'APPROVED');
  1190 |   await expectWorkload(p, 9);
  1191 |   // 5
  1192 |   await claimUi(29);
  1193 |   await expectWorkload(p, 10);
  1194 |   expect((await getCase(s.api, caseNo(29))).owner).toBe('off.reg2');
  1195 |   // 6 off.reg1 (งานในมือ 3) ไม่ติดเพดาน
  1196 |   const reg1 = await loginStaff('off.reg1');
  1197 |   expect((await claim(reg1, caseNo(30))).owner).toBe('off.reg1');
  1198 | 
  1199 |   // 7 RESET · ตีกลับ …000025 → NEED_FIX ไม่นับ
  1200 |   await reset();
  1201 |   s = await staffSession(browser, 'off.reg2');
  1202 |   p = s.page;
  1203 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1204 |   await tid(p, 'return-btn').click();
  1205 |   await tid(p, 'return-reason').fill('xxxxxxxxxx');
  1206 |   await tid(p, 'return-submit').click();
  1207 |   await expectStatus(p, 'NEED_FIX');
  1208 |   await expectWorkload(p, 8);
  1209 |   // 8
  1210 |   await claimUi(28);
  1211 |   await claimUi(29);
  1212 |   await expectWorkload(p, 10);
  1213 |   // 9 สมหญิงส่งแก้ → คืนผู้ถือเดิมแม้เกิน 10
  1214 |   const c = await citizenSession(browser, ID.SOMYING);
  1215 |   await c.page.goto(`/citizen/cases/${caseNo(25)}`);
  1216 |   await tid(c.page, 'submit-fix-btn').click();
  1217 |   await expect(tid(c.page, 'action-error')).toBeHidden();
  1218 |   await expectStatus(c.page, 'IN_REVIEW');
  1219 |   expect((await getCase(s.api, caseNo(25))).owner).toBe('off.reg2');
  1220 |   await expectWorkload(p, 11);
  1221 |   // 10 รับเพิ่มไม่ได้
  1222 |   const b10 = await expectApi(claimRaw(s.api, caseNo(30)), 409, 'WORKLOAD_LIMIT');
  1223 |   expect(b10.message).toBe(MSG.WORKLOAD_LIMIT);
  1224 |   await expectWorkload(p, 11);
  1225 | });
  1226 | 
  1227 | // ═══════════════════════════════════ SLA ═══════════════════════════════════
  1228 | 
  1229 | test('TC-SLA-01 กำหนดเสร็จตามตารางวันที่', async ({ browser }) => {
  1230 |   test.setTimeout(360_000);
  1231 |   const rows: Array<{ row: string; service: 'SV-01' | 'SV-02' | 'SV-03'; at: string; due: string; text: string }> = [
  1232 |     { row: 'a', service: 'SV-01', at: '2026-12-01T09:00:00+07:00', due: '2026-12-04T16:30:00+07:00', text: '4 ธ.ค. 2569 16:30' },
  1233 |     { row: 'b', service: 'SV-01', at: '2026-12-01T16:29:00+07:00', due: '2026-12-04T16:30:00+07:00', text: '4 ธ.ค. 2569 16:30' },
  1234 |     { row: 'c', service: 'SV-01', at: '2026-12-01T16:30:00+07:00', due: '2026-12-08T16:30:00+07:00', text: '8 ธ.ค. 2569 16:30' },
  1235 |     { row: 'd', service: 'SV-01', at: '2026-12-04T10:00:00+07:00', due: '2026-12-11T16:30:00+07:00', text: '11 ธ.ค. 2569 16:30' },
  1236 |     { row: 'e', service: 'SV-01', at: '2026-12-05T10:00:00+07:00', due: '2026-12-14T16:30:00+07:00', text: '14 ธ.ค. 2569 16:30' },
  1237 |     { row: 'f', service: 'SV-02', at: '2026-12-01T09:00:00+07:00', due: '2026-12-17T16:30:00+07:00', text: '17 ธ.ค. 2569 16:30' },
  1238 |     { row: 'g', service: 'SV-03', at: '2026-12-01T09:00:00+07:00', due: '2026-12-24T16:30:00+07:00', text: '24 ธ.ค. 2569 16:30' },
  1239 |     { row: 'h', service: 'SV-01', at: '2026-12-29T10:00:00+07:00', due: '2027-01-05T16:30:00+07:00', text: '5 ม.ค. 2570 16:30' },
  1240 |     { row: 'i', service: 'SV-01', at: '2026-12-31T23:59:00+07:00', due: '2027-01-07T16:30:00+07:00', text: '7 ม.ค. 2570 16:30' },
  1241 |   ];
  1242 |   for (const r of rows) {
  1243 |     await test.step(`แถว ${r.row}: ${r.service} ชำระ ${r.at}`, async () => {
  1244 |       await reset();
  1245 |       await setClock(r.at);
  1246 |       const s = await citizenSession(browser, ID.SOMCHAI);
  1247 |       const paid = await newPaid({ api: s.api, service: r.service, qty: 1, areaSqm: 100 });
  1248 |       expect(paid.caseNo).toBe(caseNo(31));
  1249 |       const c = await getCase(s.api, paid.caseNo);
> 1250 |       expect(c.dueAt).toBe(r.due);
       |                       ^ Error: expect(received).toBe(expected) // Object.is equality
  1251 |       await s.page.goto(`/citizen/cases/${paid.caseNo}`);
  1252 |       await expectDue(s.page, r.text, r.due);
  1253 |     });
  1254 |   }
  1255 | });
  1256 | 
  1257 | test('TC-SLA-02 หยุดนับ SLA ระหว่างรอแก้ไข', async ({ browser }) => {
  1258 |   test.setTimeout(360_000);
  1259 |   const NEW = caseNo(31);
  1260 |   const F01 = caseNo(17);
  1261 | 
  1262 |   await test.step('ส่วน 1 ตีกลับ 2 ธ.ค. ส่งแก้ 3 ธ.ค. (หยุด 1 วัน)', async () => {
  1263 |     await reset();
  1264 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1265 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1266 |     expect(paid.caseNo).toBe(NEW);
  1267 |     expect((await getCase(c.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1268 | 
  1269 |     await setClock('2026-12-02T11:00:00+07:00');
  1270 |     const o = await staffSession(browser, 'off.reg1');
  1271 |     await claim(o.api, NEW);
  1272 |     await returnCase(o.api, NEW, 'xxxxxxxxxx');
  1273 |     await o.page.goto(`/officer/cases/${NEW}`);
  1274 |     await expectStatus(o.page, 'NEED_FIX');
  1275 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1276 |     await expectStatus(c.page, 'NEED_FIX');
  1277 |     await expectLevel(c.page, 'paused');
  1278 |     await expect(tid(c.page, 'fix-deadline')).toHaveAttribute('data-iso', '2026-12-09T11:00:00+07:00');
  1279 | 
  1280 |     await setClock('2026-12-03T10:00:00+07:00');
  1281 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1282 |     await tid(c.page, 'submit-fix-btn').click();
  1283 |     await expectStatus(c.page, 'IN_REVIEW');
  1284 |     await expectDue(c.page, '8 ธ.ค. 2569 16:30', '2026-12-08T16:30:00+07:00');
  1285 |     await expectLevel(c.page, 'normal');
  1286 |     const got = await getCase(o.api, NEW);
  1287 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1288 |     expect(got.owner).toBe('off.reg1');
  1289 |     await o.page.goto(`/officer/cases/${NEW}`);
  1290 |     await expect(tid(o.page, 'case-owner')).toHaveText('off.reg1');
  1291 |   });
  1292 | 
  1293 |   await test.step('ส่วน 2 seed …000017 ส่งแก้ 1 ธ.ค. 09:00 (หยุด 2 วัน)', async () => {
  1294 |     await reset();
  1295 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1296 |     await c.page.goto(`/citizen/cases/${F01}`);
  1297 |     await expectLevel(c.page, 'paused');
  1298 |     await expect(tid(c.page, 'sla-due')).toHaveAttribute('data-iso', '2026-11-27T16:30:00+07:00');
  1299 |     await tid(c.page, 'submit-fix-btn').click();
  1300 |     await expectStatus(c.page, 'IN_REVIEW');
  1301 |     await expectDue(c.page, '1 ธ.ค. 2569 16:30', '2026-12-01T16:30:00+07:00');
  1302 |     await expectLevel(c.page, 'near');
  1303 |     const reg1 = await loginStaff('off.reg1');
  1304 |     const got = await getCase(reg1, F01);
  1305 |     expect(got.dueAt).toBe('2026-12-01T16:30:00+07:00');
  1306 |     expect(got.owner).toBe('off.reg1');
  1307 |   });
  1308 | 
  1309 |   await test.step('ส่วน 3 ส่งแก้ …000017 วันที่ 4 ธ.ค. 10:00 (หยุด 5 วัน)', async () => {
  1310 |     await reset();
  1311 |     await setClock('2026-12-04T10:00:00+07:00');
  1312 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1313 |     const r = await resubmit(c.api, F01);
  1314 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1315 |     const got = await getCase(c.api, F01);
  1316 |     expect(got.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1317 |     expect(got.slaLevel).toBe('near');
  1318 |     await c.page.goto(`/citizen/cases/${F01}`);
  1319 |     await expectLevel(c.page, 'near');
  1320 |   });
  1321 | 
  1322 |   await test.step('ส่วน 4 ตีกลับและส่งแก้วันเดียวกัน (หยุด 0 วัน)', async () => {
  1323 |     await reset();
  1324 |     const paid = await newPaid({ idNo: ID.SOMCHAI, service: 'SV-01', qty: 1 });
  1325 |     expect(paid.caseNo).toBe(NEW);
  1326 |     await setClock('2026-12-02T09:00:00+07:00');
  1327 |     const reg1 = await loginStaff('off.reg1');
  1328 |     await claim(reg1, NEW);
  1329 |     await returnCase(reg1, NEW);
  1330 |     await setClock('2026-12-02T15:00:00+07:00');
  1331 |     const r = await resubmit(paid.api, NEW);
  1332 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1333 |     expect((await getCase(paid.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1334 |   });
  1335 | 
  1336 |   await test.step('ส่วน 5 คร่อมสุดสัปดาห์/วันหยุด ส่งแก้หลัง 16:30', async () => {
  1337 |     await reset();
  1338 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1339 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1340 |     expect(paid.caseNo).toBe(NEW);
  1341 |     await setClock('2026-12-04T10:00:00+07:00');
  1342 |     const reg1 = await loginStaff('off.reg1');
  1343 |     await claim(reg1, NEW);
  1344 |     await returnCase(reg1, NEW);
  1345 |     await setClock('2026-12-08T17:00:00+07:00');
  1346 |     const r = await resubmit(c.api, NEW);
  1347 |     expect(r.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1348 |     const got = await getCase(c.api, NEW);
  1349 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1350 |     expect(got.slaLevel).toBe('overdue');
```