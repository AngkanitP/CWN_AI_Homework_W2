# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part1.spec.ts >> TC-SLA-01 กำหนดเสร็จตามตารางวันที่
- Location: tests/part1.spec.ts:1221:1

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
            - /url: /api/files/f_2958d898448251a1ed24980b
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
  1142 |     expect((await getCase(reg2, NO)).owner).toBe('off.reg1');
  1143 |     expect(await queueItems(reg2, 'mine')).toHaveLength(9);
  1144 |     const s2 = await staffSession(browser, 'off.reg2');
  1145 |     await expectWorkload(s2.page, 9);
  1146 |     await expectApi(claimRaw(reg1, NO), 409, 'ALREADY_CLAIMED');
  1147 |     expect((await getCase(reg1, NO)).owner).toBe('off.reg1');
  1148 |     expect(await claimAuditCount(NO)).toBe(1);
  1149 |   });
  1150 | });
  1151 | 
  1152 | test('TC-QUEUE-03 งานในมือสูงสุด 10', async ({ browser }) => {
  1153 |   test.setTimeout(240_000);
  1154 |   await reset();
  1155 |   let s = await staffSession(browser, 'off.reg2');
  1156 |   let p = s.page;
  1157 |   const claimUi = async (n: number) => {
  1158 |     await p.goto('/officer/queue');
  1159 |     await withMutation(p, () => queueRow(p, caseNo(n)).getByTestId('claim-btn').click());
  1160 |   };
  1161 | 
  1162 |   // 1
  1163 |   await expectWorkload(p, 9);
  1164 |   // 2 ครั้งที่ 10
  1165 |   await claimUi(28);
  1166 |   await expect(tid(p, 'action-error')).toBeHidden();
  1167 |   await expectWorkload(p, 10);
  1168 |   expect((await getCase(s.api, caseNo(28))).owner).toBe('off.reg2');
  1169 |   // 3 ครั้งที่ 11 → เพดาน
  1170 |   await claimUi(29);
  1171 |   await expect(tid(p, 'action-error')).toHaveText(MSG.WORKLOAD_LIMIT);
  1172 |   const lim = await expectApi(claimRaw(s.api, caseNo(29)), 409, 'WORKLOAD_LIMIT');
  1173 |   expect(lim.message).toBe(MSG.WORKLOAD_LIMIT);
  1174 |   const c29 = await getCase(s.api, caseNo(29));
  1175 |   expect(c29.status).toBe('SUBMITTED');
  1176 |   expect(c29.owner || null).toBeNull();
  1177 |   await expectWorkload(p, 10);
  1178 |   // 4 อนุมัติ …000025 (SV-01 ของตัวเอง) → APPROVED ไม่นับ
  1179 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1180 |   await tid(p, 'approve-btn').click();
  1181 |   await expectStatus(p, 'APPROVED');
  1182 |   await expectWorkload(p, 9);
  1183 |   // 5
  1184 |   await claimUi(29);
  1185 |   await expectWorkload(p, 10);
  1186 |   expect((await getCase(s.api, caseNo(29))).owner).toBe('off.reg2');
  1187 |   // 6 off.reg1 (งานในมือ 3) ไม่ติดเพดาน
  1188 |   const reg1 = await loginStaff('off.reg1');
  1189 |   expect((await claim(reg1, caseNo(30))).owner).toBe('off.reg1');
  1190 | 
  1191 |   // 7 RESET · ตีกลับ …000025 → NEED_FIX ไม่นับ
  1192 |   await reset();
  1193 |   s = await staffSession(browser, 'off.reg2');
  1194 |   p = s.page;
  1195 |   await p.goto(`/officer/cases/${caseNo(25)}`);
  1196 |   await tid(p, 'return-btn').click();
  1197 |   await tid(p, 'return-reason').fill('xxxxxxxxxx');
  1198 |   await tid(p, 'return-submit').click();
  1199 |   await expectStatus(p, 'NEED_FIX');
  1200 |   await expectWorkload(p, 8);
  1201 |   // 8
  1202 |   await claimUi(28);
  1203 |   await claimUi(29);
  1204 |   await expectWorkload(p, 10);
  1205 |   // 9 สมหญิงส่งแก้ → คืนผู้ถือเดิมแม้เกิน 10
  1206 |   const c = await citizenSession(browser, ID.SOMYING);
  1207 |   await c.page.goto(`/citizen/cases/${caseNo(25)}`);
  1208 |   await tid(c.page, 'submit-fix-btn').click();
  1209 |   await expect(tid(c.page, 'action-error')).toBeHidden();
  1210 |   await expectStatus(c.page, 'IN_REVIEW');
  1211 |   expect((await getCase(s.api, caseNo(25))).owner).toBe('off.reg2');
  1212 |   await expectWorkload(p, 11);
  1213 |   // 10 รับเพิ่มไม่ได้
  1214 |   const b10 = await expectApi(claimRaw(s.api, caseNo(30)), 409, 'WORKLOAD_LIMIT');
  1215 |   expect(b10.message).toBe(MSG.WORKLOAD_LIMIT);
  1216 |   await expectWorkload(p, 11);
  1217 | });
  1218 | 
  1219 | // ═══════════════════════════════════ SLA ═══════════════════════════════════
  1220 | 
  1221 | test('TC-SLA-01 กำหนดเสร็จตามตารางวันที่', async ({ browser }) => {
  1222 |   test.setTimeout(360_000);
  1223 |   const rows: Array<{ row: string; service: 'SV-01' | 'SV-02' | 'SV-03'; at: string; due: string; text: string }> = [
  1224 |     { row: 'a', service: 'SV-01', at: '2026-12-01T09:00:00+07:00', due: '2026-12-04T16:30:00+07:00', text: '4 ธ.ค. 2569 16:30' },
  1225 |     { row: 'b', service: 'SV-01', at: '2026-12-01T16:29:00+07:00', due: '2026-12-04T16:30:00+07:00', text: '4 ธ.ค. 2569 16:30' },
  1226 |     { row: 'c', service: 'SV-01', at: '2026-12-01T16:30:00+07:00', due: '2026-12-08T16:30:00+07:00', text: '8 ธ.ค. 2569 16:30' },
  1227 |     { row: 'd', service: 'SV-01', at: '2026-12-04T10:00:00+07:00', due: '2026-12-11T16:30:00+07:00', text: '11 ธ.ค. 2569 16:30' },
  1228 |     { row: 'e', service: 'SV-01', at: '2026-12-05T10:00:00+07:00', due: '2026-12-14T16:30:00+07:00', text: '14 ธ.ค. 2569 16:30' },
  1229 |     { row: 'f', service: 'SV-02', at: '2026-12-01T09:00:00+07:00', due: '2026-12-17T16:30:00+07:00', text: '17 ธ.ค. 2569 16:30' },
  1230 |     { row: 'g', service: 'SV-03', at: '2026-12-01T09:00:00+07:00', due: '2026-12-24T16:30:00+07:00', text: '24 ธ.ค. 2569 16:30' },
  1231 |     { row: 'h', service: 'SV-01', at: '2026-12-29T10:00:00+07:00', due: '2027-01-05T16:30:00+07:00', text: '5 ม.ค. 2570 16:30' },
  1232 |     { row: 'i', service: 'SV-01', at: '2026-12-31T23:59:00+07:00', due: '2027-01-07T16:30:00+07:00', text: '7 ม.ค. 2570 16:30' },
  1233 |   ];
  1234 |   for (const r of rows) {
  1235 |     await test.step(`แถว ${r.row}: ${r.service} ชำระ ${r.at}`, async () => {
  1236 |       await reset();
  1237 |       await setClock(r.at);
  1238 |       const s = await citizenSession(browser, ID.SOMCHAI);
  1239 |       const paid = await newPaid({ api: s.api, service: r.service, qty: 1, areaSqm: 100 });
  1240 |       expect(paid.caseNo).toBe(caseNo(31));
  1241 |       const c = await getCase(s.api, paid.caseNo);
> 1242 |       expect(c.dueAt).toBe(r.due);
       |                       ^ Error: expect(received).toBe(expected) // Object.is equality
  1243 |       await s.page.goto(`/citizen/cases/${paid.caseNo}`);
  1244 |       await expectDue(s.page, r.text, r.due);
  1245 |     });
  1246 |   }
  1247 | });
  1248 | 
  1249 | test('TC-SLA-02 หยุดนับ SLA ระหว่างรอแก้ไข', async ({ browser }) => {
  1250 |   test.setTimeout(360_000);
  1251 |   const NEW = caseNo(31);
  1252 |   const F01 = caseNo(17);
  1253 | 
  1254 |   await test.step('ส่วน 1 ตีกลับ 2 ธ.ค. ส่งแก้ 3 ธ.ค. (หยุด 1 วัน)', async () => {
  1255 |     await reset();
  1256 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1257 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1258 |     expect(paid.caseNo).toBe(NEW);
  1259 |     expect((await getCase(c.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1260 | 
  1261 |     await setClock('2026-12-02T11:00:00+07:00');
  1262 |     const o = await staffSession(browser, 'off.reg1');
  1263 |     await claim(o.api, NEW);
  1264 |     await returnCase(o.api, NEW, 'xxxxxxxxxx');
  1265 |     await o.page.goto(`/officer/cases/${NEW}`);
  1266 |     await expectStatus(o.page, 'NEED_FIX');
  1267 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1268 |     await expectStatus(c.page, 'NEED_FIX');
  1269 |     await expectLevel(c.page, 'paused');
  1270 |     await expect(tid(c.page, 'fix-deadline')).toHaveAttribute('data-iso', '2026-12-09T11:00:00+07:00');
  1271 | 
  1272 |     await setClock('2026-12-03T10:00:00+07:00');
  1273 |     await c.page.goto(`/citizen/cases/${NEW}`);
  1274 |     await tid(c.page, 'submit-fix-btn').click();
  1275 |     await expectStatus(c.page, 'IN_REVIEW');
  1276 |     await expectDue(c.page, '8 ธ.ค. 2569 16:30', '2026-12-08T16:30:00+07:00');
  1277 |     await expectLevel(c.page, 'normal');
  1278 |     const got = await getCase(o.api, NEW);
  1279 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1280 |     expect(got.owner).toBe('off.reg1');
  1281 |     await o.page.goto(`/officer/cases/${NEW}`);
  1282 |     await expect(tid(o.page, 'case-owner')).toHaveText('off.reg1');
  1283 |   });
  1284 | 
  1285 |   await test.step('ส่วน 2 seed …000017 ส่งแก้ 1 ธ.ค. 09:00 (หยุด 2 วัน)', async () => {
  1286 |     await reset();
  1287 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1288 |     await c.page.goto(`/citizen/cases/${F01}`);
  1289 |     await expectLevel(c.page, 'paused');
  1290 |     await expect(tid(c.page, 'sla-due')).toHaveAttribute('data-iso', '2026-11-27T16:30:00+07:00');
  1291 |     await tid(c.page, 'submit-fix-btn').click();
  1292 |     await expectStatus(c.page, 'IN_REVIEW');
  1293 |     await expectDue(c.page, '1 ธ.ค. 2569 16:30', '2026-12-01T16:30:00+07:00');
  1294 |     await expectLevel(c.page, 'near');
  1295 |     const reg1 = await loginStaff('off.reg1');
  1296 |     const got = await getCase(reg1, F01);
  1297 |     expect(got.dueAt).toBe('2026-12-01T16:30:00+07:00');
  1298 |     expect(got.owner).toBe('off.reg1');
  1299 |   });
  1300 | 
  1301 |   await test.step('ส่วน 3 ส่งแก้ …000017 วันที่ 4 ธ.ค. 10:00 (หยุด 5 วัน)', async () => {
  1302 |     await reset();
  1303 |     await setClock('2026-12-04T10:00:00+07:00');
  1304 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1305 |     const r = await resubmit(c.api, F01);
  1306 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1307 |     const got = await getCase(c.api, F01);
  1308 |     expect(got.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1309 |     expect(got.slaLevel).toBe('near');
  1310 |     await c.page.goto(`/citizen/cases/${F01}`);
  1311 |     await expectLevel(c.page, 'near');
  1312 |   });
  1313 | 
  1314 |   await test.step('ส่วน 4 ตีกลับและส่งแก้วันเดียวกัน (หยุด 0 วัน)', async () => {
  1315 |     await reset();
  1316 |     const paid = await newPaid({ idNo: ID.SOMCHAI, service: 'SV-01', qty: 1 });
  1317 |     expect(paid.caseNo).toBe(NEW);
  1318 |     await setClock('2026-12-02T09:00:00+07:00');
  1319 |     const reg1 = await loginStaff('off.reg1');
  1320 |     await claim(reg1, NEW);
  1321 |     await returnCase(reg1, NEW);
  1322 |     await setClock('2026-12-02T15:00:00+07:00');
  1323 |     const r = await resubmit(paid.api, NEW);
  1324 |     expect(r.dueAt).toBe('2026-12-04T16:30:00+07:00');
  1325 |     expect((await getCase(paid.api, NEW)).dueAt).toBe('2026-12-04T16:30:00+07:00');
  1326 |   });
  1327 | 
  1328 |   await test.step('ส่วน 5 คร่อมสุดสัปดาห์/วันหยุด ส่งแก้หลัง 16:30', async () => {
  1329 |     await reset();
  1330 |     const c = await citizenSession(browser, ID.SOMCHAI);
  1331 |     const paid = await newPaid({ api: c.api, service: 'SV-01', qty: 1 });
  1332 |     expect(paid.caseNo).toBe(NEW);
  1333 |     await setClock('2026-12-04T10:00:00+07:00');
  1334 |     const reg1 = await loginStaff('off.reg1');
  1335 |     await claim(reg1, NEW);
  1336 |     await returnCase(reg1, NEW);
  1337 |     await setClock('2026-12-08T17:00:00+07:00');
  1338 |     const r = await resubmit(c.api, NEW);
  1339 |     expect(r.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1340 |     const got = await getCase(c.api, NEW);
  1341 |     expect(got.dueAt).toBe('2026-12-08T16:30:00+07:00');
  1342 |     expect(got.slaLevel).toBe('overdue');
```